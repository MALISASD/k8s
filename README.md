# k8s

## 项目现状
当前仓库是一个**初始化骨架仓库**，目前仅包含本 README 文件，尚未包含可运行代码、配置目录或自动化脚本。

## 给新人的快速说明
- 仓库目标（待补充）：建议明确这是学习型仓库、模板仓库，还是业务/平台项目。
- 代码结构（当前）：根目录只有 `README.md`，还没有 `src/`、`docs/`、`deploy/`、`scripts/` 等常见目录。
- 工程规范（待建立）：建议尽快补充分支规范、提交规范、代码评审与发布流程。

## 建议优先补齐的基础内容
1. **目录约定**
   - `docs/`：架构设计、运行手册、故障排查。
   - `manifests/` 或 `charts/`：Kubernetes 清单或 Helm Chart。
   - `scripts/`：本地开发、构建、测试、发布脚本。
   - `tests/`：单元测试与集成测试。
2. **开发与运行说明**
   - 本地依赖（如 kubectl、kind/minikube、helm、docker）。
   - 一键启动命令与示例。
   - 常见报错与处理方式。
3. **质量保障**
   - CI（lint/test/security scan）。
   - PR 模板与 CODEOWNERS。
   - 最小可用测试用例。

## 新人学习路径建议
1. 先熟悉 Kubernetes 基础对象：Pod、Deployment、Service、ConfigMap、Ingress。
2. 通过一个最小示例跑通“开发 -> 构建镜像 -> 部署 -> 观察日志 -> 回滚”的全流程。
3. 学会使用排障命令：`kubectl get/describe/logs/events`。
4. 再学习进阶主题：资源配额、健康检查、滚动升级、灰度发布与可观测性。
