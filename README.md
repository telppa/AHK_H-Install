# AHK_H-Install  
AHK_H One-step installation package.  
AHK H版的1步安装包。  
  
### 什么是H版：  
Lexikos  维护的 AutoHotkey 版本一般称为主版或L版，也就是我们平时在官网上下载的版本。  
HotKeyIt 维护的 AutoHotkey 版本一般称为H版，只能在 Github 或官网论坛上下载。  
  
### 为什么要用H版：  
H版保持了99%以上对主版的兼容性，同时额外提供了包括但不限于以下功能。  
* 多线程  
* 加解密  
* 结构体  
* 进程注入  
* 压缩解压  
* 机器码运行  
* GUI 控件自动缩放  
* 等等...  
  
简单说就是，不改代码的情况下，主版能做的事情，H版都行，但H版能做的事情，主版就未必了。  
  
### H版下载地址：  
https://github.com/HotKeyIt/ahkdll-v1-release/archive/master.zip  
  
从上述地址下载的H版原版压缩包安装较为复杂，需要进行文件替换与修改等操作后，才能正常运行。  
有鉴于此，我制作了 “H版1步安装包” 方便使用。  
  
### “H版1步安装包” 下载地址：  
https://github.com/telppa/AHK_H-Install/archive/refs/heads/main.zip  
  
下载后双击里面的 “安装H版.ahk” 即可。  
  
### 如何恢复为主版：  
重装一遍主版即可。  
  
### 关于调试：  
目前确定 SciTE4AHK增强版 即 [SciTE4AutoHotkey-Plus](https://github.com/telppa/SciTE4AutoHotkey-Plus) 可调试H版。  
其它编辑器不确定，通常可能并不支持，需要自己尝试。  
  
### 关于编译：  
主版编译只能使用 .bin 文件。  
H版编译可以使用 .exe 或 .bin 文件。  
使用 .bin 编译时，会自动在同目录下的 .exe 中查找使用了的库文件，并自动添加到代码中。  
使用 .exe 编译时，可能不需要这一步，因为多数库文件都已经打包到 exe 的 Lib 数据中了。  
所以 .bin 文件编译出的 exe 可能会比 .exe 编译出的小 100kb 左右。  
另外，某些特殊的编译参数必须使用对方提供的 .bin 文件才行。  
我已修改 Ahk2Exe.ahk 代码屏蔽 Compiler 目录及其上级目录下的 .bin .exe .dll 识别。  
A32 U32 U64 3个目录及 Compiler 目录下的 AutoHotkeyA.exe 和 AutoHotkeyU.exe 都是必须的。  
  
-------------  
  
## 以下是对原版压缩包的一些说明  
  
### 安装方式：  
下载压缩包后解压，手动复制其中部分文件替换掉 “已经安装好的主版” 里的对应文件。  
  
### 文件夹怎么这么多：  
文件夹 | 说明 | 备注  
------------- | ------------- | -------------  
x64w_MT | Unicode x64 | MT编译  
x64w | Unicode x64 | MD编译  
Win32w_MT | Unicode x32 | MT编译  
Win32w | Unicode x32 | MD编译  
Win32a_MT | Ansi x32 | MT编译  
Win32a | Ansi x32 | MD编译  
lib | 库文件合集 | 实际上H版很多功能都是用 ahk 代码实现的，例如 CryptAES 。  
Compiler | 编译器 | 注意，编译器目录下的 DynaRun.ahk 文件必须改为 UTF-8带BOM 的编码格式，否则编译器运行会报错。  
  
### 文件怎么也这么多：  
文件 | 说明 | 备注  
------------- | ------------- | -------------  
AutoHotkey.dll | dll 版 ahk  | 一般用于进程注入或在其它语言例如 C++ 里使用 ahk ，没这方面需求的话则可以删掉。  
AutoHotkeyMini.dll | 精简的 dll 版 ahk | 精简掉了界面、热键等多种功能。内存占用更少，加载更快，更适合多线程。  
AutoHotkeySC.bin | 编译可能用到 | 这是用来替换主版 Compiler 目录下对应文件用的。  
AutoHotkey.exe | 编译可能用到 | 这是用来替换主版 AutoHotkey（U64、U32、A32）.exe 用的。  
  
### MT编译和MD编译的区别：  
这个帖子里有作者自己的解释。 https://www.autohotkey.com/boards/viewtopic.php?f=67&t=64573  
简单说就是， MT 版本将 vcruntime140.dll 编译到 exe 里面了，好处是给别人用你编译好的 .ahk 时，可以不用额外附带这个 dll 。  
坏处是， MT 版本在多线程中操作其它线程的内存可能会出错或泄漏。  
所以最好的方式还是用 MD 版本，同时将 vcruntime140.dll 放到 AutoHotkey.exe 同目录下。  
另外，如果电脑上安装了 Microsoft Visual C++ Redistributable 2015 2017 2019 的话， MD 版本也可以不带这个 dll 。  
  
### AutoHotkeyMini.dll 具体精简掉了哪些功能：  
由于作者现在已经不再具体说明移除了哪些功能，所以只能根据早期说明推测，以下功能大概率是被移除了的。  
* Hotkey (以及热键和热字串功能)  
* Gui...  
* GuiControl  
* GuiControlGet  
* Menu...  
* TrayIcon  
* FileInstall  
* ListVars  
* ListLines  
* ListHotkeys  
* KeyHistory  
* SplashImage  
* SplashText...  
* Progress  
* PixelSearch  
* PixelGetColor  
* InputBox  
* FileSelectFile  
* FileSelectFolder  
* Input  
* BlockInput  
* MouseMove  
* 与热键和图标及 Gui 相关的内置变量, A_ThisHotkey, A_IsSuspended, A_Icon...  
  
### 相对于早期版本的一些变化：  
目前的H版，已将以下内容打包到 exe 里面，存于 RC 数据中。  
文件 | RC 数据名  
------------- | -------------  
AutoHotkey.dll | F903E44B8A904483A1732BA84EA6191F  
AutoHotkeyMini.dll | FC2328B39C194A4788051A3B01B1E7D5  
7z.dll | 556EA2A65AE54D58BC52C792B3ED2ED0  
用于 WinApiDef 函数的某种资源 | C974C3B7677A402D93B047DA402587C7  
  
同时，打包了部分 ahk 写的库文件到 exe 里面，存于 Lib 数据中。  
这样做的好处是，平时看不到一堆 dll 和库文件，非常清爽。  
同时实现一些功能变得非常容易，例如多线程，不需要自己加载 dll，自己加载库文件，只需要一条命令即可。  
坏处是，以前萝卜和虚荣翻译的H版帮助，部分内容过时了。所以务必看最新的英文H版帮助或至少中英文H版帮助对照着看！  
  
-------------  