1.新建一张花费表timespend，用于记录花费

| 字段名         | 类型     | 描述                                     |
| -------------- | -------- | ---------------------------------------- |
| id             | int      | 主键自增id                               |
| tapd_timespend | float    | tapd花费                                 |
| qa_timespend   | float    | 质效花费                                 |
| is_convert     | boolean  | 是否将tapd花费转换为质效花费， 默认False |
| timespend      | float    | 总花费，tapd转化后花费+质效花费          |
| project_id     | char     | 项目id                                   |
| main_id        | char     | 项目制id                                 |
| story_id       | char     | 需求id                                   |
| task_id        | char     | 任务id                                   |
| begin          | datetime | 开始时间                                 |
| endline        | datetime | 结束时间                                 |
| is_deleted     | boolean  | 是否删除，默认False                      |
| create_by      | char     | 创建人                                   |
| update_by      | char     | 更新人                                   |
| create_time    | datetime | 创建时间                                 |
| update_time    | datetime | 更新时间                                 |

2.同步机制

* 通过Django的Signals信号机制触发同步
* 项目制关联需求时触发一个自定义信号，拉取tapd花费数据并同步
* 每日更新，通过celery定时任务同步项目下未关闭需求的花费数据

3.此次修改影响的内容

| 影响的模块          | 影响的内容           |
| ------------------- | -------------------- |
| 个人工作台-工时管理 | 工时的增删改查       |
| 项目管理-项目概览   | 项目概览的图表展示   |
| 项目管理-项目制     | 项目制的工时统计展示 |
|                     |                      |

