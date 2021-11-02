<p align="center">
    <h1 align="center">掘金每日自动签到与抽奖</h1>
</p>

<p align="center">
    每天定时自动签到获得矿石数
    <br />
    <br />
    <a href="https://github.com/sudojia/juejin-auto-sign/issues/new">上报Bug</a>
  </p>

- [✏️写在前面](#%EF%B8%8F写在前面)
- [💍介绍](#介绍)
- [😍特点](#特点)
- [🔑*Env*](#env)
- [⚠️特别声明](#特别声明)
- [🔛使用](#使用)
- [🎯TODO](#todo)
- [🕛历程](#历程)

## ✏️写在前面

很久没逛掘金了，昨晚逛的时候偶然发现了一个签到的功能，所以就学习了一下，就有了这个项目~😁

**目前 GitHub Actions 代码还是有问题**，有时间我再研究一下，本地亲测可以直接 `node index.js` （需安装 nodejs）

## 💍介绍

每天定时自动签到 [掘金社区](https://juejin.cn/) 从而获得矿石数，矿石数可进行**抽奖**、**实物兑换**，支持多用户、以及多个消息平台（Telegram、server 酱、Bark、PushPlus、钉钉等）服务推送。

项目会在每天早上的北京时间八点三十五分运行，Actions 会有延迟的，几分钟甚至半小时！

## 😍特点

- ~~💰~~ 免费（项目运行在 GitHub Actions 上.）
- 📯 多账号
- 📧 多个消息推送平台
- ...

## 🔑*Env*

### 主变量（必须）

`Settings - Secrets - New repository secret`

|      Name       |     Value     |                             说明                             | 属性 |
| :-------------: | :-----------: | :----------------------------------------------------------: | ---- |
| `JUEJIN_COOKIE` | 掘金的 Cookie | 打开[掘金](https://juejin.cn/)，F12 Network，随便找一个 `XHR` 的请求获取 Cookie<br>下面有详细说明 | 必须 |

不需要复制全部，只需要  `sessionid=xxx`  即可

多个填写规则：`sessionid=xxxxxx&sessionid=bbbbbb&sessionid=以此类推`  用 & 分割

![getCookie](https://cdn.jsdelivr.net/gh/sudojia/juejin-auto-checkin/img/getCookie.jpg)

### 消息推送变量（可选）

|       Name        |                             归属                             |  属性  |                             说明                             |
| :---------------: | :----------------------------------------------------------: | :----: | :----------------------------------------------------------: |
|    `PUSH_KEY`     |                      微信 server 酱推送                      | 非必须 | server 酱的微信通知[官方文档](http://sc.ftqq.com/3.version)，已兼容 [Server 酱·Turbo 版](https://sct.ftqq.com/) |
|    `BARK_PUSH`    | [BARK 推送](https://apps.apple.com/us/app/bark-customed-notifications/id1403753865) | 非必须 | IOS 用户下载 BARK 这个 APP，填写内容是 app 提供的`设备码`<br>例如：https://api.day.app/123 ，那么此处的设备码就是 `123` |
|   `BARK_SOUND`    | [BARK 推送](https://apps.apple.com/us/app/bark-customed-notifications/id1403753865) | 非必须 | bark 推送声音设置，例如 `choo`，具体值请在 `bark`-`推送铃声`-`查看所有铃声` |
|  `TG_BOT_TOKEN`   |                        Telegram 推送                         | 非必须 | `TG_BOT_TOKEN` 和 `TG_USER_ID` 两者必需<br>填写自己申请 [@BotFather](https://t.me/BotFather)的 Token<br>如 `10xxx4:AAFcqxxxxgER5uw` |
|   `TG_USER_ID`    |                        Telegram 推送                         | 非必须 | `TG_BOT_TOKEN` 和 `TG_USER_ID` 两者必需<br/>私聊它 [@userinfobot](https://t.me/userinfobot) 随便发点什么即可获取到自己的 ID |
|  `DD_BOT_TOKEN`   |                           钉钉推送                           | 非必须 | (`DD_BOT_TOKEN` 和 `DD_BOT_SECRET` 两者必需)[官方文档](https://developers.dingtalk.com/document/app/custom-robot-access) <br>只需 `https://oapi.dingtalk.com/robot/send?access_token=XXX` 等于 `=` 符号后面的 XXX 即可 |
|  `DD_BOT_SECRET`  |                           钉钉推送                           | 非必须 | (`DD_BOT_TOKEN` 和 `DD_BOT_SECRET` 两者必需) ，密钥，机器人安全设置页面，加签一栏下面显示的 SEC 开头的 `SECXXXXXXXXXX` 等字符，注：钉钉机器人安全设置只需勾选`加签`即可，其他选项不要勾选 |
|    `QYWX_KEY`     |                      企业微信机器人推送                      | 非必须 | 密钥，企业微信推送 webhook 后面的 key [详见官方说明文档](https://work.weixin.qq.com/api/doc/90000/90136/91770) |
|  `IGOT_PUSH_KEY`  |                          iGot 推送                           | 非必须 | iGot 聚合推送，支持多方式推送，确保消息可达。 [参考文档](https://wahao.github.io/Bark-MP-helper ) |
| `PUSH_PLUS_TOKEN` |                        pushplus 推送                         | 非必须 | 微信扫码登录后一对一推送或一对多推送下面的 token(您的 Token)<br>[官方网站](http://www.pushplus.plus/) |
| `PUSH_PLUS_USER`  |                        pushplus 推送                         | 非必须 | 一对多推送的 “群组编码”（一对多推送下面 -> 您的群组(如无则新建)->群组编码）<br>注：(1、需订阅者扫描二维码  2、如果您是创建群组所属人，也需点击“查看二维码”扫描绑定，否则不能接受群组消息推送)<br>只填 `PUSH_PLUS_TOKEN` 默认为一对一推送 |

## ⚠️特别声明

- 该项目仅用于我学习 JavaScript 以及接口调用，禁止用于商业用途，不能保证其合法性，准确性，完整性和有效性，请根据情况自行判断。
- 该项目内所有资源文件，禁止任何公众号、自媒体进行任何形式的转载、发布。
- sudojia 对除该项目问题概不负责，包括但不限于由该项目错误导致的任何损失或损害。
- 使用该项目的任何用户，包括但不限于在某些行为违反国家/地区法律或相关法规的情况下进行传播，sudojia 对于由此引起的任何隐私泄漏或其他后果概不负责。
- 请勿将该项目的任何内容用于商业或非法目的，否则后果自负。
- 如果任何单位或个人认为该项目可能涉嫌侵犯其权利，则应及时通知并提供身份证明，所有权证明，我将在收到认证文件后删除该项目。
- 任何以任何方式查看此项目的人或直接或间接使用该项目的使用者都应仔细阅读此声明。sudojia 保留随时更改或补充此免责声明的权利。一旦使用并复制了任何相关脚本或该项目的规则，则视为您已接受此免责声明！

**您必须在下载后的24小时内从计算机或手机中完全删除以上内容。**

**您使用或者复制了本仓库且本人制作的任何脚本，则视为`已接受`此声明，请仔细阅读。**

## 🔛使用

1. 右上角 Fork 该项目

2. 在 Fork 后的仓库中  `Settings - Secrets - New repository secret`  添加变量，变量说明请看  [🔑Env](#env)

3. 点击仓库中的 Actions，如图所示

   ![image](https://cdn.jsdelivr.net/gh/sudojia/sspanel_checkin/img/20210927171440.jpg)

4. 看图

   ![image](https://cdn.jsdelivr.net/gh/sudojia/sspanel_checkin/img/20210927171527.jpg)

5. 继续看图

   ![image](https://cdn.jsdelivr.net/gh/sudojia/sspanel_checkin/img/20210927171547.jpg)

6. 稍等片刻就执行好了，如果报错，不妨可以提个 [issues](https://github.com/sudojia/sspanel_checkin/issues/new)，不要害羞！

## 🎯TODO

- [ ] 一键梭哈
- [ ] ...

## 🕛历程

- 2021-11-01 22:35 - 已完成自动签到、抽奖以及多个掘金账号！