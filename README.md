# ZCSR 1.0

ZCSR 1.0 的可下载源码包集合，按仓库拆分，便于单独取用和核对。

## 下载

| 文件 | 内容 |
|---|---|
| `dist/zcsr-engine-1.0.0.zip` | 引擎核心、2D 渲染、Light2D、平台/输入/音频、测试与集成示例 |
| `dist/zcsr-uim-1.0.0.zip` | UIM 页面与控件库 |
| `dist/zcsr-runtime-1.0.0.zip` | Runtime 宿主与设置页 |
| `dist/zcsr-editor-1.0.0.zip` | 编辑器 |
| `dist/zcsr-tools-1.0.0.zip` | 工作区、调试绘制、性能分析、塔防与 2.5D 工具 |

源码包由 `git archive` 从各仓库 `v1.0.0` 生成，不含 `.git` 历史。校验：

```sh
sha256sum -c SHA256SUMS.txt
```

## 版本与提交

| 仓库 | 标签 | 提交 |
|---|---|---|
| zero-coupling-signal-router | `v1.0.0` | `9b38231df43df1d7782c6ff5ad4a1ff3bb805a32` |
| UIM | `v1.0.0` | `1fdc63b5f89bf58dd2443d3d0d3684effd6a9562` |
| zcsr_runtime | `v1.0.0` | `81cfa7aaeb2d34e1c5082a89714d7505947bae62` |
| zcsr_editor | `v1.0.0` | `fac2ea6373fb6e69000c191e720d168b3b8d97cf` |
| zcsr_tools | `v1.0.0` | `8ce9f75f54b0df7a74720c584ade9f9405fd4441` |

## 验证状态

| 仓库 | 结果 |
|---|---|
| engine | 23/23 CTest 通过 |
| UIM | 2/2 通过 |
| runtime | 默认 6/6；settings ON 10/10 |
| editor | 20/20 通过 |
| tools | 9/9 通过 |

engine 的 23/23 与 tools 的 9/9 均按 1.0 标签状态记录。

## 构建

Windows（MSVC + Ninja）：

```sh
cmake -S zcsr-engine-1.0.0 -B build -G Ninja -DZCSR_ENABLE_BOX2D=OFF
cmake --build build
ctest --test-dir build
```

Linux（X11/GLX 或 Wayland/EGL，自动选择）：

```sh
cmake -S zcsr-engine-1.0.0 -B build -G Ninja -DZCSR_ENABLE_BOX2D=OFF
cmake --build build
ctest --test-dir build
```

窗口后端可用 `ZCSR_LINUX_WINDOW_BACKEND=auto|x11|wayland|none` 指定；音频后端可用 `ZCSR_AUDIO_BACKEND=auto|pipewire|alsa|none` 指定。

## 目录关系

- `engine` 提供 `include/zcsr/` 契约头和各模块静态库。
- `UIM`、`runtime`、`editor`、`tools` 作为消费者构建，不反向侵入引擎模块内部。
- 各仓库只通过公共契约头协作，模块之间不互相包含源码。

## 文档政策

`docs/archive/` 保留历史架构、API、数学分析和集成说明，用于追溯设计演进，不代表当前实现。历史文档中的旧模块名和旧口径以归档快照为准。

## 许可

AGPLv3，见 `LICENSE`。衍生作品（包括网络服务）必须按同一许可开源。
