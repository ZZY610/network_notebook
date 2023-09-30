# Clash操作指南
## 简介
### 代理
代理是指一种在网络上的中间人，充当客户端和目标服务器之间的中转站，可以帮助用户通过它自己的IP地址来访问其他网站或服务。

代理软件是一种可以提供代理服务的应用程序，它可以通过在计算机、服务器或路由器上运行，来实现代理功能。代理软件可以用于掩盖用户真实的IP地址，以便在匿名访问互联网和保护个人隐私时使用。除了匿名访问外，代理软件还可以通过缓存、过滤和监控网络流量等功能提高网络访问速度和安全性。常见的代理软件包括Clash、Squid、Nginx等。

### Clash
Clash是一种支持多协议和多路由的 **代理软件** ，其基本的工作原理是通过代理服务器连接互联网，使用规则集来对网络流量进行控制和过滤，从而实现科学上网。

使用Clash进行翻墙时，系统自动选择了代理服务器的设置，地址为127.0.0.1（即本地回环地址），端口为7890。所有的网络请求都会被重定向到本机的7890端口。Clash本地代理客户端会监听这个端口，并根据配置的规则对这些请求进行处理，进而实现代理、转发或直接连接目标服务器。

## UI说明
### General 常规
在常规页面下可以清楚了解当前配置文件的设置，譬如常规的 http 和 socks5 代理端口等，方便对某些应用单独进行配置代理。部分含删除线功能说明在新版本后弃用。

#### 选项说明

- **Port**：Mixed(Http+Socks) 代理端口
- Allow LAN：是否允许局域网代理
  - 网络图标：显示网卡信息
- Log Level：Clash 核心日志等级
- IPV6: 是否启用 IPV6
- Home Directory：Clash 配置文件目录（不建议修改此目录下文件内容）
- GeoIP Database：GeoIP 数据库更新
- UWP Loopback：UWP 应用联网限制解除工具
- Service Mode: 虚拟网卡安装(TUN 模式)
  - 地球图标：显示 Service Mode 在线状态
- TUN Mode: 是否启用 TUN 模式
  - 设置图标：打开 TUN 模式设置面板
- TAP Device：虚拟网卡安装(TAP 模式)
- Mixin: 是否启用 Mixin 模式
  - 设置图标：启动编辑器修改 Mixin 配置
- System Proxy：系统代理开关
- Start with Windows/macOS/Linux：开机自启动开关

#### 点击行为

- Clash for Windows（标题）：快速重启软件
- v x.x.x: 当显示`new`提示时可以直接点击下载新版安装包 (每隔 6 小时检查一次更新)
- Connected/Disconnected：文件夹中显示当前日志文件

#### 右侧对应点击行为

- Port:
  - 终端图标: 使用命令行设置系统代理
  - 循环图标: 随机设置 Mixed 端口
  - 端口号：修改 Mixed Port
- Log Level: 设置日志类型
- IPv6：设置是否启用 IPv6 连接逻辑
- Clash Core
  - 盾牌图标: 添加 Allow LAN 与 System Stack 的防火墙规则
  - 内核版本号: 打开 Clash 内核控制 Web 页面
- UWP Loopback：快速打开回环代理限制器
- Home Directory：快速打开配置文件目录
- GeoIP Database：点击更新 GeoIP 库 （macOS 可用）
- TAP Device：打开 TAP 模式虚拟网卡控制面板（Windows 可用）

### Proxies 代理

代理页面主要的作用就是**切换代理模式**和**切换节点**

#### 切换代理模式

Clash 共有三种工作模式：

- 全局（Global）：所有请求直接发往**代理服务器**
- 规则（Rule）：所有请求**根据配置文件规则进行分流**
- 直连（Direct）：所有请求**直接发往目的地**

切换不同模式时，对应的节点列表会对应变化

#### 切换节点

::: tip
延迟测试(网络图标)可测试所有节点的延迟，可在Settings→Latency Test URL修改测试URL
:::

