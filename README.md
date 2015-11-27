# 好屌的脚本

Based on a _[true
story](https://www.jitbit.com/alexblog/249-now-thats-what-i-call-a-hacker/)_:



# 超过 90 秒的任务不自动化，你好意思说自己是黑客？

Based on a _[true
story](https://www.jitbit.com/alexblog/249-now-thats-what-i-call-a-hacker/)_:

> 某某某：好吧，我们的集成工程师已经跳槽到另一家公司了。那个哥们简直就是生活在终端里面。你懂的，他就是那种喜欢 Vim、用 Dot 创建图表和用 Markdown 编写 wiki 帖子等等的家伙（译者注：Dot，一种图形描述语言）。如果某些事情，甚至可以说是任何事情，哪怕只需要花费他超过 90 秒的时间，那他会写一个脚本，来自动处理那些事情。

> 某某某：嗯……所以我们坐在这里，翻翻着他的“遗产”。

> 某某某：你会喜欢这个的。

> xxx: [`smack-my-bitch-up.sh`](https://github.com/NARKOZ/hacker-scripts/blob/master/smack-my-bitch-up.sh) -
给他老婆发一条的短信，大概意思是“晚上要加班”。从一个字符串数组中自动随机地提取理由。运行在一个定时任务里面。如果晚上 9 点之后，服务器上还有他登录的有效 SSH 会话，那就会触发这个定时任务。

> xxx: [`kumar-asshole.sh`](https://github.com/NARKOZ/hacker-scripts/blob/master/kumar-asshole.sh) - 
从电子邮件的收件箱里扫描“Kumar”（他是我们一个客户的数据库管理员）。查找像“help”、“trouble”、“sorry”等这样的关键字。如果找到了，那么脚本会 SSH 连接登录到客户服务器，并且将数据库回滚到最新的备份。然后发送一条回复：“别担心，兄弟。下次小心点。”

> xxx: [`hangover.sh`](https://github.com/NARKOZ/hacker-scripts/blob/master/hangover.sh) -
另一个定时任务被设置成特定的时间。自动发送类似“感觉不舒服、要在家里工作”这样的电子邮件。从另一个定义好的字符串数组中，选取一个随机的“理由”。如果在早上 8:45 前，服务器上没有交互的 session，就会触发该定时任务。

> xxx: (and the oscar goes to) [`fucking-coffee.sh`](https://github.com/NARKOZ/hacker-scripts/blob/master/fucking-coffee.sh) - 
这个脚本会等待整整 17 秒（！），然后打开一个 SSH 会话，连接我们的咖啡机（我们完全没有想到咖啡机会连网、上面运行着 Linux、 后台还执行着 SSHD），接着给它发送一些稀奇古怪的命令。这看起来很有极客范。完成这些之后，咖啡机会开始煮一杯中号的 half-caf 拿铁咖啡，再等待 24 秒（！）就可以把咖啡倒入杯中。这个时间恰恰是那家伙从他的座位上走到咖啡机所用的时间。

> 某某某：这太 TM 牛 X 了，我要留着这些。


Original: http://bash.im/quote/436725 (in Russian)  
Pull requests with other implementations (Python, Perl, Shell, etc) are welcome.

## Usage

You need these environment variables:

```sh
# used in `smack-my-bitch-up` and `hangover` scripts
TWILIO_ACCOUNT_SID=ACxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
TWILIO_AUTH_TOKEN=yyyyyyyyyyyyyyyyyyyyyyyyyyyyyyy

# used in `kumar_asshole` script
GMAIL_USERNAME=admin@example.org
GMAIL_PASSWORD=password
```

For Ruby scripts you need to install gems:
`gem install dotenv twilio-ruby gmail`

## Cron jobs

```sh
# Runs `smack-my-bitch-up.sh` monday to friday at 9:20 pm.
20 21 * * 1-5 /path/to/scripts/smack-my-bitch-up.sh >> /path/to/smack-my-bitch-up.log 2>&1

# Runs `hangover.sh` monday to friday at 8:45 am.
45 8 * * 1-5 /path/to/scripts/hangover.sh >> /path/to/hangover.log 2>&1

# Runs `kumar-asshole.sh` every 10 minutes.
*/10 * * * * /path/to/scripts/kumar-asshole.sh

# Runs `fucking-coffee.sh` hourly from 9am to 6pm on weekdays.
0 9-18 * * 1-5 /path/to/scripts/fucking-coffee.sh
```

---
Code is released under WTFPL.
