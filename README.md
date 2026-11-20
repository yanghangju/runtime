# 短剧切片 Windows x64 运行时

这个独立仓库只包含切片工作台所需的运行依赖：

- `python/`：CPython 3.12.4、标准库、DLL 和已安装的第三方包（包括 librosa 0.11.0）。无需另装 Python 或运行 `pip install`。
- `ffmpeg/`：FFmpeg 9.0.2、FFprobe 及其 DLL。无需配置系统 `PATH`。

[manifest.json](manifest.json) 记录版本和媒体工具校验值。插件从自身的 `runtime/` 目录读取这些文件，不需要修改配置。

## 检出与验证

从源码部署时，先安装 [Git LFS](https://git-lfs.com/)。在插件根目录执行以下命令，将这个仓库检出到 `runtime/`（如果运行时已随插件打包，则无需克隆）：

```powershell
git clone "<运行时仓库路径或 URL>" runtime
git -C runtime lfs pull
```

在运行时目录内执行：

```powershell
.\python\python.exe -IB -c 'import librosa, numpy, scipy, PIL; print(librosa.__version__)'
.\ffmpeg\ffmpeg.exe -version
.\ffmpeg\ffprobe.exe -version
```

[第三方许可](licenses/) 随运行时保留；对外发布二进制前，需核对再分发条件并备齐对应源码和构建材料（见 [FFmpeg](licenses/FFMPEG.txt) 和 [FFprobe](licenses/FFPROBE.txt) 说明）。
