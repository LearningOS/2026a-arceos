# 2026f 课程维护流程

| 配置 | 值 |
| --- | --- |
| 阶段 | 项目先导阶段 — 组件化操作系统 |
| 模板 | [2026f-autotest/2026f-arceos](https://github.com/2026f-autotest/2026f-arceos) |
| 课程编号 | 2078 |
| 总分 | 600 |
| 组织 Secret | `OSCAMP_2026F_ARCEOS_TOKEN` |
| 学员变量 | `STUDENT_GITHUB` |
| 学员仓库 | `2026f-autotest/2026f-arceos-GitHub登录名` |
| Rust 工具链 | `nightly-2024-09-04`，沿用 2026s |

## 1. 维护者配置一次

组织所有者创建公开模板并启用 Template repository。组织 Actions Secret 使用上表名称，访问范围为 Public repositories。课程编号、计分权重与来源记录在 `course.json`；学员身份由建仓脚本设置，不从提交作者名字推断。

自助入口为 [2026f-autotest/enroll](https://github.com/2026f-autotest/enroll)。建仓凭证 `ENROLL_GITHUB_TOKEN` 仅保存在该入口的仓库 Actions Secrets，学员仓库只继承本课程上传 Secret。当前配置和真实验证见[领取入口维护流程](https://github.com/2026f-autotest/enroll/blob/main/docs/MAINTAINER.md)。

## 2. 学员自助领取

学员点击课程 README 的领取链接，选课程 **2078** 并提交 Issue。Actions 从 `issue.user.login` 读取账号，复制本模板、设置 `STUDENT_GITHUB`、分配仓库写权限并触发配置检查；机器人回复仓库和邀请链接。助教无需收集名单或逐个运行建仓脚本。

配置完成后自动运行 **Check student configuration**，只检查身份和共享 Token 是否存在，不调用 OpenCamp。学员接受邀请后按[提交指南](STUDENT_GUIDE.md)开始实验。失败申请由维护者在领取入口的 Actions 输入原 Issue 编号重试，账号仍取原申请人。

初次生成模板仓库时，变量未设置的自动运行会跳过。若排队期间已经绑定身份，初次 push 也可能开始评测；上传仍要求触发账号等于学员账号。

## 3. 核对自动评测和上传

`main` 的 push 自动运行 `.github/workflows/build.yml`。测试作业只拿到只读仓库权限，不含课程 Token；评分脚本在 `.github/scripts/grade.py`，保留真实输出、退出状态与超时结果。

`.github/scripts/publish.py` 读取本次运行的结果附件，校验课程、仓库、提交、练习清单、权重与学员身份；将当前实际分数保存到 `gh-pages:course-2078.json` 后，调用固定 OpenCamp 成绩上传 API。只有 `result=1` 才视为成功，HTTP 或业务错误会明确失败。Token 只在上传步骤注入，不出现在源码或日志。

本阶段沿用往期部分得分规则：每次重新评测全部练习并上传当前总分。失败、回退代码可能使当前得分下降。新提交取消同仓库尚未完成的旧评测，以减少过时结果覆盖。

`arceos/Cargo.lock` 固定实际依赖，CI 只执行 `cargo fetch --locked`，不自动更新依赖。旧流程只固定 `indexmap=2.6.0`，会拉入不兼容旧 Cargo 的 `dw_apb_uart=0.1.2`（`0.1.1` 也不兼容）；本版固定为 `0.1.0`。镜像准备与测试保留原有启动头、FAT 文件路径和输出断言，由 Python 记录退出状态；使用 mtools 写入镜像，临时镜像和日志位于仓库 `tmp/`。

最终核对 Actions 上传作业及 OpenCamp 学员成绩页面；不需要登录或修改 OpenCamp 管理后台。

## 4. 更新模板

更新 `.github/`、`enroll.py`、`course.json` 或文档后，已分配的仓库不会自动收到模板更新。维护者只同步明确修改的公共文件，保留学员实验、报告和成绩。不要把学员答案合入课程模板。

## 真实验证

见[验证记录](VALIDATION.md)，区分静态检查、模拟接口测试、真实 CI 和 OpenCamp 接口接受结果。

## 本地应急建仓

保留 `enroll.py` 供维护者处理入口故障。维护者已经完成 GitHub CLI 登录时，在本课程目录执行 `python3 enroll.py 学员GitHub登录名`；不需要把课程 Token 传给脚本。日常使用上面的自助领取入口。
