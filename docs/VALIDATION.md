# 2026f 课程 2078 验证记录

来源：[LearningOS 2026s 课程仓库](https://github.com/LearningOS/2026s-oscamp-professional-2026s-arceos-arceos-classroom-2026s-arceos-oscamp)，提交 `85237911b8fb71ac94d7a7c51597ebec6b73e939`。

## 真实 CI 与成绩上传

2026-09-14（北京时间），学员仓库 [2026f-arceos-Alayfolk64](https://github.com/2026f-autotest/2026f-arceos-Alayfolk64) 的真实 push 触发[运行 34776283016](https://github.com/2026f-autotest/2026f-arceos-Alayfolk64/actions/runs/34776283016)，被测提交 `8e5255fa2438598d2849a1a95e1034077fcc24ad`。

- 环境准备成功，六项练习全部形成真实结果，实测 **0/600，0/6 通过**。
- `print_with_color` 已构建运行，但模板未实现彩色输出；`ramfs_rename` 尚未实现重命名；`alt_alloc` 停在分配器 `todo!()`；`support_hashmap` 因未提供 `HashMap` 编译失败；`sys_map` 尚未实现 `sys_mmap`；`simple_hv` 尚未处理客户机特权指令。
- 测试作业最终失败表示实验未完成。独立的 **Save measured score and upload to OpenCamp** 作业成功，真实日志为：

```text
Course 2078: 0/600 points; 0/6 exercises passed.
Submitting measured score: course=2078, student=Alayfolk64, score=0/600
OpenCamp accepted the score (result=1).
```

- 六项结果及原始日志保存在该运行附件；实际总分保存在学员仓库 `gh-pages:course-2078.json`。
- [配置检查 34776283037](https://github.com/2026f-autotest/2026f-arceos-Alayfolk64/actions/runs/34776283037) 成功，验证 `STUDENT_GITHUB` 与组织 Secret 的共享读取。配置检查本身不上传成绩。

## 已修复的环境问题

初次真实 CI [34775639911](https://github.com/2026f-autotest/2026f-arceos/actions/runs/34775639911) 和后续 [34775933206](https://github.com/2026f-autotest/2026f-arceos-Alayfolk64/actions/runs/34775933206) 在依赖准备阶段失败，分别解析 `dw_apb_uart 0.1.2`、`0.1.1` 时报告 `feature edition2024 is required`。这些版本使用了旧 Cargo 不支持的 resolver。

现已提交 `arceos/Cargo.lock`，固定 `dw_apb_uart 0.1.0`、`indexmap 2.6.0`，CI 使用 `cargo fetch --locked`。本地原版 `nightly-2024-09-04` 的依赖下载退出 0，随后上述真实 Linux CI 完成评测和上传。实验源码和题目保持与上游一致；源码目录唯一新增文件为依赖锁文件。

## 验证范围

16 项本地脚本测试通过，覆盖身份、结果完整性、分值、退出状态和上传错误处理；它们与上述真实 CI 分开记录。未把模板改成参考答案，也没有声称满分用例已经通过。

已只读核对 [OpenCamp 秋冬季项目先导阶段](https://opencamp.cn/os2edu/camp/2026fall/stage/6) 的公开课程数据，课程编号为 2078。排行榜的登录态实际行显示仍待核验；接口接受结果已经验证。未修改 OpenCamp 后台。

自助领取入口位于 [2026f-autotest/enroll](https://github.com/2026f-autotest/enroll)，当前入口代码已部署，跨仓库建仓凭证待配置。
