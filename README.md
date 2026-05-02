# OPPO/OnePlus 内核自动编译

本仓库使用 GitHub Actions 实现自动化编译 OPPO/OnePlus 设备的手机内核。

## 📖 使用教程

### 1. 准备工作
确保你的仓库中包含以下文件：
- `.github/workflows/build.yml` (即你之前生成的 Actions 脚本)
- 本 README.md 文件

### 2. 开始编译
1. 进入你的 GitHub 仓库主页。
2. 点击顶部的 **Actions** 标签页。
3. 在左侧工作流列表中选择 **Build OPPO Kernel**。
4. 点击右侧的 **Run workflow** 按钮。
5. 填入以下参数（或直接用默认值测试）：

| 参数名 | 说明 | 示例值 |
| :--- | :--- | :--- |
| `proprietary_repo` | 闭源驱动仓库地址 | `https://github.com/oppo-source/android_kernel_modules_and_devicetree_oppo_sm6375` |
| `proprietary_branch` | 闭源驱动分支 | `oppo/sm6375_t_13.1.0_oppo_a1_5g` |
| `kernel_repo` | 内核源码仓库地址 | `https://github.com/oppo-source/android_kernel_oppo_sm6375` |
| `kernel_branch` | 内核源码分支 | `oppo/sm6375_t_13.1.0_oppo_a1_5g` |

6. 点击绿色的 **Run workflow** 确认运行。

### 3. 下载产物
编译成功后，页面下方会出现 **Artifacts** 区域，点击下载 `kernel-image` 压缩包即可。解压后得到的 `Image` 文件即为内核镜像。

## ⚙️ 编译原理
脚本严格按照酷安教程的逻辑执行：
1. **拉取驱动**：从闭源仓库下载 `vendor` 和 `kernel` 文件夹。
2. **构建结构**：在 `/kernel` 目录下创建 `common` 文件夹。
3. **合并源码**：将内核源码仓库的内容移动到 `/kernel/common` 下。
4. **编译**：在 `/kernel/common` 目录下执行 `make` 命令。

## 🛠️ 常见问题 (Troubleshooting)

### Q1: 编译时报错 `Permission denied`？
**A**: 这是文件权限问题。请确保你的 YAML 脚本中包含修复权限的命令：
