# macOS 下将 WOFF2 转换为 TTF/OTF 的完整教程

本教程适用于 macOS 系统，详细介绍如何通过 Python 和 FontTools 将 `.woff2` 格式的可变字体转换为 `.ttf` 或 `.otf` 格式，同时包含每条命令的说明和常见问题的解决方案。

---

## 一、前提条件

1. **系统**：macOS  
2. **已安装 Python 3**：  
   - 打开“终端(Terminal)”，输入：  
     ```bash
     python3 --version
     ```  
   - 若能显示 `Python 3.x.x` 就说明已装好。若提示“command not found”，需先去 [Python 官网](https://www.python.org/downloads/mac-osx/) 下载并安装。  
3. **已安装 `pip3`**：  
   - 在终端输入：  
     ```bash
     pip3 --version
     ```  
   - 如果没有，可执行：  
     ```bash
     python3 -m ensurepip --upgrade
     ```

---

## 二、安装工具：FontTools + Brotli

WOFF2 解压需要 FontTools（Python 库）和 Brotli（解码算法）。在终端里执行：

```bash
pip3 install --upgrade fonttools brotli
如果看到 Successfully installed fonttools… brotli… 这类提示，就表示安装成功。
三、将 WOFF2 转换为 TTF/OTF
方法 A：使用 TTX 命令（通用两步法）
1. 解压 WOFF2 为 TTX
把你的 MyFont.woff2 放到一个文件夹里（例如：桌面下 font 文件夹）。
打开终端，输入以下命令：
bash
复制代码
# 切换到存放 WOFF2 文件的目录
cd ~/Desktop/font

# 将 WOFF2 转换为 TTX 格式
python3 -m fontTools.ttx -f MyFont.woff2
这会生成一个 MyFont.ttx 文件。

2. 将 TTX 转为 TTF/OTF
在同一终端窗口，输入以下命令：

bash
复制代码
python3 -m fontTools.ttx -f MyFont.ttx
如果字体是 TrueType 轮廓 → 输出 .ttf
如果字体是 CFF/CFF2 轮廓 → 输出 .otf
结果
解压完成后，你会在同文件夹下看到生成的 .ttf 或 .otf 文件。

方法 B：直接用 woff2 子命令（较新版本支持）
1. 升级 FontTools
确保 FontTools 是最新版本：

bash
复制代码
pip3 install --upgrade fonttools
2. 一步解压 WOFF2
切换到文件所在目录，输入以下命令：

bash
复制代码
cd ~/Desktop/font

python3 -m fonttools woff2 decompress MyFont.woff2 -o MyFont.ttf
-o MyFont.ttf 用于指定输出文件名。
如果字体是 CFF2 轮廓，输出文件仍会是 .otf，即使指定 .ttf 后缀。
四、安装字体并测试
在 Finder 中找到生成的 .ttf 或 .otf 文件。
双击文件，打开字体预览窗口。
点击“安装”，将字体添加到系统中。
打开设计软件（如 Illustrator、Photoshop），在字体列表中找到这款字体进行测试。
五、常见问题
1. 找不到 python3 或 pip3 命令
需先安装 Python 3 和 pip：

去 Python 官网 下载并安装。
或执行以下命令安装 pip：
bash
复制代码
python3 -m ensurepip --upgrade
2. 提示 No module named fontTools 或 No module named brotli
说明需要安装依赖库：

bash
复制代码
pip3 install --upgrade fonttools brotli
3. 输出为 .otf 而不是 .ttf
如果原字体使用的是 CFF/CFF2 轮廓，则解压后会自动生成 .otf 格式。
.otf 和 .ttf 功能相同，均可正常安装和使用。
4. 字体安装后无法正常显示
可能是字体仅包含部分字符或编码映射不全，可使用专业工具（如 FontForge）检查。
确保系统中没有冲突的旧版本字体，必要时先卸载旧字体。
六、完整命令总结
方法 A：两步走（通用）
bash
复制代码
cd ~/Desktop/font          # 切换到文件夹
python3 -m fontTools.ttx -f MyFont.woff2  # 解压为 TTX
python3 -m fontTools.ttx -f MyFont.ttx    # 转为 TTF/OTF
方法 B：一步完成（若支持）
bash
复制代码
cd ~/Desktop/font          # 切换到文件夹
python3 -m fonttools woff2 decompress MyFont.woff2 -o MyFont.ttf
希望这份教程能够帮助你轻松完成字体格式的转换！如有疑问，欢迎随时反馈。

markdown
复制代码

---

## 上传到 GitHub 的方法

1. 登录 [GitHub](https://github.com)，点击右上角 **`+`** → **`New repository`**。
2. 创建一个新仓库，填写仓库名（如 `woff2-to-ttf-guide`），选中 **`Add a README file`**。
3. 在新仓库中点击 `README.md` 文件，选择 **Edit**。
4. 将上述 Markdown 文本**全部复制粘贴**到 `README.md` 文件中。
5. 点击 **Commit changes** 保存即可。

下次需要时，只需访问你的仓库，就能直接查看和分享这份完整教程！ 🎉





您说：
你给我的第一段markdown没错，但是后面没有啊，请你把后面的文字也一起变为markdown那样的格式
ChatGPT 说：
ChatGPT
以下是完整的 Markdown 格式 文档，包含之前未格式化的部分，适合直接复制到 GitHub 的 README.md 文件中。

markdown
复制代码
# macOS 下将 WOFF2 转换为 TTF/OTF 的完整教程

本教程适用于 macOS 系统，详细介绍如何通过 Python 和 FontTools 将 `.woff2` 格式的可变字体转换为 `.ttf` 或 `.otf` 格式，同时包含每条命令的说明和常见问题的解决方案。

---

## 一、前提条件

1. **系统**：macOS  
2. **已安装 Python 3**：  
   - 打开“终端(Terminal)”，输入：  
     ```bash
     python3 --version
     ```  
   - 若能显示 `Python 3.x.x` 就说明已装好。若提示“command not found”，需先去 [Python 官网](https://www.python.org/downloads/mac-osx/) 下载并安装。  
3. **已安装 `pip3`**：  
   - 在终端输入：  
     ```bash
     pip3 --version
     ```  
   - 如果没有，可执行：  
     ```bash
     python3 -m ensurepip --upgrade
     ```

---

## 二、安装工具：FontTools + Brotli

WOFF2 解压需要 FontTools（Python 库）和 Brotli（解码算法）。在终端里执行：

```bash
pip3 install --upgrade fonttools brotli
如果看到 Successfully installed fonttools… brotli… 这类提示，就表示安装成功。
三、将 WOFF2 转换为 TTF/OTF
方法 A：使用 TTX 命令（通用两步法）
1. 解压 WOFF2 为 TTX
把你的 MyFont.woff2 放到一个文件夹里（例如：桌面下 font 文件夹）。
打开终端，输入以下命令：
bash
复制代码
# 切换到存放 WOFF2 文件的目录
cd ~/Desktop/font

# 将 WOFF2 转换为 TTX 格式
python3 -m fontTools.ttx -f MyFont.woff2
这会生成一个 MyFont.ttx 文件。

2. 将 TTX 转为 TTF/OTF
在同一终端窗口，输入以下命令：

bash
复制代码
python3 -m fontTools.ttx -f MyFont.ttx
如果字体是 TrueType 轮廓 → 输出 .ttf
如果字体是 CFF/CFF2 轮廓 → 输出 .otf
结果
解压完成后，你会在同文件夹下看到生成的 .ttf 或 .otf 文件。

方法 B：直接用 woff2 子命令（较新版本支持）
1. 升级 FontTools
确保 FontTools 是最新版本：

bash
复制代码
pip3 install --upgrade fonttools
2. 一步解压 WOFF2
切换到文件所在目录，输入以下命令：

bash
复制代码
cd ~/Desktop/font

python3 -m fonttools woff2 decompress MyFont.woff2 -o MyFont.ttf
-o MyFont.ttf 用于指定输出文件名。
如果字体是 CFF2 轮廓，输出文件仍会是 .otf，即使指定 .ttf 后缀。
四、安装字体并测试
在 Finder 中找到生成的 .ttf 或 .otf 文件。
双击文件，打开字体预览窗口。
点击“安装”，将字体添加到系统中。
打开设计软件（如 Illustrator、Photoshop），在字体列表中找到这款字体进行测试。
五、常见问题
1. 找不到 python3 或 pip3 命令
需先安装 Python 3 和 pip：

去 Python 官网 下载并安装。
或执行以下命令安装 pip：
bash
复制代码
python3 -m ensurepip --upgrade
2. 提示 No module named fontTools 或 No module named brotli
说明需要安装依赖库：

bash
复制代码
pip3 install --upgrade fonttools brotli
3. 输出为 .otf 而不是 .ttf
如果原字体使用的是 CFF/CFF2 轮廓，则解压后会自动生成 .otf 格式。
.otf 和 .ttf 功能相同，均可正常安装和使用。
4. 字体安装后无法正常显示
可能是字体仅包含部分字符或编码映射不全，可使用专业工具（如 FontForge）检查。
确保系统中没有冲突的旧版本字体，必要时先卸载旧字体。
六、完整命令总结
方法 A：两步走（通用）
bash
复制代码
cd ~/Desktop/font          # 切换到文件夹
python3 -m fontTools.ttx -f MyFont.woff2  # 解压为 TTX
python3 -m fontTools.ttx -f MyFont.ttx    # 转为 TTF/OTF
方法 B：一步完成（若支持）
bash
复制代码
cd ~/Desktop/font          # 切换到文件夹
python3 -m fonttools woff2 decompress MyFont.woff2 -o MyFont.ttf
希望这份教程能够帮助你轻松完成字体格式的转换！如有疑问，欢迎随时反馈。

markdown
复制代码

---

### 将上述文档上传到 GitHub 的操作

1. **登录 [GitHub](https://github.com)**。
2. 点击右上角 **`+`** → **`New repository`**。
3. 填写仓库名称（如 `woff2-to-ttf-guide`），选中 **`Add a README file`**。
4. 创建后，点击进入 `README.md` 文件，选择 **Edit**。
5. 将以上 **Markdown 文档** 复制粘贴到 `README.md` 文件中。
6. 点击 **Commit changes** 保存。

这样，你就拥有了一份详细的在线教程，随时可访问或分享！ 🎉
