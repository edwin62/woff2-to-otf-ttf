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
