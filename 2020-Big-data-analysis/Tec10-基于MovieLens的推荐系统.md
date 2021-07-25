Tec10-基于MovieLens的推荐系统
---

# 1. 概述
1. 基于MovieLens数据集进行推荐
2. 使用了基于内容的推荐和基于协同过滤的推荐

# 2. 完整代码
```py
# -*- coding: utf-8 -*-
import csv
import time
import pandas as pd
import numpy as np
from tqdm import tqdm
from sklearn.feature_extraction.text import TfidfVectorizer
from sklearn.metrics.pairwise import linear_kernel
from sklearn.metrics.pairwise import cosine_similarity

class MyRecommend:
    def __init__(self, movie_data_path, rating_data_path, tags_data_path):
        self.movie_data = pd.read_csv(movie_data_path)
        self.movie_data['genres'] = self.movie_data["genres"].fillna("")
        self.rating_data = pd.read_csv(rating_data_path)
        self.tags_data = pd.read_csv(tags_data_path)
        self.movie_origin_source = {}
        self.user_average = {}
        self.movie_average = {}

    def init_similarity(self):
        user_ids = self.rating_data["userId"].drop_duplicates().sort_values()
        movie_ids = self.rating_data["movieId"].drop_duplicates().sort_values()
        i = 0
        for movie_id in movie_ids:
            self.movie_origin_source[movie_id] = i
            i += 1

        all_user_matrix = []
        zeros = []
        for x in range(len(movie_ids)):
            zeros.append(0)
        for user_id in tqdm(user_ids):
            tmp = zeros.copy()
            seen_movies = self.rating_data[self.rating_data["userId"] == user_id]
            seen_movies_ids = seen_movies["movieId"]
            for seen_movies_id in seen_movies_ids:
                position = self.movie_origin_source[seen_movies_id]
                tmp[position] = seen_movies[seen_movies["movieId"] == seen_movies_id]["rating"].values[0]
            average = np.mean(tmp)
            self.user_average[user_id] = average
            for i in range(len(tmp)):
                tmp[i] -= average
            all_user_matrix.append(tmp)

        all_user_df = pd.DataFrame(all_user_matrix)
        all_user_matrix.clear()
        self.all_user_similarity = cosine_similarity(all_user_df.values)

        all_movie_matrix = []
        zeros = []
        for x in range(len(user_ids)):
            zeros.append(0)
        for movie_id in tqdm(movie_ids):
            tmp = zeros.copy()
            seen_users = self.rating_data[self.rating_data["movieId"] == movie_id]
            seen_users_ids = seen_users["userId"]
            for seen_user_id in seen_users_ids:
                tmp[seen_user_id - 1] = seen_users[seen_users["userId"] == seen_user_id]["rating"].values[0]
            average = np.mean(tmp)
            self.movie_average[movie_id] = average
            for i in range(len(tmp)):
                tmp[i] -= average
            all_movie_matrix.append(tmp)

        all_movie_df = pd.DataFrame(all_movie_matrix)
        all_movie_matrix.clear()
        self.all_movie_similarity = cosine_similarity(all_movie_df.values)

    def user_based_one(self, user_id, movie_id, is_seen=True):
        """
        用户-用户协同过滤
        预测 user_id 会给 movie_id 的评分
        :param is_seen:
        :param user_id:
        :param movie_id:
        :return:
        """
        # 用户 user_id 的全部评分信息
        user_ratings = self.rating_data[self.rating_data["userId"] == user_id]

        # 检查是不是没有评价过
        if len(user_ratings[user_ratings["movieId"] == movie_id].values) and is_seen:
            return 0.0

        # 看过影片 movie_id 的全部用户id
        seen_user_ids = self.rating_data[self.rating_data["movieId"] == movie_id]["userId"]
        # 用户相似度
        similarity_users = []
        weight_similarity = 0.0
        total_similarity = 0.0

        for seen_user_id in seen_user_ids:
            # 看过movie_id的电影的用户的全部评分情况
            seen_user_ratings = self.rating_data[self.rating_data["userId"] == seen_user_id]

            similarity = self.all_user_similarity[seen_user_id - 1][user_id - 1]
            similarity_user = [seen_user_id, similarity]
            similarity_users.append(similarity_user)

            weight_similarity += similarity * \
                                 seen_user_ratings[seen_user_ratings["movieId"] == movie_id]["rating"].values[0]
            total_similarity += similarity
        if total_similarity == 0.0 or total_similarity == 0:
            return 0.0
        return weight_similarity / total_similarity + self.user_average[user_id]

    def movie_based_one(self, user_id, movie_id, is_seen=True):
        """
        物品-物品协同过滤
        预测 user_id 会给 movie_id 的评分
        :param is_seen:
        :param user_id:
        :param movie_id:
        :return:
        """
        # movie_id的全部评分情况
        movie_ratings = self.rating_data[self.rating_data["movieId"] == movie_id]

        # 检查是不是没有评价过
        if len(movie_ratings[movie_ratings["userId"] == user_id].values) and is_seen:
            return 0.0

        # user_id 看过的所有影片 movie_id
        seen_movie_ids = self.rating_data[self.rating_data["userId"] == user_id]["movieId"]

        # 影片相似度
        similarity_movies = []
        weight_similarity = 0.0
        total_similarity = 0.0

        for seen_movie_id in seen_movie_ids:
            seen_movie_ratings = self.rating_data[self.rating_data["movieId"] == seen_movie_id]

            try:
                similarity = self.all_movie_similarity[self.movie_origin_source[seen_movie_id]][
                    self.movie_origin_source[movie_id]]
            except Exception as e:
                similarity = 0.0
            similarity_movie = [seen_movie_id, similarity]
            similarity_movies.append(similarity_movie)

            weight_similarity += similarity * \
                                 seen_movie_ratings[seen_movie_ratings["userId"] == user_id]["rating"].values[0]
            total_similarity += similarity
        result = weight_similarity / total_similarity
        if(movie_id not in self.movie_average):
            return result
        return result + self.movie_average[movie_id]

    def content_based_predict(self, movie_ids, seen_movie_ids, n=10):
        """
        找到和 movie_id 相似的电影
        :param movie_ids:
        :param seen_movie_ids: 已经看过的电影
        :param n: 推荐个数
        :return:
        """
        tfidf = TfidfVectorizer(stop_words="english")
        tfidf_matrix = tfidf.fit_transform(self.movie_data["genres"])
        # 计算余弦相似度
        cosine_sim = linear_kernel(tfidf_matrix, tfidf_matrix)

        # 建立电影列表索引，方便进行相互索引
        indices = pd.Series(self.movie_data.index, index=self.movie_data["movieId"]).drop_duplicates()

        similarities = {}
        for movie_id in movie_ids:
            idx = indices[movie_id]
            similarity = list(enumerate(cosine_sim[idx]))
            similarity = sorted(similarity, key=lambda x: x[1], reverse=True)
            similarity = similarity[1: 1 + int(n / 2)]
            for s in similarity:
                if s[0] in similarities or s[0] in seen_movie_ids:
                    continue
                else:
                    similarities[s[0]] = s[1]
        recommend_ids = list(similarities.keys())
        recommend_ids.sort(key=lambda x: similarities[x], reverse=True)
        movie_indices = recommend_ids[:n]
        recommends = self.movie_data["movieId"].iloc[movie_indices]
        return recommends

    def predict(self, user_ids, n=10, least_rating=3.0):
        """
        联合推荐，先通过内容推荐来缩小范围，然后使用协同过滤
        :param user_ids: 用户范围
        :param n:内容过滤输出为前10
        :param least_rating:最低可以接受的评分
        :return:
        """
        users_result = {}
        for user_id in tqdm(user_ids):
            # 推荐的电影
            result = []
            seen_movie_ids = self.rating_data[self.rating_data["userId"] == user_id]["movieId"].drop_duplicates()
            # 选择用户最喜欢的前n个电影
            love_movie_ids = self.rating_data[self.rating_data["userId"] == user_id].sort_values(by=["rating"]).head(n)[
                "movieId"].drop_duplicates()
            recommend_ids = self.content_based_predict(love_movie_ids, seen_movie_ids, n)
            for recommend_id in recommend_ids:
                result.append(recommend_id)
            # 进行协同过滤(物品和用户两种)，低于预测评分不进行推荐
            recommend_scores = []
            for recommend_id in recommend_ids:
                user_based_score = self.user_based_one(user_id, recommend_id)
                movie_based_score = self.movie_based_one(user_id, recommend_id)
                if user_based_score < least_rating and movie_based_score < least_rating:
                    continue
                recommend_scores.append([recommend_id, user_based_score, movie_based_score])
            recommend_scores.sort(key=lambda x: x[1] + x[2])
            # 推荐至少前2名
            if (len(recommend_scores) < 2):
                users_result[user_id] = [recommend_id[0] for recommend_id in recommend_scores]
            else:
                users_result[user_id] = [recommend_id[0] for recommend_id in recommend_scores[:2]]

        with open("result/movie" + str(time.time()) + ".csv", "w", encoding="utf-8", newline="") as f:
            writer = csv.writer(f)
            writer.writerow(["userId", "movieId"])
            for user_id in users_result.keys():
                for recommend_id in users_result[user_id]:
                    writer.writerow([user_id, recommend_id])

    def evaluate(self, user_ids, edges):
        """
        评估效果，以一个用户为例，检验协同过滤算法
        :param user_ids:
        :param edges: 边界
        :return:
        """
        valid = {}
        for edge in edges:
            valid[edge] = 0
        total = 0
        for user_id in user_ids:
            seen_movies = self.rating_data[self.rating_data["userId"] == user_id]
            seen_movie_ids = seen_movies["movieId"]
            total += len(seen_movie_ids)
            for seen_movie_id in tqdm(seen_movie_ids):
                real_score = seen_movies[seen_movies["movieId"] == seen_movie_id]["rating"].values[0]
                user_based_score = self.user_based_one(user_id, seen_movie_id, False)
                movie_based_score = self.movie_based_one(user_id, seen_movie_id, False)
                for edge in edges:
                    if (abs(real_score - user_based_score) <= edge or
                            abs(real_score - movie_based_score) <= edge):
                        valid[edge] += 1
        for edge in edges:
            print("上下浮动范围为" + str(edge) + "时的准确率为" + str(valid[edge] / total * 100) + "%")


if __name__ == '__main__':
    myRecommend = MyRecommend("./ml-latest-small/movies.csv",
                              "./ml-latest-small/ratings.csv",
                              "./ml-latest-small/tags.csv")
    myRecommend.init_similarity()
    print(myRecommend.user_based_one(1, 1, False))
    myRecommend.predict(range(611))
    myRecommend.evaluate(range(5), [0.25, 0.5, 0.75, 1])
```

# 3. 参考
1. <a href = "https://www.jianshu.com/p/9ada2ba92919?utm_campaign">分析9000部电影|一个简单的电影推荐系统</a>
2. <a href = "https://blog.csdn.net/weixin_26752765/article/details/108132875">基于MovieLens的电影推荐系统</a>
3. <a href = "https://blog.csdn.net/Joenyye/article/details/80912909">Python推荐算法案例(2)——基于内容的电影推荐</a>