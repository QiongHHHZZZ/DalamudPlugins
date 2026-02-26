# DalamudPlugins（国服自定义插件源）

这是一个用于 Dalamud 的自定义插件仓库清单（`pluginmaster.json`），用于维护多个插件的国服版本发布。

## 用户使用方法

在 Dalamud 中添加以下自定义仓库地址：

- `https://raw.githubusercontent.com/QiongHHHZZZ/DalamudPlugins/main/pluginmaster.json`

路径：`Dalamud -> 插件安装器 -> 设置 -> 自定义插件仓库`

## 仓库结构

- `pluginmaster.json`：插件清单（核心文件）
- `README.md`：维护规范与发布流程

## 版本规则（通用，适用于后续新增插件）

为保证 Dalamud 版本比较稳定，统一使用 **4 段纯数字版本号**：

- 格式：`A.B.C.D`
- 不使用带后缀版本（如 `-beta`）和 5 段版本。

### 推荐规则（上游同步 + 本地修订）

当插件有上游版本时，建议第 4 段按 `UUFF` 编码：

- `UU`：上游第 4 段（两位）
- `FF`：本地修订序号（`00-99`）

示例 A（有上游，推荐）：

- 上游：`1.2.3.45`
- 纯上游同步：`1.2.3.4500`
- 本地修订 1：`1.2.3.4501`
- 本地修订 2：`1.2.3.4502`
- 上游升级到 `1.2.3.46`：`1.2.3.4600`

示例 B（无上游，自研插件）：

- 首发：`1.0.0.1`
- 第二次发布：`1.0.0.2`
- 小版本功能更新：`1.1.0.1`

说明：

- `00` 表示纯同步上游；`01+` 表示本地改动版本（仅适用于“有上游”的插件）。
- 版本号必须单调递增，避免客户端不提示更新。
- 上述示例仅用于演示版本规则，不指向任何具体插件。

## 新增插件流程

1. 准备插件仓库与可下载安装包（zip）。
2. 确认插件项目版本号（`Version` / `AssemblyVersion` / `FileVersion`）一致。
3. 在插件仓库创建 `tag/release`，上传 zip 资产。
4. 在 `pluginmaster.json` 新增条目，至少包含：
   - `Name`
   - `InternalName`
   - `AssemblyVersion`
   - `RepoUrl`
   - `DownloadLinkInstall`
   - `DownloadLinkUpdate`
   - `DalamudApiLevel`
5. 提交并推送 `DalamudPlugins` 仓库。

## 更新已有插件流程

1. 在插件源码仓库更新版本号并构建发布包。
2. 发布新 `tag/release`，确认 zip 链接可下载。
3. 修改 `pluginmaster.json` 对应条目：
   - `AssemblyVersion`
   - `DownloadLinkInstall`
   - `DownloadLinkUpdate`
   - （可选）`Description` / `Punchline`
4. 推送后在 Dalamud 中刷新仓库，确认可检测到更新。

## 发布前检查清单

- [ ] `pluginmaster.json` 格式合法（JSON 无语法错误）
- [ ] `AssemblyVersion` 与插件包版本一致
- [ ] 安装/更新链接可访问且文件名正确
- [ ] 版本号高于上一发布版本
- [ ] 在 Dalamud 中可正常安装/更新

## 说明

- 本仓库是独立分发渠道，可以与上游官方仓库不同步。
- 如需追溯每个插件的版本细节，请以插件源码仓库和 release 记录为准。
