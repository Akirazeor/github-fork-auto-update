# 自动同步上游仓库 (Upstream Sync Workflow)

这是一个 GitHub Actions Workflow，用于自动将你的 fork（派生）仓库与上游（原始）仓库的特定分支保持同步。

## 功能

* **定时同步**：默认配置为每周日午夜（UTC时间）自动从上游仓库拉取最新更改。
* **手动触发**：允许你随时从 GitHub Actions 标签页手动运行同步。
* **分支指定**：你可以指定要同步的上游仓库分支和目标 fork 仓库分支。
* **仅限 Fork**：此 workflow 包含一个检查，确保它只在 fork 仓库中运行。
* **错误提示**：如果同步步骤失败，会输出一条提示信息。

## 如何使用

1.  **导航至 Actions 页面**：

      * 打开你在 GitHub 上的 Fork 项目。
      * 点击仓库导航栏中的 **Actions** 标签页。
        ![image](https://github.com/user-attachments/assets/fbbb7362-e26c-4727-b533-226e6a72e482)


2.  **新建 Workflow 文件**：

      * 在 Actions 页面，点击 **New workflow** 按钮。
      * 接着，选择 **set up a workflow yourself** (自己设置一个工作流程)。
        ![image](https://github.com/user-attachments/assets/6a67ef85-e328-44b1-b05e-0cc126d5a817)

3.  **粘贴 Workflow 代码并命名文件**：

      * 将sync-upstream.yml完整复制。
      * 粘贴到打开的编辑器中。
      * 在编辑器顶部的 `name:` 字段右侧（或者如果该字段不存在，则在页面顶部中间位置），将文件名修改为 `sync-upstream.yml`。
          * GitHub 会自动将其保存在 `.github/workflows/` 目录下。

4.  **修改核心配置参数**：
    在粘贴的代码中，找到并修改以下关键参数以匹配你的需求：

      * **(重要) 上游仓库路径 (`upstream_sync_repo`)**：

          * 找到 `upstream_sync_repo:` 这一行。
          * 将其值修改为 **你 Fork 的原始仓库** 的路径。格式通常是 `原始仓库拥有者名称/原始仓库名称`。
              * 例如，如果你 Fork 的是 `some-cool-project/some-cool-project`，那么这里就填写 `some-cool-project/some-cool-project`。
              * 这个信息通常在你 Fork 仓库页面的仓库名称下方，会有一行小字显示 "forked from OWNER/REPO"。
              ![image](https://github.com/user-attachments/assets/977f6c4b-79ae-415f-9a8e-e89a7d890bea)

      * **(可选) 定时任务执行频率 (`cron`)**：

          * 找到 `cron:` 这一行。
          * 默认值 `'0 0 * * 0'` 表示每周日午夜 (UTC 时间) 执行一次。
          * 你可以根据需求修改此 [cron 表达式](https://crontab.guru/)。例如，`'0 0 * * *'` 代表每天午夜执行。如果不需要定时执行，可以删除整个 `schedule` 部分（但保留 `workflow_dispatch` 以便手动触发）。

      * **(可选) 同步分支名称**：

          * `upstream_sync_branch:`：上游仓库中你希望同步的分支名称 (例如 `main`, `master`, `develop`)。
          * `target_sync_branch:`：你的 Fork 仓库中，希望将更新同步到的分支名称 (通常与 `upstream_sync_branch` 保持一致)。
          * 根据需要修改这两个值。

5.  **提交 Workflow 文件**：

      * 完成代码粘贴和参数修改后，点击页面右上角的 **Commit changes...** 按钮。
      * 你可以直接选择 **Commit directly to the `main` branch** (或其他你的默认分支)，然后点击 **Commit changes**。

6.  **测试运行 (推荐)**：

      * Workflow 文件提交后，再次导航到仓库的 **Actions** 标签页。
      * 在左侧列表中，你应该能看到你刚刚创建的 Workflow 名称 (例如 "Upstream Sync")。点击它。
      * 在右侧，你会看到一个 **Run workflow** 的下拉按钮（如果 `workflow_dispatch:` 已配置）。点击它，然后再次点击绿色的 **Run workflow** 按钮。
      * 你可以点击正在运行的 Workflow 实例来查看其执行日志和状态，确保一切按预期工作。如果运行成功，表示配置无误。
      ![image](https://github.com/user-attachments/assets/5cf5c5be-4a55-4a1d-9e78-9bac9c47fa31)
