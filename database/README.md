# 数据模型规划（尚未创建数据库）
| 表 | 关键字段 | 约束 |
| --- | --- | --- |
| users | id, username, password_hash, role | 用户名唯一；角色 reader/admin |
| categories | id, name | 分类名唯一 |
| books | id, title, author, category_id | 书目与实物副本分开 |
| book_copies | id, book_id, barcode, status | 条码唯一；available/borrowed/reserved |
| loans | id, user_id, copy_id, borrowed_at, due_at, returned_at | 一个副本最多一条未归还记录 |
| reservations | id, user_id, book_id, status, created_at, allocated_copy_id, expires_at | 同一读者同一书目不能重复有效预约 |
| notifications | id, user_id, loan_id, type, event_date, read_at | 逾期提醒以 loan_id/type/event_date 唯一去重 |

逾期规则：returned_at 为空且当前时间严格晚于 due_at；已归还记录不再提醒。
时间存储统一为 UTC，页面按 Asia/Shanghai 显示；“到期当天”若按日期设置，转换为当地当天结束时刻。
归还、分配预约、更新副本状态必须在同一事务中完成；需要行锁或等价并发控制。
预约状态建议 waiting → ready → fulfilled，另有 cancelled/expired。
开发时补充建表脚本和匿名样例数据，不提交真实个人信息。
