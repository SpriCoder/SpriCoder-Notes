Python 图片处理
---
1. 当图片被加载进来后，会是一个非常高维复杂的向量形式，本文主要包含对图片的灰度处理、二值化处理、降噪处理和SVD等降维手段。
2. 完成的代码在文末

# 1. 图片的灰度处理
```py
# encoding=utf8
from PIL import Image
 
def main():
	img = Image.open('RandomPicture.png')
	grey = image.convert('L')
  # 保存到当前目录下的grey.png中去
	grey.save('grey.png')
 
if __name__ == '__main__':
	main()
```

# 2. 灰度图的二值化
```py
def get_bin_table(threshold=200):
  '''
  获取灰度转二值的映射table
  0表示黑色,1表示白色
  :param threshold: 二值化的边界阈值
  :return:
  '''
  table = []
  for i in range(256):
    if i < threshold:
      table.append(0)
    else:
      table.append(1)
  return table

def main():
	image = Image.open('RandomPicture.png')
	grey = image.convert('L')
	table = get_bin_table()
	binary = grey.point(table, '1')
	binary.save('binary.png')
 
if __name__ == '__main__':
	main()
```

# 3. 图片降噪处理
1. 选择使用了9邻域法进行图片降噪

```py
def _sum_9_region_new(img, x, y):
  '''
  确认噪声点
  :param img:图片
  :param x:
  :param y:
  :return:
  '''
  # 获取当前的像素点的值
  cur_pixel = img.getpixel((x, y))
  width = img.width
  height = img.height

  # 白色区域不统计领域降噪
  if cur_pixel == 1:
    return 0

  # 对于前几行进行降噪
  if y < 3:
    return 1
  # 对最后几行进行降噪
  elif y > height - 3:
    return 1
  # 目前处理的是中间几行
  else:
    # 前两列进行降噪
    if x < 3:
      return 1
    # 最后两列进行降噪
    elif x == width - 1:
      return 1
    # 对中间区域进行九邻域降噪
    else:
      sum = img.getpixel((x - 1, y - 1)) \
            + img.getpixel((x - 1, y)) \
            + img.getpixel((x - 1, y + 1)) \
            + img.getpixel((x, y - 1)) \
            + cur_pixel \
            + img.getpixel((x, y + 1)) \
            + img.getpixel((x + 1, y - 1)) \
            + img.getpixel((x + 1, y)) \
            + img.getpixel((x + 1, y + 1))
      return 9 - sum

def _collect_noise_point(img):
  '''
  搜索到所有的噪声点
  :param img: 图片数组
  :return:
  '''
  noise_point_list = []
  for x in range(img.width):
    for y in range(img.height):
      res_9 = _sum_9_region_new(img, x, y)
    # 找到孤立的点
      if (0 < res_9 < 3) and img.getpixel((x, y)) == 0:
        pos = (x, y)
        noise_point_list.append(pos)
  return noise_point_list

def _remove_noise_pixel(img, noise_point_list):
  '''
  根据噪点的位置信息，消除二值图片的黑点噪声
  :param img: 图片数组
  :param noise_point_list: 统计到的噪声点的情况
  :return:
  '''
  for item in noise_point_list:
    img.putpixel((item[0], item[1]), 1)

def main():
  binary = Image.open('binary.png')
  noise_point_list = _collect_noise_point(binary)
  _remove_noise_pixel(binary, noise_point_list)
```

# 4. SVD操作
1. 对图片进行SVD操作，从而降低图片的数字的大小，尽量让信息压缩，提高信息密度

```py
def _restore(u, sigma, v, k):
  '''
  转换成图片数组
  :param u:
  :param sigma:
  :param v:
  :param k:
  :return:
  '''
  a = np.dot(u[:, :k], np.diag(sigma[:k])).dot(v[:k, :])
  a[a < 0] = 0
  a[a > 255] = 255
  return np.rint(a).astype('uint8')

def _SVD(frame, K = 10):
  '''
  进行SVD操作
  :param frame: 图片数组
  :param K: 保留特征值数量
  :return:
  '''
  a = np.array(frame)
  # 由于是彩色图像，所以3通道。a的最内层数组为三个数，分别表示RGB，用来表示一个像素
  u_r, sigma_r, v_r = np.linalg.svd(a[:, :, 0])
  u_g, sigma_g, v_g = np.linalg.svd(a[:, :, 1])
  u_b, sigma_b, v_b = np.linalg.svd(a[:, :, 2])

  R = _restore(u_r, sigma_r, v_r, K)
  G = _restore(u_g, sigma_g, v_g, K)
  B = _restore(u_b, sigma_b, v_b, K)
  I = np.stack((R, G, B), axis=2)
  return I
```

