# 🌏 DevOps 路线图 —— 去行话化的入门指南

[English](./README.md) | [中文](./README.zh.md)

> **目标：** 构建、部署并维护任何项目，而不会被基础设施或 DevOps 的复杂性卡住。

---

## 🧭 为什么要做这个项目

我在学习 DevOps 工具时最大的困难不是“不会用”，而是**不理解这些名词在说什么**。  
很多英文术语语义模糊、含义抽象、甚至自相矛盾。第一次遇到 **JSON**、**Container**、**Kubernetes** 这些词时，我完全懵了。

这些词让我大脑直接宕机。  
后来我才明白，很多工程师在发明工具时随口造了个词，对他们有意义，但对新人却毫无帮助。  
比如：
- “Kubernetes” 是什么？  
- “Pod”、“Ingress”、“Helm”、“Daemonset”——为什么都像神话？  
- “Container” 到底装的是什么？  

所以我决定做一个仓库，用来**梳理（de-jargonify）**整个 DevOps 体系，从语义上理解每个概念，而不是死记定义。  

每一个概念我都会讲清楚：
- 它的字面含义（semantic meaning）  
- 它的真实作用（why it exists）  
- 以及何时真正需要用到它  

目标是：让像我一样被“英文行话”困扰的人也能彻底看懂 DevOps。

---

## 🧱 这个仓库包含什么

这是一个**多章节的 DevOps 学习路线图**，就像一本你能“照抄照用”的基础设施手册。

每一页介绍 DevOps 的一个层面，从本地开发环境到上线运维。

| 层级 | 主题 | 内容简介 | 链接 |
|------|------|-----------|------|
| 🧩 **基础概念** | [00_intro.md](./docs/zh/00_intro.md) | 讲清楚 DevOps 是什么，以及它的整体逻辑 |
| 🖥️ **本地开发环境** | [01_local_dev.md](./docs/zh/01_local_dev.md) | 学会在本地运行项目（Docker、Compose、Makefile） |
| ☁️ **基础设施层** | [02_infrastructure.md](./docs/zh/02_infrastructure.md) | 服务器、虚拟机与基础设施即代码（Terraform、Ansible） |
| 🚀 **持续集成 / 持续部署** | [03_cicd.md](./docs/zh/03_cicd.md) | 自动化测试与部署（GitHub Actions、GitLab CI） |
| 📦 **容器化** | [04_containers.md](./docs/zh/04_containers.md) | 容器到底是什么，Docker 又为什么存在 |
| 🧭 **编排系统** | [05_kubernetes.md](./docs/zh/05_kubernetes.md) | Kubernetes 去行话化讲解：Pod、Node、Service、Ingress |
| 🔐 **配置与密钥管理** | [06_secrets.md](./docs/zh/06_secrets.md) | 如何安全地管理密码、密钥和环境变量 |
| 📈 **监控与日志** | [07_monitoring.md](./docs/zh/07_monitoring.md) | 观察系统健康状况：Prometheus、Grafana、ELK |
| ⚙️ **自动化脚本** | [08_scripts.md](./docs/zh/08_scripts.md) | Shell / Makefile 脚本模板与说明 |
| 🧰 **DevOps 工具索引** | [09_tool_index.md](./docs/zh/09_tool_index.md) | 工具名称语义解释大全 |
| 🌐 **示例项目** | [10_examples.md](./docs/zh/10_examples.md) | Node + Postgres、Flask + Redis 等项目模板 |

---

## 📚 如何使用

1. 找到你卡住的主题，比如 “Kubernetes”。  
2. 打开对应文档，看“语义解释 + 实际用途”。  
3. 在 `templates/` 里复制可用的配置模板。  
4. 修改 `.env` 后运行 `make deploy` 或相关脚本。  
5. 一边运行一边理解背后的逻辑。

---

## 🔍 编写原则

- **去行话化（De-jargonify）：** 所有工具先讲“意图”，再讲“实现”。  
- **由浅入深（Bottom-up）：** 从本地 → 基础设施 → 自动化 → 编排系统。  
- **可复制（Reusable）：** 每个目录都带模板，直接可用。  
- **场景驱动（Practical）：** 不空谈定义，只讲“什么时候该用”。  

---

## 🗺️ 全局流程图
其实整个 DevOps / IT 层的世界，可以拆成五块：

开发与构建层（Build）
👉 工具：Git, GitHub Actions, Jenkins, CI/CD
👉 核心思想：版本控制 + 自动化测试 + 构建产物

打包与运行层（Run）
👉 工具：Docker, Containerd, Kubernetes
👉 核心思想：隔离、调度、资源管理

监控与通信层（Connect）
👉 工具：Webhook, WSS, SSE, gRPC, REST
👉 核心思想：事件通知 + 数据流动 + 实时反馈

基础设施层（Infra）
👉 工具：AWS, Terraform, Ansible
👉 核心思想：虚拟化 + 自动化配置 + 权限与安全

可观测与稳定层（Observe）
👉 工具：Prometheus, Grafana, ELK
👉 核心思想：日志、指标、报警、可视化反馈
