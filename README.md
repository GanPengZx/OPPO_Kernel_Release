# 📱 OPPO/一加 内核自动编译脚本

<p align="center">
  <img src="https://img.shields.io/badge/Platform-Android-brightgreen?logo=android" alt="Platform">
  <img src="https://img.shields.io/badge/Build-GitHub%20Actions-blue?logo=githubactions" alt="Build">
  <img src="https://img.shields.io/github/stars/GanPengZx/OPPO_Kernel_Release?style=social" alt="Stars">
  <img src="https://img.shields.io/github/forks/GanPengZx/OPPO_Kernel_Release?style=social" alt="Forks">
</p>

> 借助 GitHub Actions 的云端算力，实现 OPPO/OnePlus 部分机型内核的**全自动化编译**。只需填写参数，即可坐等成品内核镜像出炉！

---

## 📑 目录
- [🚀 快速开始](#-快速开始)
- [📦 获取产物](#-获取产物)
- [⚙️ 编译原理](#️-编译原理)
- [🛠️ 常见问题](#️-常见问题)

---

## 🚀 快速开始

### 1. 前置条件
确保你的 GitHub 仓库中包含以下两个核心文件：
- `.github/workflows/build.yml` (GitHub Actions 自动化脚本)
- `README.md` (本文件)

### 2. 触发编译
无需本地配置任何环境，全程在云端运行：
1. 进入项目主页，点击顶部的 **Actions** 标签页。
2. 在左侧工作流列表中选中 **Build Kernel**。
3. 点击右侧的 **Run workflow** 按钮，展开参数面板。

### 3. 填写编译参数
根据你的机型源码情况，填入对应的仓库地址和分支。如果是首次测试，可直接使用默认值。

| 参数名 | 说明 | 示例值 |
| :--- | :--- | :--- |
| `proprietary_repo` | 闭源驱动仓库地址 | `https://github.com/oppo-source/..._oppo_sm6375` |
| `proprietary_branch`| 闭源驱动分支 | `oppo/sm6375_t_13.1.0_oppo_a1_5g` |
| `kernel_repo` | 内核源码仓库地址 | `https://github.com/oppo-source/...kernel_oppo_sm6375` |
| `kernel_branch` | 内核源码分支 | `oppo/sm6375_t_13.1.0_oppo_a1_5g` |

填完后，点击绿色的 **Run workflow** 即可静待佳音！

---

## 📦 获取产物

编译成功后，系统会自动打包生成产物：
1. 在对应的 Action 运行记录页面，向下滑动找到 **Artifacts** 区域。
2. 点击下载 `kernel-image` 压缩包。
3. 解压后得到的 `Image` 文件，就是你要的内核镜像啦！

---

## ⚙️ 编译原理

本脚本完美复刻了传统本地编译的核心逻辑，并将其搬到了云端：
1. **拉取资源**：分别克隆闭源驱动仓库和纯净内核源码仓库。
2. **重构目录**：在 `/kernel` 目录下建立 `common` 文件夹，并将内核源码移入其中，符合安卓内核编译树的标准结构。
3. **注入驱动**：将闭源仓库中的 `vendor` 和 `kernel` 相关文件合并到编译树中。
4. **一键编译**：在 `/kernel/common` 目录下执行 `make` 命令，输出最终镜像。

---

## 🛠️ 常见问题 (Troubleshooting)

**Q1: 编译时报错 `Permission denied`？**
> **答**：这是常见的文件权限缺失问题。请确保你的 `build.yml` 脚本中包含了赋予执行权限的命令（例如 `chmod +x` 相关操作），以保证编译脚本具有正确的运行权限。

---

<p align="center">
  Happy Hacking! ❤️
</p>