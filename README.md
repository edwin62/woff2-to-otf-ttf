# woff2-to-otf-ttf
一、前提条件
系统：macOS
已安装 Python 3：
打开“终端(Terminal)”，输入：
bash
复制代码
python3 --version
若能显示 Python 3.x.x 就说明已装好。若提示“command not found”，需先去 Python 官网 下载并安装。
已安装 pip3：
在终端输入：
bash
复制代码
pip3 --version
如果出现 pip 21.x.x (或类似)，说明 pip3 可用。
如果没有，可执行：
bash
复制代码
python3 -m ensurepip --upgrade
这会自动安装或升级 pip3。
二、安装工具：FontTools + Brotli
WOFF2 解压需要 FontTools（Python 库）和 Brotli（解码算法）。在终端里执行：

bash
复制代码
pip3 install --upgrade fonttools brotli
--upgrade 确保安装最新版本，减少兼容性问题。
如果看到 Successfully installed fonttools… brotli… 这类提示，就表示安装 OK。
三、将 WOFF2 → TTF/OTF 的两种方法
方法 A：使用 TTX 命令（最通用，两步走）
1. 把 WOFF2 解压成 TTX
把你的 MyFont.woff2 放到一个文件夹里（例如：桌面/Desktop 下新建文件夹 font）。
打开“终端”，输入以下两行命令（每行按回车）：
bash
复制代码
# 先切换到存放 woff2 的目录
cd ~/Desktop/font

# 把 woff2 转成 ttx (XML) 格式
python3 -m fontTools.ttx -f MyFont.woff2
cd ~/Desktop/font：
cd 是“Change Directory”；~ 表示你的用户目录，所以 ~/Desktop/font 就是“桌面里的 font 文件夹”。
python3 -m fontTools.ttx -f MyFont.woff2：
python3 -m fontTools.ttx 表示用 Python 的 fontTools.ttx 模块来执行；
-f 表示强制覆盖/继续操作；
MyFont.woff2 是输入文件名。
这一步会在同目录下生成一个 MyFont.ttx。
2. 把 TTX 转成 TTF (或 OTF)
仍然在同一个终端窗口，输入：

bash
复制代码
python3 -m fontTools.ttx -f MyFont.ttx
这会在同目录下生成一个新的字体文件：
如果原字体是 TrueType 轮廓 → MyFont.ttf
如果原字体是 CFF/CFF2 轮廓 → MyFont.otf
执行成功后，你就能在 ~/Desktop/font 文件夹里看到这个新字体文件。
方法 B：直接用 woff2 子命令（若 FontTools 较新）
1. 升级 FontTools 确保支持 woff2 子命令
bash
复制代码
pip3 install --upgrade fonttools
2. 解压命令
bash
复制代码
cd ~/Desktop/font   # 进入放 woff2 的文件夹

python3 -m fonttools woff2 decompress MyFont.woff2 -o MyFont.ttf
-o MyFont.ttf 指定输出文件名。
如果字体是 CFF2 轮廓，可能输出会是 .otf（即使你写 .ttf 后缀，内核依然是 OTF 格式，也不影响安装使用）。
注意：不同版本的 FontTools 对这条命令的兼容不尽相同。如果报“unrecognized arguments”之类的错，说明版本太老或不兼容，可以改用“方法 A”。

四、安装并在软件中测试
在 Finder(访达) 里找到解压后得到的 .ttf 或 .otf。
双击该文件，macOS 会弹出“字体预览/字体册”窗口。
点击 “安装”，系统将其安装到字体目录。
打开需要使用该字体的应用（如 Illustrator、Photoshop、Pages 等），在字体列表里找到这款字体，进行测试。
有时需要重启应用或刷新字体缓存才会生效。
五、常见问题
找不到 python3 命令
说明 Python 3 未安装或未配置好，需先去 Python.org 下载安装。
No module named fontTools / brotli
说明没安装 FontTools 或 Brotli。再次执行：
bash
复制代码
pip3 install --upgrade fonttools brotli
报错：unrecognized arguments (比如 -o…)
说明 FontTools 版本不支持该子命令，或者太旧。请先 pip3 install --upgrade fonttools；
若仍然不行，就用“方法 A”(TTX) 进行两步转换。
输出为 .otf，而不是 .ttf
如果字体内部是 CFF/CFF2 轮廓，就天然是 OTF 格式，不影响正常使用。
安装后软件中打不出字
可能是字体仅包含部分字符、或内部编码不匹配；可用更专业的字体编辑器（FontForge 等）检查具体映射。
重名 / 旧版本冲突
“字体册(Font Book)”里若已存在同名字体，会导致冲突。建议先卸载旧字体，再装新的。
最简要的“命令行范例”汇总
假设你在桌面上新建了一个名为font的文件夹，并将MyFont.woff2放入其中，想要生成 MyFont.ttf/.otf：

bash
复制代码
# 1. 切换到文件夹
cd ~/Desktop/font

# 2.1 方法A：两步走
python3 -m fontTools.ttx -f MyFont.woff2  # -> 生成 MyFont.ttx
python3 -m fontTools.ttx -f MyFont.ttx    # -> 生成 MyFont.ttf / MyFont.otf

# 2.2 方法B：若 FontTools 新版支持
# python3 -m fonttools woff2 decompress MyFont.woff2 -o MyFont.ttf
然后双击新生成的字体文件安装即可。

这样做，你就能非常清晰地从头到尾完成：
进入文件夹 → 2. 执行转换命令 → 3. 得到 TTF/OTF → 4. 安装并使用
一切就绪，祝你转换顺利！
