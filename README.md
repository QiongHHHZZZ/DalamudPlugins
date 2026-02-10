# DalamudPlugins

这是一个 Dalamud 自定义插件仓库清单（pluginmaster）。

## 使用方法

在 Dalamud → 插件安装器 → 设置 → 自定义插件仓库 中添加：

- https://raw.githubusercontent.com/QiongHHHZZZ/DalamudPlugins/main/pluginmaster.json

## 版本号规则（上游同步 + 本地修订）

为避免和上游版本冲突，同时保证 Dalamud 可正确比较更新版本，统一使用 **4 段版本号**：

- 格式：`主版本.次版本.补丁.构建`
- 约定：第 4 段采用“上游版本尾号 + 两位本地修订”

示例（以上游 `4.0.4.39` 为例）：

- 上游同步版：`4.0.4.3900`
- 本地修订 1：`4.0.4.3901`
- 本地修订 2：`4.0.4.3902`
- 上游升级到 `4.0.4.40` 时：`4.0.4.4000`

说明：

- `00` 代表“纯上游同步”；`01+` 代表“基于该上游版本的本地修订”。
- 必须保证版本号单调递增，避免客户端无法识别更新。
- 不使用 5 段版本号（如 `4.0.4.39.1`），避免 Dalamud 解析/比较问题。

## 发布流程（手动）

每次发布请按以下顺序执行：

1. 在插件项目中更新 `Version`（如 `4.0.4.3901`）。
2. 构建并打包 `Artisan.zip`。
3. 在 `Artisan` 仓库创建同名 tag/release（如 `v4.0.4.3901`），上传 `Artisan.zip`。
4. 更新本仓库 `pluginmaster.json` 中 `Artisan` 条目：
   - `AssemblyVersion`
   - `DownloadLinkInstall`
   - `DownloadLinkUpdate`
5. 提交并推送 `DalamudPlugins`。

这样可以确保：版本可区分、客户端下载可用、插件更新可见。
