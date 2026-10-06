# 证据与归纳

目录：证据分层 → Review 直接证据（R1–R6）→ 本人发起/整合的代码（C1–C3）→ 归纳与限制

截至 2026-10-06 读取公开 GitHub 资料。只讨论可见的工程作品和技术反馈，不推断私人工作方式、性格、投入时长或全部能力。样本支持可迁移方法，不代表 Daniel 的完整、永久偏好。

## 证据分层

- 直接证据：账号 `danielfbm` 的具体 review 评论及回复
- 代码观察：由该账号发起/署名/整合的 PR 最终可见 patch；不等于每行本人手写，且可能有协作者或 AI 辅助
- 本技能建议：由上述证据归纳的实现/review 流程、严重度模板和教学示例，不是本人原话或强制规范
- 不采用：仅有批准/LGTM 的样本、别人的评论、机器人的自述、仅靠 PR 标题/描述猜测代码风格

同一 PR 的多轮意见是一个上下文，不能当作多个独立跨项目样本。以下摘录均为中文概括而非长篇转录。

## Review 直接证据

### R1：追到 diff 外的旧行为

- 来源：[tektoncd/cli #2889 评论](https://github.com/tektoncd/cli/pull/2889#discussion_r3666536333)
- 作者：danielfbm；日期：2026-07-28 14:46:45 UTC
- 观察：沿旧排序路径指出普通流水线日志顺序可能回归，给出双任务对照、修复位置与回归测试方向
- 归纳：审新功能时检查旧保证和消费者；用可区分的输入证明影响
- 限定：同 PR 正式 review 状态为 COMMENTED；文字里的 BLOCKER 不能转述为 GitHub REQUEST_CHANGES，也不授权自动操作状态

### R2：检查测试是否真正能抓错

- 来源：[tektoncd/cli #2889 测试评审](https://github.com/tektoncd/cli/pull/2889#discussion_r3480735886)
- 作者：danielfbm；日期：2026-06-26 10:24:24 UTC
- 观察：质疑覆盖是否有效；该 PR 多轮意见涉及非零 retry、多个任务、相同时间戳，以及恢复旧错误时测试能否失败
- 归纳：测试必须区分正确/错误行为；相关输入的辨别力比测试数量更重要
- 限定：已读最终 patch 中排序修复、same_start_time 与非零 retry 断言，不声称本技能制作时运行过该项目测试；评论中的复现次数只是作者自述

### R3：删除无必要复杂度，允许延期扩展

- 来源：[AlaudaDevops/run-actions #36 必要性提问](https://github.com/AlaudaDevops/run-actions/pull/36#discussion_r2995208709)，[作者确认遗漏](https://github.com/AlaudaDevops/run-actions/pull/36#discussion_r2995970371)
- 本人评论日期：2026-03-26 14:09:01 UTC
- 观察：问正常安装 skill 后为何仍需额外提示；作者确认已无必要。另提出可使用输出文件简化数字结果交付的方向
- 延期证据：[pr-cli 扩展建议](https://github.com/AlaudaDevops/run-actions/pull/36#discussion_r2995231085)，[作者明确留待以后](https://github.com/AlaudaDevops/run-actions/pull/36#discussion_r2998762701)
- 正式 review：2026-03-26 [CHANGES_REQUESTED](https://github.com/AlaudaDevops/run-actions/pull/36#pullrequestreview-4014475144)，2026-03-27 [APPROVED](https://github.com/AlaudaDevops/run-actions/pull/36#pullrequestreview-4018363556)
- 归纳：先问必要性；区分当前验收条件和可后续讨论的扩展，不能归纳为“所有建议都完成才批准”

### R4：公共默认值与环境差异分离

- 来源：[AlaudaDevops/toolbox #7](https://github.com/AlaudaDevops/toolbox/pull/7#discussion_r2043480484)
- 作者：danielfbm；日期：2025-04-15 03:32:22 UTC
- 观察：要求公共镜像作为默认值，内网镜像由流水线/配置注入；最终 diff 增加 BUILDER_IMAGE/BASE_IMAGE 参数并由流水线传入环境值
- 归纳：验证默认值能服务目标用户，将部署环境差异留给配置或调用端；不推导为禁止所有私有镜像
- 交叉印证：[toolbox #67 参数化意见](https://github.com/AlaudaDevops/toolbox/pull/67#discussion_r2321181306)；此补充仅支持同一方向，不据此新增更强规则

### R5：让测试进入持续验证路径

- 来源：[AlaudaDevops/toolbox #25 本人要求](https://github.com/AlaudaDevops/toolbox/pull/25#issuecomment-3026133183)
- 作者：danielfbm；日期：2025-07-02 02:25:43 UTC
- 观察：要求 kube-bench-report 单测在 PR 和 main 更新时自动执行；最终 workflow 针对 main 的 PR/push 且相关目录变化触发
- 归纳：确认改动相关测试有适当 CI 入口，不能说仓库所有 PR 都必须执行全部测试
- 限定：PR 作者是 Copilot，[创建 workflow 的回复](https://github.com/AlaudaDevops/toolbox/pull/25#issuecomment-3026137675)属于机器人，不是 Daniel 的亲写实现，也不是本次 CI 执行结果

### R6：保留自我反思，不模仿缺点

- 来源：[tektoncd/cli #2889 后续说明](https://github.com/tektoncd/cli/pull/2889#issuecomment-5112278106)
- 作者：danielfbm；日期：2026-07-29 02:58:01 UTC
- 观察：本人承认重要反馈提出较晚
- 本技能建议：较早做行为/风险判断，但仍以查证为准；“晚提 blocker”不是要复制的习惯

## 本人发起/整合的代码观察

以下三个仓库已核对为 public，读取了实际 PR patch、关键文件及 commit 元数据；没有运行这些项目的测试。优先使用固定 commit 对应的最终实现，而非可能过时的 PR 说明。

### C1：子 Pipeline 结果传播

- [danielfbm/pipeline #8](https://github.com/danielfbm/pipeline/pull/8)；[固定 commit/diff](https://github.com/danielfbm/pipeline/commit/c4d51c0b2b190d4f3bb8474bacf0486a9c96aefc)
- 日期：PR 2026-06-11 创建；patch author date 2026-07-28；commit 提交元数据日期 2026-09-26。三者含义不同。核验时为 open 的个人 fork PR，不能说已被上游接受或发布
- 归因：PR user / commit author 为 danielfbm，committer 为 claude；仅支持“Daniel 署名、提交和整合”，不支持纯手写断言
- 实现：按 TaskRun/CustomRun/ChildPipelineRun 选择不同结果查找，随后共享缺失结果校验；保留成功缺失与失败状态的错误区别。[校验路径](https://github.com/danielfbm/pipeline/blob/c4d51c0b2b190d4f3bb8474bacf0486a9c96aefc/pkg/reconciler/pipelinerun/resources/pipelinerunresolution.go#L1042-L1089)
- 实现：将已完成的 child 结果转换为现有 TaskRunResult，并以合并 accessor 服务主协调器；包括失败但产出结果的 child，跳过未完成状态，保留类型和值。[结果聚合](https://github.com/danielfbm/pipeline/blob/c4d51c0b2b190d4f3bb8474bacf0486a9c96aefc/pkg/reconciler/pipelinerun/resources/pipelinerunstate.go#L206-L252)
- 测试：consumer 缺失结果用例移除 parent 自身的结果引用，避免另一个失败路径掩盖目标问题，并断言 consumer TaskRun 没有被创建；parent 结果缺失另测。helper 用例区分空、缺失、running、failed、string/array/object；reconciler 与 e2e 检查不同边界
- 交付：实现同附文档和两个可执行 YAML 示例，明确保留 matrix 等既有独立限制
- 归纳：先适配既有语义路径，保留来源/错误契约；用隔离失败原因的测试验证真实副作用。该 PR 为 18 文件、+2090/-202，不能推导“只允许小 PR”

### C2：非默认 ServiceAccount 继承测试

- [tektoncd/pipeline #10206](https://github.com/tektoncd/pipeline/pull/10206)；[固定 commit/diff](https://github.com/tektoncd/pipeline/commit/4bdbd0e1669f026ae43929a4025e6b1c3e79204d)
- 日期：2026-06-06 创建，2026-07-07 合并；patch author date 2026-07-04，提交元数据日期 2026-07-06
- 归因：danielfbm 提交；commit 明示 Assisted-By Claude。只读代码观察，不认定每行亲写
- 最终实现：新增小型 WithServiceAccount fixture decorator，复用统一 params/workspaces fixture，删除几个大段近似 fixture。测试用非默认 pinp-sa，避免不发生继承也因 default 相等而通过
- 最终实现：既有 assertPinP 仅对空/default 的预期值忽略 ServiceAccountName，指定非默认值时纳入 full-spec diff。[helper 与测试](https://github.com/tektoncd/pipeline/blob/4bdbd0e1669f026ae43929a4025e6b1c3e79204d/test/pipelinerun_pinp_test.go#L181-L194)，[e2e 范围](https://github.com/tektoncd/pipeline/blob/4bdbd0e1669f026ae43929a4025e6b1c3e79204d/test/pipelinerun_pinp_test.go#L263-L302)
- 描述纠正：PR 正文仍说新增独立 fixture 并对 child PipelineRun/TaskRun/pod 三层直接断言，最终 diff 已改为复用 fixture、只新增 child PipelineRun 检验。代码说明下层由既有 serviceaccount_test.go 覆盖；本研究未独立验证该下层套件
- 归纳：用非默认值和有效比较排除假阳性；按变化边界补测试，不机械复制数据或三层断言。剩余测试仍有重叠，不能概括为“零重复”

### C3：Reporter wrapper 与输出过滤

- [danielfbm/tkn-act #50](https://github.com/danielfbm/tkn-act/pull/50)；[最终修正 commit/diff](https://github.com/danielfbm/tkn-act/commit/6fb351f3f19193c65a470e74faa2fac28d1ec7c8)
- 日期：2026-05-16 创建并合并，四个 commit 的 author date 均为当日
- 归因：danielfbm 提交，四个 commit 都明示 Co-Authored-By Claude；描述中的 review-subagent findings 不计为本人 review 发言
- 实现：filter 实现既有 Reporter 接口，以 early return 过滤并委托 Emit/Close；无过滤条件也可统一套 wrapper。边界事件、空 Task、空 Step 按各自语义保留。[最终 filter](https://github.com/danielfbm/tkn-act/blob/6fb351f3f19193c65a470e74faa2fac28d1ec7c8/internal/reporter/filters.go#L1-L75)
- 实现：在 setupRunPersistence 之前只包 live reporter，保留完整持久化流供 logs replay 再选择。[接线位置](https://github.com/danielfbm/tkn-act/blob/6fb351f3f19193c65a470e74faa2fac28d1ec7c8/cmd/tkn-act/run.go#L194-L242)
- 实现与测试：时间戳输出提成小 helper、复用 labelOf、不改 JSON 事件形状；内存 capture sink 验证过滤/边界/Close。最终修正 commit 补遗漏的过滤边界、help 和文档，不是初次实现就完美
- 归纳：在合适的接线边界加展示策略，保持生命周期与原始数据契约；修复发现后补窄回归测试，并同步实际行为与 help

## 从代码样本提炼的建议

这些是本技能的有限归纳：优先复用同义路径；保留真实契约；让测试能区别错误实现；检查状态/边界；按变化边界配置验证；以最终代码校正文档。adapter、wrapper、fixture decorator 只是适合这些样本的选择，不是每次任务必须使用的结构。

## 不能从这些样本推出的结论

不要宣称他固定偏爱某种缩进、命名后缀、面向对象/函数式范式、语言或框架；项目惯例仍优先。不要把单次实现升格为所有项目必须采用的架构。不要将公开代码风格分析用于判断私人特征、模仿身份或制造本人背书。
