<p align="right">
  <a href="./README.md">简体中文</a> | <a href="./README_EN.md">English</a>
</p>

<p align="center">
  <img src="./docs/images/diet-agent-hero.svg" alt="Diet Agent 项目横幅" width="100%" />
</p>

<h1 align="center">🥗 Diet Agent</h1>

<p align="center">
  <strong>基于多 Agent 的智能饮食推荐系统</strong>
</p>

<p align="center">
  理解用户需求，必要时主动追问，再从餐食库中给出可解释的推荐。
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Java-21-ED8B00?logo=openjdk&logoColor=white" alt="Java 21" />
  <img src="https://img.shields.io/badge/Spring%20Boot-3.3.13-6DB33F?logo=springboot&logoColor=white" alt="Spring Boot" />
  <img src="https://img.shields.io/badge/AgentScope-1.0.11-7257FA" alt="AgentScope" />
  <img src="https://img.shields.io/badge/MySQL-8.0.17%2B-4479A1?logo=mysql&logoColor=white" alt="MySQL" />
  <img src="https://img.shields.io/badge/Qwen-qwen--max%20%7C%20qwen--turbo-615CED" alt="Qwen" />
</p>

---

## 📖 项目简介

Diet Agent 是一个面向日常饮食场景的多 Agent 推荐系统。

用户可以直接输入：

> 今晚想吃清淡一点、适合减脂的高蛋白晚餐。

系统会识别餐次、口味、健康目标和用餐场景等信息；如果条件不足，会先向用户追问，再从个人餐食库或公共餐食库中检索并推荐合适的餐食。

```text
用户输入
  → 意图识别与槽位提取
  → 信息完整性判断
  → 主动澄清
  → 餐食检索与排序
  → 生成推荐理由
  → 健康风险检查
  → 返回推荐结果并保存 Trace
```

---

## ✨ 主要功能

- 🧠 **自然语言理解**：识别餐次、心情、场景、健康目标、菜系、口味和便利性。
- 🙋 **主动澄清**：信息不足时先追问，而不是直接生成模糊推荐。
- 🗂️ **双餐食库**：支持个人餐食库 `PERSONAL` 和公共餐食库 `PUBLIC`。
- ⚖️ **候选排序**：根据七类标签计算匹配度，并支持“换一批”。
- 🛡️ **风险守卫**：拦截医疗承诺、极端节食等高风险内容。
- 🔎 **链路追踪**：记录意图、槽位、候选、耗时和模型结果，便于调试与评估。

---

项目将自然语言理解和回复生成交给 LLM，将澄清判断、检索、排序、状态管理和风险兜底交给确定性代码，使推荐流程更加稳定、可解释。

---

## 🛠️ 技术栈

| 技术 | 用途 |
|---|---|
| Java 21 | 核心业务与 Agent 编排 |
| Spring Boot 3.3.13 | REST API 与静态页面托管 |
| AgentScope Java 1.0.11 | Agent 构建与模型调用 |
| Qwen Max / Turbo | 意图识别、澄清和推荐回复 |
| MyBatis 3.0.4 | 数据访问 |
| MySQL 8.0.17+ | 餐食、会话、消息和 Trace 持久化 |
| HTML / CSS / JavaScript | 内置 Web 前端 |
| Maven | 项目构建 |

---

## 🚀 快速开始

### 1. 准备环境

- JDK 21
- Maven 3.9+
- MySQL 8.0.17+
- DashScope API Key

### 2. 克隆项目

```bash
git clone https://github.com/lll965-ux/diet_agent.git
cd diet_agent
```

### 3. 初始化数据库

```bash
mysql -u root -p -e "CREATE DATABASE IF NOT EXISTS diet_db CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;"
mysql -u root -p diet_db < src/main/resources/db/diet_db.sql
```

> ⚠️ `diet_db.sql` 会删除并重建同名表，请勿直接用于已有数据或生产数据库。

### 4. 创建配置文件

Linux / macOS：

```bash
cp src/main/resources/application-example.yml src/main/resources/application.yml
```

Windows PowerShell：

```powershell
Copy-Item .\src\main\resources\application-example.yml `
  .\src\main\resources\application.yml
```

修改 `application.yml` 中的数据库密码和 DashScope API Key：

```yaml
spring:
  datasource:
    username: root
    password: your-mysql-password

agentscope:
  dashscope:
    api-key: your-dashscope-api-key
```

### 5. 启动项目

```bash
mvn spring-boot:run
```

访问：

```text
http://localhost:8080/
```

首次体验建议在聊天页切换到“公共库”，然后输入：

```text
晚饭推荐清淡低脂的，最好高蛋白。
```

---

## 📁 目录结构

```text
src/main/
├── java/com/diet/
│   ├── agent/          # Agent 构建与 Prompt 加载
│   ├── controller/     # REST API
│   ├── service/        # 编排、检索、推荐、风险和 Trace
│   ├── mapper/         # MyBatis Mapper
│   └── model/          # 请求、响应与状态模型
└── resources/
    ├── db/             # 数据库初始化脚本
    ├── diet/prompts/   # Agent Prompt
    ├── mapper/         # MyBatis XML
    └── static/         # Web 页面
```

---

<p align="center">
  <strong>🥗 让“今天吃什么”变得更简单。</strong>
</p>
