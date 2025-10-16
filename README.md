# ZQ-Track - 订阅管理与提醒系统

基于Cloudflare Workers的轻量级订阅管理系统，帮助您轻松跟踪各类订阅服务的到期时间，并通过 Telegram、Webhook 等多渠道发送及时提醒。

## ✨ 功能特色

### 🎯 核心功能
- **订阅管理**：添加、编辑、删除各类订阅服务
- **智能提醒**：自定义提前提醒天数，自动续订计算
- **农历显示**：支持农历日期显示，可控制开关
- **状态管理**：订阅启用/停用，过期状态自动识别

### 📱 多渠道通知
- **Telegram**：支持 Telegram Bot 通知
- **NotifyX**：集成 NotifyX 推送服务
- **Webhook 通知**：支持自定义 Webhook 推送
- **企业微信机器人**：支持企业微信群机器人通知
- **邮件通知**：基于 Resend 的专业邮件服务
- **Bark**：支持 iOS Bark 推送
- **自定义 Webhook**：支持自定义请求格式和模板

### 🌙 农历功能
- **农历转换**：支持 1900-2100 年农历转换
- **智能显示**：列表和编辑页面可控制农历显示
- **通知集成**：通知消息中可包含农历信息

### 🎨 用户体验
- **响应式设计**：完美适配桌面端和移动端
- **备注优化**：长备注自动截断，悬停显示完整内容
- **实时预览**：日期选择时实时显示对应农历
- **用户偏好**：记住用户的显示偏好设置



## 🚀 手动部署指南

### 前提条件

- Cloudflare账户
- Telegram Bot (用于发送通知)
- 可以直接将代码丢给AI,帮助查漏补缺

### 部署步骤

1.登陆cloudflare,创建worker,粘贴本项目中的js代码,点击部署



2.创建KV键值 **SUBSCRIPTIONS_KV**



3.给worker绑定上键值对,以及设置定时执行时间!



4.打开worker提供的域名地址,输入默认账号密码: admin  password (或者admin admin123),可以在代码中查看默认账号密码!


5.前往系统配置,修改账号密码,以及配置tg通知的信息



6.配置完成可以点击测试通知,查看是否能够正常通知,然后就可以正常添加订阅使用了!
## 🔧 通知渠道配置

### Telegram
- **Bot Token**: 从 [@BotFather](https://t.me/BotFather) 获取
- **Chat ID**: 从 [@userinfobot](https://t.me/userinfobot) 获取

### NotifyX
- **API Key**: 从 [NotifyX官网](https://www.notifyx.cn/) 获取

### 企业微信机器人
- **推送 URL**: 参考[官方文档](https://developer.work.weixin.qq.com/document/path/91770)获取

### Webhook 通知
- **推送 URL**: 根据所使用的 Webhook 服务或自建接口填写，例如 `https://your-service.com/hooks/notify`
- 支持自定义请求方法、请求头与消息模板
- **模板占位符**：`{{title}}`、`{{content}}`、`{{tags}}`（多行形式）、`{{tagsLine}}`、`{{timestamp}}`、`{{formattedMessage}}`

### Bark（iOS 推送）
- **服务器地址**：默认 `https://api.day.app`，也可使用自建服务器
- **设备 Key**：在 Bark App 内复制
- **历史记录**：勾选“保存推送”后可保留推送历史

### 邮件通知 (Resend)
- **API Key**: 从 [Resend 官方教程](https://developers.cloudflare.com/workers/tutorials/send-emails-with-resend/) 获取
- **发件人邮箱**: 必须是已在 Resend 验证的域名邮箱
- **收件人邮箱**: 接收通知的邮箱地址
- 支持 HTML 格式的美观邮件模板

### 🔔 通知时间与时区说明
- Cloudflare Workers 的 Cron 表达式使用 **UTC 时区**，例如 `0 8 * * *` 表示 UTC 08:00 触发
- 若希望在北京时间（UTC+8）早上 8 点提醒，可将 Cron 设置为 `0 0 * * *`
- 若需要小时级提醒，可将 Cron 调整为 `0 * * * *`（每小时执行一次），并在系统配置中指定允许的通知小时
- 系统配置中的 “系统时区” 用于计算订阅剩余时间和格式化展示，建议与提醒需求保持一致

### 🔐 第三方 API 安全调用
- 通过 `POST /api/notify/{token}` 可触发系统通知，请在后台配置“第三方 API 访问令牌”
- 令牌也可通过 `Authorization: Bearer <token>` 或 `?token=<token>` 传入
- 未配置或令牌不匹配时接口会直接拒绝请求，建议定期更换随机令牌


> 💡 **提示**: 系统默认每天早上8点自动检查即将到期的订阅



## 🤝 贡献

欢迎贡献代码、报告问题或提出新功能建议!

MIT Lic
