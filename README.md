# k8s

> 面向新人：这份文档用于快速理解仓库结构、关键知识点与学习路径。

## 1. 仓库整体结构（当前状态）

当前仓库仍处于 **bootstrap（初始化）** 阶段，代码与目录尚未落地。

- 当前已有：`README.md`
- 当前缺失：业务代码、Kubernetes 清单、脚本、测试、CI 配置

这意味着：新人现在的重点不是“读实现”，而是先建立一个可运行、可测试、可协作的最小工程骨架。

---

## 2. 建议的标准目录结构（建议尽快建立）

```text
.
├── README.md
├── docs/                    # 设计文档、运行手册、故障排查
│   ├── architecture.md
│   ├── runbook.md
│   └── troubleshooting.md
├── manifests/               # 原生 Kubernetes YAML
│   ├── base/
│   └── overlays/
├── charts/                  # (可选) Helm Chart
├── scripts/                 # 本地开发、部署、回滚、检查脚本
│   ├── dev-up.sh
│   ├── deploy.sh
│   └── check.sh
├── tests/                   # 单元/集成/e2e 测试
├── .github/workflows/       # CI 流程
└── .gitignore
```

> `manifests/` 与 `charts/` 不一定同时需要：
> - 想要“显式、直接、易读”可优先 `manifests/`
> - 想要“模板化、参数化、多环境”可优先 `charts/`

---

## 3. 新人需要先掌握的关键内容

### 3.1 Kubernetes 基础对象（必须）
- **Pod**：最小运行单元。
- **Deployment**：无状态应用的声明式发布与滚动更新。
- **Service**：服务发现与访问入口（ClusterIP/NodePort/LoadBalancer）。
- **ConfigMap / Secret**：配置与敏感信息管理。
- **Ingress**：七层流量入口与路由。

### 3.2 交付链路（必须跑通一次）
1. 写应用（最小 HTTP 服务即可）
2. 构建镜像
3. 推送镜像仓库
4. 部署到集群
5. 验证访问
6. 看日志 + 定位错误
7. 回滚版本

### 3.3 排障能力（必须训练）
建议至少熟练以下命令：

```bash
kubectl get pods -A
kubectl describe pod <pod-name> -n <ns>
kubectl logs <pod-name> -n <ns>
kubectl get events -n <ns> --sort-by=.metadata.creationTimestamp
kubectl rollout status deployment/<name> -n <ns>
kubectl rollout undo deployment/<name> -n <ns>
```

---

## 4. 工程化与协作规范（建议在第一阶段补齐）

### 4.1 Git 与评审规范
- 分支命名：`feature/*`、`fix/*`、`docs/*`
- Commit 规范：`feat:`、`fix:`、`docs:`、`chore:`
- PR 模板：变更说明、影响范围、验证方式、回滚方案
- `CODEOWNERS`：明确评审责任人

### 4.2 质量门禁（CI）
至少包含：
- YAML/Chart lint
- 单元测试
- 镜像构建检查
- 安全扫描（依赖与镜像）

### 4.3 可观测性（尽早规划）
- 日志：结构化日志（JSON）
- 指标：QPS、错误率、延迟（RED）
- 健康检查：`readinessProbe`、`livenessProbe`

---

## 5. 给新人的 2 周学习建议（可执行）

### 第 1 周：打基础 + 跑通最小链路
- Day 1-2：理解 Pod / Deployment / Service
- Day 3：写一个最小服务并容器化
- Day 4：部署到本地集群（kind / minikube）
- Day 5：模拟故障并完成一次回滚

### 第 2 周：工程化 + 排障
- Day 1-2：补充脚本与文档（runbook/troubleshooting）
- Day 3：加入基础 CI（lint + test）
- Day 4：做一次容量/探针/资源限制配置
- Day 5：复盘：输出“部署与故障处理SOP”

---

## 6. 下一步落地清单（建议按优先级）

1. 创建目录骨架：`docs/`, `manifests/`, `scripts/`, `tests/`
2. 提交一个最小可运行示例（含 Deployment + Service）
3. 增加 `Makefile` 或脚本统一入口（如 `make deploy` / `make test`）
4. 增加 CI 工作流
5. 补齐架构图与运维手册

---

如果你是刚加入项目的同学，建议先从“第 1 周计划”执行，目标是 **一周内独立完成一次部署、排障、回滚**。
