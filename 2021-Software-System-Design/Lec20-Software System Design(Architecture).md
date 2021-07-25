Lec20-Software System Design(Architecture)
---

# 1. Outline
1. Soffware Architecture
2. Quality Atributes
3. Architecture Patterns
4. Designing Software Architecture
5. Documenting Software Architecture
6. Evaluating Software Architecture
7. Describing Architecture
8. Microservice Architecture *

# 2. Software Architecture in General
1. What is software architecture?
   1. Structure, Elements, Relationships, Design
2. What does a software architect do?
3. Where do architectures come from?
   1. NFRs, ASRs, Quality Requirements; Stakeholders, Organisations, Technical Enironmes...
4. Architecture Views
   1. Logical view, Process view, Physical view, Development view + Use case scenaris...
5. Architectural acivities and process
6. Software architecture knowledge areas

# 3. Architecture Process
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec20/1.png)

# 4. Quality Attributes
1. Soffware Requirements
   1. Functional requirements, Quality requirements (NFRs), Constraints
2. Quality Atributes
   1. Modeling quality ttribute scenaris: Source, Stimulus, Artefact, Envronment, Response, Measure
   2. Availability, Interoperbility, Modifabilit, Performance, Security, Testability, Usability, Xclilty...
   3. Tatics for quality atributes
3. Architecturally Significant Requirements
   1. How to gather and identify ASRs: Requirements, Interviews, Business goals, Utiliy tree 

# 5. Architecture Patterns
1. Architecture Patterns
   1. Context, Problem, Solution: elements + relations + constraints
2. Module Patterns
   1. Layered pattern
3. Component-Connector Patterns
   1. Broker pattern, Model-view-controller pattern, Pipe-and-filter pattern, Client-server pattern, Peer-to-peer pattern,Service-oriented pattern, Publish-subscribe pattern, Share-data pattern
4. Allocation Patterns
   1. Map-reduce pattern, Multi-tier pattern
5. Patterns vs. Tactics

# 6. Designing Architecture
1. General Design Strategy
   1. Abstraction, Decomposition, Divide & conquer, Generation and test, Iteration, Reuse
2. Attribute-Driven Design (ADD)
   1. Choose a part to design
   2. Marshal all ASRs for that part
   3. Create and test a design for that part
   4. Inputs to and outputs of ADD
   5. 8-step process: 1. confirm requirements, 2. choose an element to decompose, 3. identify ASRs, 4. choose a design satisfying ASRs, 5. instantiate elements & allocate responsibilities, 6. define interface, 7. verify & refine requirements, 8. repeat step 2-7 until all ASRs satisfied

# 7. Documenting Architecture
1. Views and Beyond
   1. Views:
      1. Styles (viewpoints), patterns and views
      2. Structural views: module views, component-and-connector views, allocation views
      3. Quality views
   2. Documenting views: 1. build stakeholder/view table, 2. combine views, 3. prioritise & stage
   3. Beyond views: documentation info & architecture info (mapping between views)
   4. Documentation : views + beyond

# 8. Evaluating Architecture
1. ATAM: Architecture Tradeoff Analysis Method
   1. Stakeholders involved in ATAM
   2. Inputs to and outputs of ATAM
   3. Phase 0: Partnership & preparation
   4. Phase 1: Evaluation - 1
      1. present ATAM, 2. present business drivers, 3. present architecture, 4. identify architectural approaches, 5. generate utility tree, 6. analyse architectural approaches
   5. Phase 2: Evaluation - 2
      1. present ATAM & results, 7. brainstorm & prioritize, 8. analyse architectural approaches, 9. present results
   6. Phase 3: Follow-up

# 9. Final Exam
1. 简答题、论述题、设计分析题
2. 英文题目、中文或英文答题
3. 个别题目可能需画图
4. 卷面分数 = 基础内容 60% + 高阶内容 40%
5. 总评成绩 = 平时作业 40% + 期末考试 60%