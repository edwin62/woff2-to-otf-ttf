# 字体转换笔记

## 一、前提条件

### 1. 系统要求
- **系统**：macOS
- **Python 3 已安装**：
  - 打开“终端(Terminal)”，输入：
    ```bash
    python3 --version
    ```
  - 如果能显示 `Python 3.x.x`，说明已安装。如果提示“command not found”，需要先从 [Python 官网](https://www.python.org/) 下载并安装。

### 2. pip3 已安装
- 在终端输入：
  ```bash
  pip3 --version
  ```
  - 如果显示 `pip 21.x.x` 或类似版本，说明已安装。
  - 如果没有，可以执行：
    ```bash
    python3 -m ensurepip --upgrade
    ```
    这会自动安装或升级 pip3。

## 二、安装工具：FontTools + Brotli

- WOFF2 解压需要 **FontTools**（Python 库）和 **Brotli**（解码算法）。
- 在终端执行以下命令安装：
  ```bash
  pip3 install --upgrade fonttools brotli
  ```
- 如果看到 `Successfully installed fonttools… brotli…`，表示安装成功。

## 三、将 WOFF2 转换为 TTF/OTF 的两种方法

### 方法 A：使用 TTX 命令（两步走）

#### 1. 解压 WOFF2 为 TTX
- 将 `MyFont.woff2` 放入一个文件夹（例如：桌面上的 `font` 文件夹）。
- 打开终端，执行以下命令：
  ```bash
  # 切换到存放 woff2 的目录
  cd ~/Desktop/font

  # 将 woff2 转换为 ttx (XML) 格式
  python3 -m fontTools.ttx -f MyFont.woff2
  ```
  - `cd ~/Desktop/font`：切换到桌面上的 `font` 文件夹。
  - `python3 -m fontTools.ttx -f MyFont.woff2`：
    - 用 `fontTools.ttx` 模块处理字体文件。
    - `-f`：强制覆盖。
    - `MyFont.woff2` 是输入文件名。

- 运行成功后，会在同目录生成 `MyFont.ttx`。

#### 2. 将 TTX 转换为 TTF 或 OTF
- 在终端输入：
  ```bash
  python3 -m fontTools.ttx -f MyFont.ttx
  ```
- 运行成功后，会生成：
  - 如果原字体是 TrueType 轮廓 → `MyFont.ttf`
  - 如果原字体是 CFF/CFF2 轮廓 → `MyFont.otf`

### 方法 B：直接使用 `woff2` 子命令（FontTools 较新版本支持）

#### 1. 确保 FontTools 是最新版本
```bash
pip3 install --upgrade fonttools
```

#### 2. 解压 WOFF2
```bash
cd ~/Desktop/font   # 切换到放置 woff2 的文件夹
python3 -m fonttools woff2 decompress MyFont.woff2 -o MyFont.ttf
```
- `-o MyFont.ttf`：指定输出文件名。
- 如果字体是 CFF2 轮廓，可能输出为 `.otf` 格式，即使指定 `.ttf` 后缀，仍为 OTF 格式。

### 注意事项
- **方法 A 更通用**，适用于所有版本的 FontTools。
- 如果方法 B 报错 `unrecognized arguments`，说明 FontTools 版本过旧或不兼容，请更新或改用方法 A。

## 四、安装并在软件中测试

1. 在 Finder(访达) 中找到解压得到的 `.ttf` 或 `.otf` 文件。
2. 双击文件，macOS 会弹出“字体预览/字体册”窗口。
3. 点击“安装”，系统会将字体安装到字体目录。
4. 打开需要使用该字体的应用（如 Illustrator、Photoshop、Pages 等），在字体列表中找到该字体并测试。
5. 有时需要重启应用或刷新字体缓存才能生效。

## 五、常见问题

### 1. 找不到 `python3` 命令
- Python 3 未安装或未配置好。
- 前往 [Python.org](https://www.python.org/) 下载并安装。

### 2. 报错：`No module named fontTools / brotli`
- 表示未安装 FontTools 或 Brotli。
- 再次执行：
  ```bash
  pip3 install --upgrade fonttools brotli
  ```

### 3. 报错：`unrecognized arguments`（如 `-o`）
- FontTools 版本不支持该子命令，或版本过旧。
- 执行以下命令升级：
  ```bash
  pip3 install --upgrade fonttools
  ```
- 如果仍不行，改用“方法 A”。

### 4. 输出为 `.otf` 而非 `.ttf`
- 如果字体内部是 CFF/CFF2 轮廓，天然为 OTF 格式，不影响使用。

### 5. 安装后软件中无法输入字符
- 字体可能仅包含部分字符，或内部编码不匹配。
- 可使用专业字体编辑器（如 FontForge）检查具体映射。

### 6. 重名 / 旧版本冲突
- 如果“字体册(Font Book)”中已存在同名字体，可能导致冲突。
- 建议先卸载旧版本字体，再安装新版本。

## 六、命令行范例汇总

假设在桌面上新建了一个名为 `font` 的文件夹，并将 `MyFont.woff2` 放入其中，想要生成 `MyFont.ttf` 或 `MyFont.otf`。

### 方法 A
```bash
# 1. 切换到文件夹
cd ~/Desktop/font

# 2.1 解压为 TTX
python3 -m fontTools.ttx -f MyFont.woff2

# 2.2 转换为 TTF/OTF
python3 -m fontTools.ttx -f MyFont.ttx
```

### 方法 B（如果 FontTools 较新）
```bash
# 1. 切换到文件夹
cd ~/Desktop/font

# 2. 解压为 TTF/OTF
python3 -m fonttools woff2 decompress MyFont.woff2 -o MyFont.ttf
```

然后双击新生成的字体文件安装即可。
