# 2026f 项目先导阶段 — 组件化操作系统

基于 [LearningOS 2026s 课程仓库](https://github.com/LearningOS/2026s-oscamp-professional-2026s-arceos-arceos-classroom-2026s-arceos-oscamp)，由 [2026f-autotest](https://github.com/2026f-autotest) 统一分配学员仓库、运行真实测试并上传 OpenCamp。

**课程编号：2078 · 6 项练习 · 总分：600**

## 学员提交流程

1. 在 OpenCamp 加入本阶段训练营，绑定自己的 GitHub 登录账号。
2. 点击[领取作业仓库](https://github.com/2026f-autotest/enroll/issues/new?template=enroll.yml)，选择课程 **2078** 并提交申请；等待机器人回复，然后接受仓库邀请。
3. 克隆分配的仓库，在 `main` 完成实验并 push。
4. 在 Actions 查看各项测试、原始日志、分数和上传结果，再核对 OpenCamp 学员成绩页面。

**学员无需 Fork、安装 GitHub CLI 或填写课程 Token。** 身份由领取程序自动绑定，Token 由组织 Secret 共享。

详细步骤见[学员指南](docs/STUDENT_GUIDE.md)。维护者见[建仓与维护流程](docs/MAINTAINER.md)。

## 计分规则

沿用往期各项练习的权重，每项全部通过才获得该项分数。每次提交重新计算全部练习，上传本次实际总分；不是按提交次数累加。部分完成也会上传测得的分数。编译或测试未通过、超时的练习记 0 分；环境准备失败、缺少结果或结果不完整时不上传。

| 练习 | 分值 |
| --- | ---: |
| `print_with_color` | 100 |
| `ramfs_rename` | 100 |
| `alt_alloc` | 100 |
| `support_hashmap` | 100 |
| `sys_map` | 100 |
| `simple_hv` | 100 |

Actions 中测试作业变红表示还有未完成练习；单独的 **Save measured score and upload to OpenCamp** 作业显示成绩同步是否成功。日志出现 `OpenCamp accepted the score (result=1).` 才表示接口接受成绩。

成绩明细同时保存在运行附件和学员仓库的 `gh-pages:course-2078.json`，无需启用 GitHub Pages。

## 文档与来源

- [学员指南](docs/STUDENT_GUIDE.md)
- [维护流程](docs/MAINTAINER.md)
- [验证记录](docs/VALIDATION.md)
- [2026s 上游原始说明](docs/UPSTREAM-2026s.md)

上游源码提交：`85237911b8fb71ac94d7a7c51597ebec6b73e939`。保留原有实验源码、练习题和许可证。
