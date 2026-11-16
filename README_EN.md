<p align="right">
  <a href="./README.md">简体中文</a> | <a href="./README_EN.md">English</a>
</p>

<p align="center">
  <img src="./docs/images/diet-agent-hero.svg" alt="Diet Agent project banner" width="100%" />
</p>

<h1 align="center">🥗 Diet Agent</h1>

<p align="center">
  <strong>A Multi-Agent Intelligent Meal Recommendation System</strong>
</p>

<p align="center">
  Understands what users want, asks follow-up questions when needed, and provides explainable recommendations from a meal library.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Java-21-ED8B00?logo=openjdk&logoColor=white" alt="Java 21" />
  <img src="https://img.shields.io/badge/Spring%20Boot-3.3.13-6DB33F?logo=springboot&logoColor=white" alt="Spring Boot" />
  <img src="https://img.shields.io/badge/AgentScope-1.0.11-7257FA" alt="AgentScope" />
  <img src="https://img.shields.io/badge/MySQL-8.0.17%2B-4479A1?logo=mysql&logoColor=white" alt="MySQL" />
  <img src="https://img.shields.io/badge/Qwen-qwen--max%20%7C%20qwen--turbo-615CED" alt="Qwen" />
</p>

---

## 📖 Overview

Diet Agent is a multi-agent recommendation system designed for everyday meal planning.

Users can simply enter a request such as:

> I want a light, high-protein dinner that is suitable for fat loss tonight.

The system identifies information such as meal type, taste preferences, health goals, and dining context. If important details are missing, it asks follow-up questions before retrieving and recommending suitable meals from either a personal or public meal library.

```text
User input
  → Intent recognition and slot extraction
  → Information completeness check
  → Proactive clarification
  → Meal retrieval and ranking
  → Recommendation explanation generation
  → Health risk check
  → Return recommendations and save the Trace
```

---

## ✨ Key Features

- 🧠 **Natural language understanding**: Recognizes meal type, mood, context, health goals, cuisine, taste, and convenience preferences.
- 🙋 **Proactive clarification**: Asks follow-up questions when information is incomplete instead of returning vague recommendations.
- 🗂️ **Two meal libraries**: Supports both a personal meal library (`PERSONAL`) and a public meal library (`PUBLIC`).
- ⚖️ **Candidate ranking**: Scores matches across seven categories and supports requesting another set of recommendations.
- 🛡️ **Risk guardrails**: Blocks medical promises, extreme dieting advice, and other high-risk content.
- 🔎 **End-to-end tracing**: Records intents, slots, candidates, latency, and model output for easier debugging and evaluation.

---

Diet Agent delegates natural language understanding and response generation to the LLM, while deterministic code handles clarification decisions, retrieval, ranking, state management, and risk control. This makes the recommendation workflow more stable and explainable.

---

## 🛠️ Tech Stack

| Technology | Purpose |
|---|---|
| Java 21 | Core business logic and agent orchestration |
| Spring Boot 3.3.13 | REST APIs and static web hosting |
| AgentScope Java 1.0.11 | Agent construction and model invocation |
| Qwen Max / Turbo | Intent recognition, clarification, and recommendation responses |
| MyBatis 3.0.4 | Data access |
| MySQL 8.0.17+ | Persistence for meals, sessions, messages, and traces |
| HTML / CSS / JavaScript | Built-in web frontend |
| Maven | Project build system |

---

## 🚀 Quick Start

### 1. Prerequisites

- JDK 21
- Maven 3.9+
- MySQL 8.0.17+
- DashScope API Key

### 2. Clone the Repository

```bash
git clone https://github.com/lll965-ux/diet_agent.git
cd diet_agent
```

### 3. Initialize the Database

```bash
mysql -u root -p -e "CREATE DATABASE IF NOT EXISTS diet_db CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;"
mysql -u root -p diet_db < src/main/resources/db/diet_db.sql
```

> ⚠️ `diet_db.sql` drops and recreates tables with the same names. Do not run it against an existing database containing important data or in production.

### 4. Create the Configuration File

Linux / macOS:

```bash
cp src/main/resources/application-example.yml src/main/resources/application.yml
```

Windows PowerShell:

```powershell
Copy-Item .\src\main\resources\application-example.yml `
  .\src\main\resources\application.yml
```

Update the database password and DashScope API Key in `application.yml`:

```yaml
spring:
  datasource:
    username: root
    password: your-mysql-password

agentscope:
  dashscope:
    api-key: your-dashscope-api-key
```

### 5. Run the Application

```bash
mvn spring-boot:run
```

Open:

```text
http://localhost:8080/
```

For your first try, switch to the **Public Library** on the chat page and enter:

```text
Recommend a light, low-fat, high-protein dinner.
```

---

## 📁 Project Structure

```text
src/main/
├── java/com/diet/
│   ├── agent/          # Agent construction and prompt loading
│   ├── controller/     # REST APIs
│   ├── service/        # Orchestration, retrieval, recommendations, risk control, and traces
│   ├── mapper/         # MyBatis mappers
│   └── model/          # Request, response, and state models
└── resources/
    ├── db/             # Database initialization scripts
    ├── diet/prompts/   # Agent prompts
    ├── mapper/         # MyBatis XML files
    └── static/         # Web pages
```

---

<p align="center">
  <strong>🥗 Making “What should I eat today?” easier to answer.</strong>
</p>
