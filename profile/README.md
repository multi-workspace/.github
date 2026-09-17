# multi-workspace

> **一切皆可组合，交付皆有 Workspace，仓库只承载所有权。**
>
> Everything composable · every delivery has a Workspace · repositories carry ownership only.

这里是 **Product Harness** 的机制层命名空间：用一组各自持有所有权的仓库，组合出可交付的多产品平台。

## 它要解决什么

把多个仓库拼成一个产品，难的从来不是写代码，而是三件事：

| 问题 | 表现 |
| --- | --- |
| **组合会漂移** | "我希望组合成什么"与"现在实际是什么"是两件事；没有唯一事实源，两边就各说各话 |
| **跨仓契约没有归属** | 契约同时被生产者和消费者依赖，放到任何一方都会让另一方被动 |
| **并行的人和 agent 没有共享状态** | 状态写在对话里、写在脑子里，一次上下文切换就归零 |

## 三条硬规矩

**1. 意图、观察、证据分开记，不许互相冒充**

| 载体 | 记什么 | 不声称什么 |
| --- | --- | --- |
| Manifest | 我希望组合成什么 | 不声称已经实现 |
| Lock | 我实际观察到哪个精确 SHA、什么摘要 | 不声称已经验证 |
| Release Bundle | 我验证过什么、证据在哪 | 不声称自己被包含在 Lock 里 |

**2. 模块只有一个 owner，组合根不写业务源码**

业务源码、领域契约、服务配置、部署实现、系统测试各自归属唯一的 Repository；组合根只承载治理、入口、Manifest / Lock、统一合同与组合检查。

**3. 机器可以提议，写操作必须由人放行**

提议 → 人工决策 → 一次性授权 → 执行回执。授权一次性、可过期、可回放；自动放行不是默认值。

## 组成

| 模块 | 角色 | 职责 |
| --- | --- | --- |
| `platform-contracts` | contract | 契约与架构正文 —— 唯一事实源 |
| `platform-control-plane` | runtime | 控制面：资源声明、plan / diff / apply |
| `platform-identity` | runtime | 身份、工作区令牌、主体绑定 |
| `platform-credential-store` | security | 凭证引用、轮换、撤销 |
| `platform-policy-approval` | runtime | 提议、审批与一次性授权 |
| `platform-gateway` | runtime | 能力入口、鉴权与路由 |
| `platform-agent-gateway` | runtime | Agent 接入面 |
| `platform-console` | ui | 管理台 |
| `platform-developer-tools` | developer-tools | CLI 与本地开发面 |
| `platform-operations` | operations | 部署、迁移、回滚 |
| `platform-testkit` | quality | 组合验收与质量门禁 |

## 现状

平台在自建 GitLab 上开发，**尚未开源**；本组织先作为对外入口与命名空间。

上面写的是已经在跑的规矩，不是路线图。架构正文、契约与验收证据目前不公开 —— 没有被验证过的东西，这里也不会说它已经完成。

---

对外品牌与身份见 **[github.com/wanweave](https://github.com/wanweave)**。