节点按照策略组分开，并可以以组为单位进行延迟测试，可以方便选出延迟更低的节点。或者可以使用策略组优化逻辑，策略组原理请参考：[策略组原理理解](https://github.com/Fndroid/jsbox_script/wiki/%E5%85%B3%E4%BA%8E%E7%AD%96%E7%95%A5%E7%BB%84%E7%9A%84%E7%90%86%E8%A7%A3)

### Profiles 配置

::: tip
深颜色表示当前配置文件已被载入成功

远程配置文件指通过 URL 导入的配置文件
:::

每个配置文件都包括如下信息：

- 名称
- 类型（远程显示域名，本地显示 local）
- 上次更新时间
- 操作栏

操作栏分别可以进行如下操作：

- Edit: 使用内置编辑器进行文本编辑
- Edit externally: 使用外部编辑器进行文本编辑
- Update: 刷新配置文件(仅限远程配置文件)
- Show in folder: 在系统文件夹显示配置文件
- Diff: 创建diff文件进行编辑以合并到原配置文件
- Proxies: 编辑链接策略
- Rules: 编辑链接规则
- Copy: 复制配置文件
- QRCode: 生成当前配置文件QR码(仅限远程配置文件)
- Settings: 编辑当前配置文件相关
- Delete: 删除当前配置文件

### Logs 日志

此界面能直观地观察当前命中的规则以及所使用的策略类型及路由，以及设置记录日志的类型

- mode: 代理模式
- Search：过滤日志
- Info/Debug: 日志等级（仅面板，不影响日志文件生成）
- Clear: 清除全部日志
- Stop: 停止记录日志

::: tip
此界面仅在开启时捕获

如需获取所有 log，可以查看配置文件夹下的 logs 文件夹
:::

### Connections 连接

![](~@imgs/ui-connections.png)

在这个页面可以直观的看到当前的所有连接状态，可以一键关闭指定或全部连接

#### 顶栏

- Pause/Resume: 暂停/继续连接统计
- Total: 显示当前上下行流量总量
- Search：搜索指定连接
- 排序按钮(依据):
  - Upload Speed 根据上行速度
  - Download Speed 根据下行速度
  - Upload Traffic 根据上行流量
  - Download Traffic 根据下行流量
  - Time 根据建立连接的时间
- Close All: 关闭全部连接

#### 连接显示区域

- TCP/UDP: 连接协议
- HTTP Connect/HTTP/Socks5/TUN: 连接类型
- 禁止符号: 关闭连接

点击之后可查看更加详细的信息

- Alive/Closed: 连接是否存活
- Host: 连接到的主机
- Network: 连接协议
- Traffic: 此连接上/下行流量
- Source: 连接来源地址
- Destinaion: 连接目的地址（如 Host 已被 DNS 解析则显示对应 IP 地址）
- Rule: 连接命中的规则
- Process Path: 连接发起应用路径（需要经过 PROCESS-NAME 规则触发）
- Chains: 连接策略链
- Start Time: 建立连接的时间

## Settings 设置

#### Reset All Settings

重置 CFW 的全部设置，恢复到默认值

#### Force Quit

强制退出 CFW

#### Quit

正常退出 CFW

### Security

#### Core Secret

设置 Home Directory/config.yaml 中 secret 参数为随机 uuid4，访问核心 API 被网页直接调用

#### Allow unsafe URLs

设置在请求时不验证认证的 URL

### General

#### Settings Editor

设置 Settings 界面使用的编辑器，如需要自定义命令，则需要命令支持中断（类似`subl --wai`）

#### Notifications

设置是否允许弹出系统级通知

#### Silent Start

设置启动后是否显示主界面

#### Random Controller Port

设置是否使用随机端口作为核心控制器端口（Home Directory/config.ymal 中 external-controller 中 port 部分）

#### Random Mixed Port

设置是否使用随机端口作为 General 中 Port 参数（Home Directory/config.ymal 中 mixed-port 参数）

#### Lightweight Mode

[轻量模式](../lightweight.md)

#### Run Time Format

设置主界面左下角运行时间格式

#### GUI Log Folder

设置 GUI 日志文件夹

#### Show New Version Icon

设置是否显示新版本提示标志

#### Automatic Upgrade (macOS)

设置是否自动更新，设置后有新版本将在后台更新，更新完成后下次启动即是最新版本

### Appearance

#### Theme

设置主题颜色

#### Follow System Theme

设置是否根据系统选择 Light / Dark 主题

#### Font Family

设置主界面字体，如字体不存在可能会导致界面显示不全

#### Use System Emoji

设置是否使用系统 Emoji 字体，关则表示使用 CFW 内置 Emoji 字体

#### Default Icon Path (Windows)

设置默认状态下任务栏图标

#### System Proxy On Icon Path (Windows)

设置 System Proxy 开启下任务栏图标

#### Hide Tray Icon

设置是否隐藏任务栏图标

#### Enhanced Tray

设置是否启用自定义任务栏（macOS）/ 悬浮窗（Windows）

将右侧图标拖动至左侧表示显示该元素

[具体参考](../tray.md)

#### Text

设置 Enhanced Tray 的 Script 部分显示为固定文本

#### Script

设置 Enhanced Tray 的 Script 部分显示为 Script 指向 JavaScript 脚本运行返回的内容

#### Script Interval

设置 Enhanced Tray 的 Script 的刷新频率

#### Transparent （Windows）

设置 Enhanced Tray 是否使用透明界面

### System Proxy

#### Type （Windows）

设置系统代理类型

#### PAC Content （Windows）

设置系统代理类型为 PAC 时，对应 PAC 脚本内容。[规范参考此处](https://developer.mozilla.org/en-US/docs/Web/HTTP/Proxy_servers_and_tunneling/Proxy_Auto-Configuration_PAC_file)

#### Bypass Domain/IPNet

设置系统代理绕过域名或 IP 集合

#### Specify Protocol （Windows）

设置是否指定系统代理协议（仅建议在使用 Python 编程遇到网络问题时打开）

#### Static Host

设置系统代理 Host 部分为静态内容，不设置则 host 默认为 127.0.0.1

### Mixin

[具体参考](../mixin.md)

#### Type

设置 Mixin 类型

#### YAML

设置当 Mixin Type 为 YAML 时对应内容

#### JavaScript

设置当 Mixin Type 为 JavaScript 时对应内容

### Proxies

#### Proxy Item Width

设置 Proxies 界面中每个节点显示宽度

#### Mini List Width

设置 Proxies 界面中右侧导航栏展开宽度

#### Order By

设置 Proxies 界面中节点排序依据

可选：

- Default：默认排序
- Latency：延迟排序
- Alphabet：字母表排序

#### Latency Test URL

设置 Proxies 界面中点击延迟测试按钮时使用的 URL

#### Latency Test Timeout

设置 Proxies 界面中点击延迟测试按钮时超时时间

#### Show Filter

设置 Proxies 界面是否显示关键字过滤图标

#### Hide Unselectable Group

设置 Proxies 界面中是否隐藏不可选策略组

### Connections

#### Break When Proxy Change

设置在 Proxies 界面中切换节点时打断 connection 的策略

可选：

- None：不打断
- Chain：连接中包含节点时打断
- All：打断所有连接

#### Break When Profile Change

设置切换 profile 时是否打断所有连接

#### Break When Mode Change

设置切换 mode 时是否打断所有连接

#### Display Chain Type

设置 Connections 界面中显示的 chain 类型

可选：

- Proxy：节点名
- Group：策略组名
- Both：节点名以及策略组名

### Providers

#### Use CFW Editor

设置是否使用内置编辑器打开 provider 文件

### Outbound

#### Interface Name

设置出口网络网卡（如非必要请勿设置，后续版本将去除此功能）

### Child Processes

[具体参考](../childprocess.md)

#### Processes

设置子进程

### Profiles

#### Parsers

设置预处理器内容，[具体参考](../parser.md)

#### Console Output

设置预处理器调用 `console.log`时输出日志文件目录

#### Folder Path

设置 profiles 文件夹路径，默认 Home Directory / profiles

#### Request Headers

设置更新配置文件时请求头内容，如需设置单个配置文件请求头内容，请在 Profiles 界面中操作

#### Select After Updated

设置更新配置文件后是否选中该 profile

### Logs

#### Preload

设置 Logs 界面预加载日志行数，设置为 0 则不预加载

### Actions

[具体参考](../actions.md)

#### Scripts

设置执行 Action 时调用代码

#### Console Output

设置 Actions 代码执行 `console.log`时输出文件路径

### Shortcuts

#### System Proxy

设置 System Proxy 开关快捷键

#### TUN Mode

设置 TUN Mode 开关快捷键

#### Mixin

设置 Mixin 开关快捷键

#### Global Mode

设置将 mode 切换为 Global 快捷键

#### Direct Mode

设置将 mode 切换为 Direct 快捷键

#### Rule Mode

设置将 mode 切换为 Rule 快捷键

#### Script Mode

设置将 mode 切换为 Script 快捷键

#### Show/Hide Dashboard

设置显示/隐藏主界面快捷键

#### Run Tray Script

设置执行 Enhanced Tray 的 Script 代码快捷键

### Cache

#### Fake IP Cache

`Clear`清除 Fake IP 缓存

### Experimental Features（macOS）

#### DHCP Server

[具体参考](../dhcp.md)
