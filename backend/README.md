# 后端开发入口
技术栈尚未锁定，先按学校要求或已掌握的语言选择一种。建议保持单体应用，避免微服务。
- src/modules/catalog/：图书及副本查询、管理员维护。
- src/modules/borrowing/：借出、归还、库存状态；这是后续模块的数据基础。
- src/modules/recommendation/：只读借阅历史，返回推荐及理由。
- src/modules/overdue-reminder/：扫描未归还记录，创建去重站内消息。
- src/modules/circulation/：预约队列、归还分配、领取超时。
- src/jobs/：每日逾期扫描、预约保留到期扫描。
登录和读者/管理员权限需在接入真实数据前实现；读者身份从服务端会话取得，不能信任请求中的 user_id。
