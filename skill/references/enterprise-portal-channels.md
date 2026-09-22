# 企业官网招聘通道矩阵

按「专业对口企业库」（profession-enterprise-map.json）对口企业官网招聘页的可访问性实测结果（2026-09-21 探测）。技能运行时按简历专业板块 → 对口企业清单 → 本表判断官网是否可采集。

## 可用：免登录可浏览（浏览器通道，按需采集）

| 行业 | 企业 | 招聘页 | 数据形态 |
|---|---|---|---|
| 食品 | 蒙牛 | mengniu.zhiye.com（北森italent） | 社招/校招入口；岗位列表 JS 异步加载，需浏览器 |
| 食品 | 农夫山泉 | nongfuspring.com/join/ | SSR 页面 |
| 食品 | 双汇 | shuanghui.net/join/ | 招聘启事公告（非结构化，可提取公司+岗位+城市） |
| 食品 | 良品铺子 | lppz.com/joinus | SSR 页面 |
| 食品 | 康师傅 | masterkong.com.cn/join/ | SSR 页面 |
| 互联网 | 华为 | career.huawei.com | SPA 壳，岗位走接口 |
| 互联网 | 哔哩哔哩 | jobs.bilibili.com | SPA，岗位走接口 |
| 互联网 | 百度 | talent.baidu.com | SPA，岗位走接口 |
| 互联网 | 网易 | hr.163.com | 岗位列表页 |
| 制造 | 海尔 | maker.haier.net | SSR 页面 |
| 制造 | 三一 | sanygroup.com/join/ | 大页面（322KB）含招聘信息 |
| 制造 | 大疆 | we.dji.com/zh-CN/jobs | SPA，岗位走接口 |
| 医疗 | 药明康德 | wuxiapptec.com.cn/careers/ | 大页面（532KB） |
| 教育 | 新东方 | zhaopin.xdf.cn | SSR 页面 |
| 金融 | 招商银行 | career.cmbchina.com | 跳转/小页面 |
| 金融 | 平安 | talent.pingan.com | 跳转/小页面 |

## 需登录/ATS 内部：仅投递页可见（暂不可自动采集）

- 伊利：ehire.51job.com（前程无忧企业版登录墙）
- 蒙牛岗位明细：北森 italent 接口需登录态
- 各银行网申系统（招商/工商等网申需注册账号）

## 不可用：404 / 连接失败 / 无岗位数据

洽洽、携程、比亚迪、宁德时代、格力、美的、中芯国际、恒瑞、迈瑞、好未来、中公、顺丰、万科、中国建筑、小米（607字节空壳）

## 采集方式

1. **优先**：智联/实习僧/腾讯/前程无忧/拉勾 5 主通道（结构化、稳定）；
2. **专业板块补充**：按简历专业从 profession-enterprise-map.json 取对口企业，对照本表「可用」名单，用豆包浏览器逐个访问官网招聘页，`bu.read_all`/文本提取岗位（岗位名称/公司/城市/链接），写入 `browser_jobs.json` 后经采集器 `--browser-file` 合并入库；
3. 官网岗位结构与 5 主通道不同源，天然去重；每个官网可采 10-20 条/次；
4. 登录墙官网（伊利等）不自动采集，用户手动浏览时可将岗位链接发给技能入库。