# 5. 图像预处理完整代码
```py
# -*- coding: utf-8 -*-
from PIL import Image
from tqdm import tqdm
import numpy as np
import os

class PreDigest():
    def __init__(self, source, dirpath, K, block, number):
        '''
        预处理初始化类
        :param source: 图片原路径
        :param dirpath: 保存目录路径
        :param K: 保留的特征值数量
        :param block: 二值化操作梯度的大小
        :param number: 进行二值化操作的次数
        '''
        self.source = source
        self.dirpath = dirpath
        self.K = K
        self.block = block
        self.number = number

    def _get_bin_table(self, threshold=200):
        '''
        获取灰度转二值的映射table
        0表示黑色,1表示白色
        :param threshold: 二值化的边界阈值
        :return:
        '''
        table = []
        for i in range(256):
            if i < threshold:
                table.append(0)
            else:
                table.append(1)
        return table

    def _sum_9_region_new(self, img, x, y):
        '''
        确认噪声点
        :param img:图片
        :param x:
        :param y:
        :return:
        '''
        # 获取当前的像素点的值
        cur_pixel = img.getpixel((x, y))
        width = img.width
        height = img.height

        # 白色区域不统计领域降噪
        if cur_pixel == 1:
            return 0

        # 对于前几行进行降噪
        if y < 3:
            return 1
        # 对最后几行进行降噪
        elif y > height - 3:
            return 1
        # 目前处理的是中间几行
        else:
            # 前两列进行降噪
            if x < 3:
                return 1
            # 最后两行进行降噪
            elif x == width - 1:
                return 1
            # 对中间区域进行九邻域降噪
            else:
                sum = img.getpixel((x - 1, y - 1)) \
                      + img.getpixel((x - 1, y)) \
                      + img.getpixel((x - 1, y + 1)) \
                      + img.getpixel((x, y - 1)) \
                      + cur_pixel \
                      + img.getpixel((x, y + 1)) \
                      + img.getpixel((x + 1, y - 1)) \
                      + img.getpixel((x + 1, y)) \
                      + img.getpixel((x + 1, y + 1))
                return 9 - sum

    def _collect_noise_point(self, img):
        '''
        搜索到所有的噪声点
        :param img: 图片数组
        :return:
        '''
        noise_point_list = []
        for x in range(img.width):
            for y in range(img.height):
                res_9 = self._sum_9_region_new(img, x, y)
                # 找到孤立的点
                if (0 < res_9 < 3) and img.getpixel((x, y)) == 0:
                    pos = (x, y)
                    noise_point_list.append(pos)
        return noise_point_list

    def _remove_noise_pixel(self, img, noise_point_list):
        '''
        根据噪点的位置信息，消除二值图片的黑点噪声
        :param img: 图片数组
        :param noise_point_list: 统计到的噪声点的情况
        :return:
        '''
        for item in noise_point_list:
            img.putpixel((item[0], item[1]), 1)

    def _restore(self, u, sigma, v, k):
        '''
        转换成图片数组
        :param u:
        :param sigma:
        :param v:
        :param k:
        :return:
        '''
        a = np.dot(u[:, :k], np.diag(sigma[:k])).dot(v[:k, :])
        a[a < 0] = 0
        a[a > 255] = 255
        return np.rint(a).astype('uint8')

    def _SVD(self, frame, K = 10):
        '''
        进行SVD操作
        :param frame: 图片数组
        :param K: 保留特征值数量
        :return:
        '''
        a = np.array(frame)
        # 由于是彩色图像，所以3通道。a的最内层数组为三个数，分别表示RGB，用来表示一个像素
        u_r, sigma_r, v_r = np.linalg.svd(a[:, :, 0])
        u_g, sigma_g, v_g = np.linalg.svd(a[:, :, 1])
        u_b, sigma_b, v_b = np.linalg.svd(a[:, :, 2])

        R = self._restore(u_r, sigma_r, v_r, K)
        G = self._restore(u_g, sigma_g, v_g, K)
        B = self._restore(u_b, sigma_b, v_b, K)
        I = np.stack((R, G, B), axis=2)
        return I

    def _pre_digest(self, gray, threshold):
        table = self._get_bin_table(threshold)
        binary = gray.point(table, '1')
        noise_point_list = self._collect_noise_point(binary)
        self._remove_noise_pixel(binary, noise_point_list)
        binary.save(os.path.join(self.dirpath, "T matrix_" + str(threshold) + ".png"))

    def _svd_img(self, filepath):
        '''
        开始执行svd操作
        :param filepath:
        :return:
        '''
        img = Image.open(filepath)
        svd_array = self._SVD(img, self.K)
        svd_img = Image.fromarray(svd_array)
        new_path = os.path.join(self.dirpath, "T matrix_svd.png")
        svd_img.save(new_path)
        return new_path

    def run(self):
        print("开始SVD处理!")
        new_path = self._svd_img(self.source)
        print("结束SVD处理!")
        img = Image.open(new_path)
        gray = img.convert('L')
        gray.save(os.path.join(self.dirpath, "T matrix_grey.png"))
        for i in tqdm(range(1, self.number)):
            self._pre_digest(gray, self.block * i)

if __name__ == '__main__':
    K = 400
    block = 25
    number = int(256 / block)
    dir_path = "./after_img_" + str(K) + "_" + str(block)
    if(not os.path.exists(dir_path)):
        os.mkdir(dir_path)
    tmp = PreDigest("./img/T matrix.png", dir_path, K, block, number)
    tmp.run()
```

