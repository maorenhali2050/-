# 测试开发入口
当前没有可执行业务测试，因为后端尚未实现。
后续优先添加：
- borrowing：副本并发借出、重复归还、权限越权。
- overdue-reminder：到期边界、已归还过滤、同日提醒幂等。
- circulation：FIFO、取消、超时、重复分配、预约读者身份验证。
- recommendation：有/无历史、库存不足、当前借阅排除、数量上限。
业务验收参考 docs/modules.md；端到端流程参考 docs/development-plan.md。
