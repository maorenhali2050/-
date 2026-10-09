# API 草案（所有接口尚未实现）
统一前缀 /api；JSON 响应；列表分页；错误返回 code/message，服务端校验权限和状态。
| 方法与路径 | 用途 | 权限 |
| --- | --- | --- |
| POST /auth/login | 登录建立会话 | 匿名 |
| POST /auth/logout | 退出会话 | 已登录 |
| GET /books | 搜索、分类查询 | 读者/管理员 |
| POST /books | 维护书目 | 管理员 |
| POST /loans | 确认借出，传读者及副本 ID | 管理员 |
| POST /loans/{id}/return | 归还并触发预约分配 | 管理员 |
| GET /me/loans | 当前用户借阅与逾期状态 | 读者 |
| GET /me/recommendations | 推荐列表与理由 | 读者 |
| GET /me/notifications | 站内消息 | 读者 |
| PATCH /me/notifications/{id} | 标为已读，仅本人 | 读者 |
| POST /reservations | 为本人预约 book_id | 读者 |
| GET /me/reservations | 本人预约及排队状态 | 读者 |
| DELETE /reservations/{id} | 取消本人有效预约 | 读者 |
| GET /admin/overdue-loans | 逾期借阅列表 | 管理员 |
| GET /admin/reservations | 等待和待领取预约 | 管理员 |
| POST /reservations/{id}/checkout | 确认队首领取并借出 | 管理员 |

预约领取不与普通借出混用：必须验证预约读者、保留副本和保留时限。
建议状态码：400 参数错误，401 未登录，403 权限不足，404 不存在，409 库存或状态冲突。
定时任务是内部服务，不开放匿名“扫描”接口。