# 6. 将Numpy数组保存为图像的方法

## 6.1. 使用Scipy.misc来保存
1. 标准化图像版本:min(data)是黑色，max(data)白色

```py
import scipy.misc
scipy.misc.imsave('outfile.jpg', image_array)
```

2. 如果是精确的灰度级或标准RGB通道使用如下操作

```py
import scipy.misc
scipy.misc.toimage(image_array, cmin=0.0, cmax=...).save('outfile.jpg')
```

## 6.2. 使用PIL
1. 对于一个给定的numpy数组A

```py
from PIL import Image
im = Image.fromarray(A)
im.save("your_file.jpeg")
```

## 6.3. 使用matplotlib
1. 使用本身matplotlib

```py
import matplotlib
matplotlib.image.imsave('name.png', array)
```

1. 使用matplotlib.pyplot

```py
import matplotlib.pyplot as plt
plt.imshow(matrix) #Needs to be in row,col order
plt.savefig(filename)
```

## 6.4. 使用Opencv
```py
import cv2
import numpy as np
 
cv2.imwrite("filename.png", np.zeros((10,10)))
```

# 7. 使用Mathpix API自制Mathpix snipping
1. mathpix是一款非常好用的img2Latex的软件。
2. 官方开放了API，每个月有1000次免费使用的机会。

## 7.1. 注册API接口账号
1. 首先去<a href = "https://dashboard.mathpix.com/login">官网</a>注册一个mathpix的账号
2. 然后接受一个**激活协议**，输入信用卡激活账号
3. 之后从Account Information中找到API keys，拿到app_id和app_key即可

## 7.2. 配置情况
1. 使用pyqt5完成UI界面制作，再使用qss进行一定优化

```py
# 包依赖
import sys
import os
import base64
import requests
import json
import PyQt5.QtGui
import PyQt5.QtCore
from PyQt5.QtWidgets import QApplication, QLabel, QPushButton, QWidget, QGridLayout, QLineEdit
from PyQt5.QtCore import Qt
from PIL import ImageGrab
import pyperclip
import matplotlib.pyplot as plt
```

