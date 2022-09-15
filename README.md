# ![Logo](chrome/app/theme/chromium/product_logo_64.png) Chromium

Chromium is an open-source browser project that aims to build a safer, faster,
and more stable way for all users to experience the web.

The project's web site is https://www.chromium.org.

To check out the source code locally, don't use `git clone`! Instead,
follow [the instructions on how to get the code](docs/get_the_code.md).

Documentation in the source is rooted in [docs/README.md](docs/README.md).

Learn how to [Get Around the Chromium Source Code Directory Structure
](https://www.chromium.org/developers/how-tos/getting-around-the-chrome-source-code).

For historical reasons, there are some small top level directories. Now the
guidance is that new top level directories are for product (e.g. Chrome,
Android WebView, Ash). Even if these products have multiple executables, the
code should be in subdirectories of the product.

If you found a bug, please file it at https://crbug.com/new.

## 主要目录

android_webview，Android WebView 实现，封装 Content 层以集成进 Android 平台。android 重要的支持。
base，通用代码，基础组件，包含字符串、文件、线程、消息队列等工具类集合。
cc，Chromium compositor 的缩写，负责渲染合成。
chrome，Chromium 浏览器实现。
components，提供最顶层（Android WebView 或 Chrome）选配使用的 Content 组件。
content，多进程沙盒浏览器的核心代码，管理进程架构和线程架构。
gin，V8 的轻量绑定系统。
gpu，OpenGL 封装代码，包含 CommandBuffer 和 OpenGL 兼容性支持等。
net，网络栈实现。
ipc，进程间消息通信实现。
media，多媒体封装代码，包含了媒体内容捕获和播放的组件集合。
mojo，类似于 Android 的 AIDL，提供了跨语言（C++ / Java / JavaScript）跨平台的进程间对象（Object）通信机制；对比 ipc ，后者提供的是单语言（C++）的进程间消息（Message）通信机制。这是chromium最新设计的IPC架构，会逐渐替换掉老的IPC。
out，编译时创建的目录，用于存放生成产物。
skia，Android skia 图形库，这里存放的是 Chromium 对 skia 的 配置和扩展代码，另有 third_party/skia 目录存放原生的 skia 代码。
third_party/WebKit，网页排版引擎。third_party下还有其他很多组件如webrtc,tcmalloc
ui，UI 框架。
url，GURL，Google 的开源 URL 解析和规范化库。
v8，V8 JavaScript 引擎库。

## 其他一级目录

apps，Chrome Apps 框架。
ash，Aura Shell 的缩写，实现 Chrome OS 的窗口管理和系统 UI。
blink，LayoutTests 脚本。
breakpad，开源的多平台异常上报系统。
build，编译脚本和配置文件。
build_overrides，用于不同的产品自定义设置选项。
buildtools，编译工具。
chromecast，Google 的一款数字电视棒，运行精简的 Chrome OS 操作系统。
chrome_elf，Chrome Early Loading Framework 的缩写，Chrome 浏览器启动早期执行代码的框架。
chromeos，Google 开发的基于 PC 的操作系统.
cloud_print，Google 云打印。
courgette，增量升级系统。
crypto，加密算法。
dbus，进程间通信及远程过程调用机制。
device，外接设备封装代码。
docs，项目文档。
extensions，Chrome Extensions 框架。
google_apis，Google API 封装代码。
google_update，存放生成 Windows 下 Google Update 的 IDL 的文件。
headless，用于服务器环境下运行 Chromium 。
infra，Chromium 开发用到的服务器和工具等基础设施相关的脚本。
ios，Chrome for iOS 相关代码。
jingle，P2P 通信库，这里存放的是 Chromium 对 libjingle 的胶水层代码，另有 third_party/libjingle_xmpp 目录存放原生的 libjingle 代码。
mash，mus + ash，mus 是 mojo UI service 的缩写。
native_client，缩写为 NaCl，Chrome Native 插件框架。
native_client_sdk，Nacl 的 sdk。
pdf，PDF 插件代码。
ppapi，在沙盒中运行插件的框架。
printing，打印。
remoting，Chrome 远程桌面。
rlz，Google 用来追踪产品市场推广活动以及分发活动效果的一个组件。
sandbox，沙盒机制。
sdch，网络模块 SDCH 压缩算法的配置目录，另有 net/sdch 目录存放 SDCH 算法的实际代码。
services，Chrome Foundation Services，如果将 Chrome 理解成一个轻量的 OS，该目录就是提供基础的系统服务的层。
sql，SQLite 封装代码。
storage，Chrome’s Blob Storage 系统。
styleguide，代码风格指引。
testing，测试框架。
third_party，第三方库。
tools，工具。

## content

app，进程入口和启动时的基本逻辑。
browser，运行在主进程，负责处理 I/O 消息以及与子进程通信。
child，运行在子进程的通用逻辑。
common，多进程共享的数据类型。
gpu，运行在 GPU 进程，CommandBuffer 的服务端，负责实际执行 GL 命令。
ppapi_plugin，运行在插件进程的逻辑。
public，定义和导出抽象接口给上一层（Android WebView 或 Chrome）访问。
renderer，运行在 Renderer 进程，嵌入 WebKit。
shell，Content Shell 实现。
test，测试代码。
utility，运行在 Utility 进程，操作不信任数据。

## android_webview

apk，Android WebView Apk 的资源和代码文件。
browser，Content 模块主进程封装、回调以及扩展代码
common，Browser 端与 Renderer 端共享的数据类型。
glue，Android WebView 系统接口的胶水层实现代码。
gpu，Content 模块 GPU 进程封装、回调以及扩展代码。
java，Android WebView 调用 Chromium 代码的顶级入口，封装 Content 层代码。
javatests，Java 类的单元测试代码。
lib，so 入口以及启动时的扩展逻辑。
public，定义和导出抽象的 Native 接口给 Android WebView 的渲染管线使用。
renderer，Content 模块 Renderer 进程封装、回调以及扩展代码。
test，Android WebView 的测试代码
ui，字符串和 UI 资源。