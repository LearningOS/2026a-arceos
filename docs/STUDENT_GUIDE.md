# 学员领取与提交指南

## 1. 绑定账号并领取仓库

在 OpenCamp 加入课程 2078 对应训练营，并绑定自己的 GitHub 登录名。把登录名提供给维护者，接受 GitHub 仓库邀请。无需加入组织成为成员，也无需自己创建或 Fork 作业仓库。

## 2. 克隆作业仓库

```sh
git clone https://github.com/2026f-autotest/2026f-arceos-你的GitHub登录名.git
```

把占位文字替换为自己的登录名；该命令下载已分配的作业仓库。

```sh
cd 2026f-arceos-你的GitHub登录名
```

进入本地仓库。保持在默认的 `main` 分支完成实验，环境与课程说明见 [2026s 原始文档](UPSTREAM-2026s.md)。

## 3. 提交实验

使用自己已经登录的 Git 客户端提交并 push 到 `main`。命令行示例：

```sh
git add 你修改的实验文件
git commit -m "Complete an exercise"
git push origin main
```

依次暂存指定实验文件、记录提交、推送到分配仓库的 `main`。Git 的 push 仍需使用自己的 GitHub 账号授权；这与课程上传 Token 无关。可以直接用已登录的 GitHub Desktop 或编辑器完成相同步骤。

## 4. 查看评测与成绩

每次 push 自动触发配置检查和正式评测。打开 Actions，查看各练习原始日志与分数。只有自己账号触发的运行会上传自己的成绩；维护者代推只测试。

总分 600，上传本次完整评测的实际得分。未完成的模板出现测试失败属于预期。环境安装失败或运行被取消时不会上传不完整结果。

上传成功日志为 `OpenCamp accepted the score (result=1).`。若接口拒绝，先确认自己加入本阶段训练营、绑定同一个 GitHub 账号，再把脱敏错误交给维护者。修复后可在 GitHub Actions 重跑工作流。学员不需要添加任何课程 Secret。