## 7.3. 完整代码
```py
# coding:utf-8
import sys
import os
import base64
import requests
import json
import PyQt5.QtGui
import PyQt5.QtCore
from PyQt5.QtWidgets import QApplication, QLabel, QPushButton, QWidget, QGridLayout, QLineEdit
from PyQt5.QtCore import Qt
from PIL import ImageGrab
import pyperclip
import matplotlib.pyplot as plt

env = os.environ

default_headers = {
    'app_id': env.get('APP_ID', '你的APP_ID'),
    'app_key': env.get('APP_KEY', '你的APP_KEY'),
    'Content-type': 'application/json'
}

service = 'https://api.mathpix.com/v3/latex'

class Img2Latex(QWidget):

    def __init__(self):
        super().__init__()
        self.initUI()

    def initUI(self):
        self.setGeometry(300, 300, 800, 700)
        self.setWindowTitle('Img2Latex')

        # copy latex
        self.Latex1copyBtn = QPushButton()
        self.Latex2copyBtn = QPushButton()
        self.Latex3copyBtn = QPushButton()
        # set copy btn icon
        self.Latex1copyBtn.setIcon(PyQt5.QtGui.QIcon(r".\img\copy.png"))
        self.Latex2copyBtn.setIcon(PyQt5.QtGui.QIcon(r".\img\copy.png"))
        self.Latex3copyBtn.setIcon(PyQt5.QtGui.QIcon(r".\img\copy.png"))

        # edit latex
        self.Latex1EditBtn = QPushButton()
        self.Latex2EditBtn = QPushButton()
        self.Latex3EditBtn = QPushButton()
        # set edit btn icon
        self.Latex1EditBtn.setIcon(PyQt5.QtGui.QIcon(r".\img\edit.png"))
        self.Latex2EditBtn.setIcon(PyQt5.QtGui.QIcon(r".\img\edit.png"))
        self.Latex3EditBtn.setIcon(PyQt5.QtGui.QIcon(r".\img\edit.png"))

        # img to latex convert btn
        self.img2latexBtn = QPushButton('convert')

        # show the picture on clipboard
        self.imgLable = QLabel()

        # show the formula in latex
        self.Latex1Edit = QLineEdit()
        self.Latex2Edit = QLineEdit()
        self.Latex3Edit = QLineEdit()
        self.Latex1Edit.setEnabled(False)
        self.Latex2Edit.setEnabled(False)
        self.Latex3Edit.setEnabled(False)

        # # show the convert latex result
        # self.reviewImgLable = QLabel()
        # self.reviewImgLable.setStyleSheet("border: 2px solid red")

        grid = QGridLayout()
        grid.setSpacing(20)

        # 排版
        grid.addWidget(self.imgLable, 1, 0, 5, 3)

        grid.addWidget(self.img2latexBtn,6,0,1,2)

        grid.addWidget(self.Latex1Edit, 7, 0)
        grid.addWidget(self.Latex1copyBtn, 7, 1)
        # grid.addWidget(self.Latex1EditBtn, 7, 2)

        grid.addWidget(self.Latex2copyBtn, 8, 1)
        grid.addWidget(self.Latex2Edit, 8, 0)
        # grid.addWidget(self.Latex2EditBtn, 8, 2)

        grid.addWidget(self.Latex3copyBtn, 9, 1)
        grid.addWidget(self.Latex3Edit, 9, 0)
        # grid.addWidget(self.Latex3EditBtn, 9, 2)

        # grid.addWidget(self.reviewImgLable, 10, 0, 4, 3)

        self.setLayout(grid)

        # sign and slot

        # img to latex convert
        self.img2latexBtn.clicked.connect(self.convert)

        # copy latex
        self.Latex1copyBtn.clicked.connect(self.copyLatex1)
        self.Latex2copyBtn.clicked.connect(self.copyLatex2)
        self.Latex3copyBtn.clicked.connect(self.copyLatex3)

        # beautify the window
        self.Beautify()
        self.show()

    def Beautify(self):
        self.setWindowOpacity(0.9)  # 设置窗口透明度
        # self.setAttribute(qtpy.QtCore.Qt.WA_TranslucentBackground) # 设置窗口背景透明
        # self.setWindowFlag(qtpy.QtCore.Qt.FramelessWindowHint) # 隐藏边框
        pe = PyQt5.QtGui.QPalette()
        self.setAutoFillBackground(True)
        # pe.setColor(PyQt5.QtGui.QPalette.Window, Qt.Black)  #设置背景色
        pe.setColor(PyQt5.QtGui.QPalette.Background, Qt.black)
        self.setPalette(pe)
        self.imgLable.setStyleSheet(
            ''' QLabel{
                border: 2px solid red;
                border-radius:15px;
                padding:2px 4px;
                background-color:#aaa;
            }''')
        
        self.Latex1Edit.setStyleSheet(
            '''QLineEdit{
                border:1px solid gray;
                border-radius:10px;
                padding:2px 4px;
                background-color:#ddd;
                height:35px;
                font-color:black;
                font-weight:1000;
                font-size:24px
            }''')
        self.Latex2Edit.setStyleSheet(
            '''QLineEdit{
                border:1px solid gray;
                border-radius:10px;
                padding:2px 4px;
                background-color:#ddd;
                height:35px;
                font-color:black;
                font-weight:1000;
                font-size:24px
            }''')
        self.Latex3Edit.setStyleSheet(
            '''QLineEdit{
                border:1px solid gray;
                border-radius:10px;
                padding:2px 4px;
                background-color:#ddd;
                height:35px;
                font-color:black;
                font-weight:1000;
                font-size:24px
            }''')

        self.Latex1copyBtn.setStyleSheet(
            '''QPushButton{
                border:1px solid gray;
                border-radius:4px;
                padding:5px 5px;
                height:35px

            }''')
        self.Latex2copyBtn.setStyleSheet(
            '''QPushButton{
                border:1px solid gray;
                border-radius:4px;
                padding:5px 5px;
                height:35px
            }''')
        self.Latex3copyBtn.setStyleSheet(
            '''QPushButton{
                border:1px solid gray;
                border-radius:4px;
                padding:5px 5px;
                height:35px
            }''')

        self.img2latexBtn.setStyleSheet(
            '''QPushButton{
                border:2px solid gray;
                border-radius:10px;
                padding:5px 5px;
                background-color:#555;
                font-size:24px;
                font-color:#fff;
                font-weight:700;
                font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
            }''')

    #
    # Return the base64 encoding of an image with the given filename.
    #

    def image_uri(self,filename):
        image_data = open(filename, "rb").read()
        return "data:image/jpg;base64," + base64.b64encode(image_data).decode()

    # Call the Mathpix service with the given arguments, headers, and timeout.
    def latex(self, args, headers=default_headers, timeout=30):
        r = requests.post(service,
                          data=json.dumps(args), headers=headers, timeout=timeout)
        return json.loads(r.text)

    def convert(self):
        self.grapclipboard()
        r = self.latex({
            'src':self.image_uri(r".\img\equa.png"),
            'formats': ['latex_simplified']
        })
        # print(r['latex_simplified'])
        latex1 = r['latex_simplified']

        # test
        # latex1='111'
        latex2 = '$' + latex1 + '$'
        latex3 = '$$' + latex1 + '$$'
        self.Latex1Edit.setText(latex1)
        self.Latex2Edit.setText(latex2)
        self.Latex3Edit.setText(latex3)

    def copyLatex1(self):
        # get the latex formula
        text = self.Latex1Edit.text()
        # copy it to clipboard
        pyperclip.copy(text)

    def copyLatex2(self):
        text = self.Latex2Edit.text()
        pyperclip.copy(text)

    def copyLatex3(self):
        text = self.Latex3Edit.text()
        pyperclip.copy(text)

    #
    # 识别剪贴板公式
    #
    def grapclipboard(self):
        im = ImageGrab.grabclipboard()
        im.save(r'.\img\equa.png', 'PNG')
        self.imgLable.setPixmap(PyQt5.QtGui.QPixmap(r'.\img\equa.png'))

    #
    # 为程序添加快捷键
    #
	# 可以自己定义
    def keyPressEvent(self, event):
        if (event.key() == Qt.Key_T)and(event.modifiers() == Qt.AltModifier):
            self.convert()
        if (event.key() == Qt.Key_C)and(event.modifiers() == Qt.AltModifier):
            self.copyLatex3()

if __name__ == '__main__':
    app = QApplication(sys.argv)
    ex = Img2Latex()
    sys.exit(app.exec_())
```

> <a href = "https://dashboard.mathpix.com/user-data">所有接口的调用记录</a>
> <a href = "https://github.com/Joshua-li-yi/img2latex">完整的项目参考</a>

## 7.4. 官方参考
1. <a href = "https://docs.mathpix.com/">官方mathpix接口文档</a>
2. <a href = "https://github.com/Mathpix/api-examples">官方的API示例</a>

# 8. 参考
1. <a herf = "https://blog.csdn.net/u012067766/article/details/80013611">使用python PIL库实现简单验证码的去噪</a>
2. <a href = "https://blog.csdn.net/zhuoyuezai/article/details/79635120">如何将Numpy数组保存为图像</a>
3. <a href = "https://blog.csdn.net/m0_37772174/article/details/102886027">SVD应用于图像压缩 Python代码测试</a>
4. <a href = "https://blog.csdn.net/weixin_44984664/article/details/105242426">调用Mathpix API 自制Mathpix snipping (每月1000次免费！！！)</a>