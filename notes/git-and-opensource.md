# Git 与开源贡献笔记

> 2026-11-13 记录。当天完成了从装 Git 到第一个 PR 合并的完整流程。

## 一、本地 Git 基础

```bash
git init                        # 初始化仓库（默认分支 main）
git status                      # 查看状态（最常用，迷路先看它）
git add .                       # 暂存所有改动
git commit -m "说明"            # 提交，一句话说清"改了什么、为什么"
git log --oneline --decorate    # 查看简洁历史
git diff                        # 查看未暂存的改动
```

## 二、连接 GitHub

```bash
git remote add origin <仓库地址>   # 关联远端
git push -u origin main            # 首次推送（-u 建立跟踪，以后直接 git push）
git pull                           # 拉取远端更新
```

- 身份配置：`git config --global user.name / user.email`
- 建议用 GitHub 的 noreply 邮箱，避免暴露真实邮箱
- **绝对不要把 API Key、密码提交到仓库**（.gitignore 里排除 `.env`、`*.key`）

## 三、参与开源的标准流程（fork 模式）

```text
1. Fork 原项目到自己账号
2. git clone 自己的 fork
3. git checkout -b fix-xxx        # 每个 PR 一个新分支，main 保持干净
4. 改动 → commit → push 到 fork
5. 网页提 PR：base 指向【原项目】的 main
6. 等 CI 检查和 review，合并后删分支
```

## 四、第一条 PR 的实战教训

1. **提 PR 前必须先检查 Issue 是否已被认领**：
   - 打开 Issue 页面看评论区有没有关联 PR
   - 搜同仓库的开放 PR：`is:pr is:open` 关键词搜标题
   - 重复提交 PR 是帮倒忙，浪费维护者时间
2. **核实修复覆盖范围**：本次 `algoritm_A` 错别字看似一处，
   实际被两个 PR 覆盖了 6 个语言版本（#2000 zh、#2024 en/ja/ko/ru/zh-hant）
3. **推荐仓库可能消失**：FastGithub 原仓库已删除（404），
   参考别人的推荐时先确认仓库能打开、近期有提交
4. Chrome 自动翻译会乱翻 GitHub 界面（main→主角色、Files→档案），
   建议对 github.com 关闭翻译，改用 GitHub 自带中文设置
5. PR 描述区如果有 `- [ ]` 清单，勾上它（改成 `- [x]`），显得认真

## 五、读 Issue / PR 的方法

- 筛选：`is:issue is:open label:"good first issue"`
- 重点看：报错者如何描述现象（环境、复现步骤、日志）→
  维护者追问什么 → 最终如何闭环
- PR 看 `Files changed`：绿行新增、红行删除，从文档类小 PR 读起

## 六、当前进行中

- [x] 注册 GitHub、建 learning-notes 仓库
- [x] 第一个 PR：first-contributions #128404（已合并）
- [ ] 用 hello-algo 学数据结构，阅读中记录发现的错误（发现即提 Issue）
