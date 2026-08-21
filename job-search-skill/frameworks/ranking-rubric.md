# Job Ranking Rubric

只对快速筛选前 10 个岗位做深度评分。评分依据是「完整 JD 中的要求」对「用户简历中的证据」，不是 title 或关键词相似度。

## 1 · 拆解要求

从每份 JD 提取：

- Must Have：不满足会显著降低拿面概率的 3-7 条要求
- Nice to Have：加分但通常不构成门槛的要求
- Hidden Signals：ownership、0→1、enterprise、ambiguity、craft、technical depth 等工作方式信号
- Hard Gates：地点、工作授权、证照、语言、on-call、出差等明确门槛

JD 没写的要求不得自行补入。推断出来的信号必须标为「推断」。

## 2 · 单条证据评分

每条要求按简历事实打分：

- `1.0` 直接命中：简历有具体项目/职责，并有规模、结果或可验证细节
- `0.5` 相邻命中：领域相邻、角色深度不足，或只有 claim 没有细节
- `0.0` 未命中：简历没有证据

只看用户给出的简历。不要因为种子 JD 提到某项能力，就假定用户具备它。

## 3 · 总分区间

```text
Base = 0.60 × MustHave + 0.20 × NiceToHave + 0.20 × HiddenSignalFit
```

先按公式算中心值，再给 ±5-8 个百分点的区间。最终显示如 `72-82%`，不要显示 `77.3%`。

上限规则：

- 1 条 Must Have 为 `0`：上限 75%
- 2 条及以上 Must Have 为 `0`：上限 55%
- 任一 Hard Gate 失败：直接 Skip，不进入 Tier A/B
- 完整 JD 不可见：上限 69%，标 `Description unavailable`

## 4 · 新鲜度只作排序，不伪装成匹配

深度匹配分不包含发布时间。两个匹配区间相近的岗位，按以下顺序排序：

1. 发布时间更近
2. Must Have 直接证据更多
3. 风险更少
4. 更符合用户公司/工作方式偏好

这能避免一个刚发布但明显不匹配的岗位仅凭「新」冲到前面。

## 5 · 输出证据

每个入选岗位都输出：

- `Why it fits`：引用 2 条简历事实，不能只复述 JD
- `Main risk`：招聘经理最可能质疑的一点
- `Missing evidence`：简历中看不出的关键要求；没有则写 `None found`
- `Next step`：Apply / Referral first / Deep decode / Portfolio first

不确定的信息写 `Unknown`，不要补全公司规模、薪资、签证政策或岗位状态。