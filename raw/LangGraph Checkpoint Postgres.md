---
title: "DeepSeek"
source: "https://chat.deepseek.com/a/chat/s/e658473f-fe6b-4fd7-af20-9c0cb02be137"
author:
published:
created: 2026-04-18
description: "Chat with DeepSeek AI – your intelligent assistant for coding, content creation, file reading, and more. Upload documents, engage in long-context conversations, and get expert help in AI, natural language processing, and beyond. | 深度求索（DeepSeek）助力编程代码开发、创意写作、文件处理等任务，支持文件上传及长文本对话，随时为您提供高效的AI支持。"
tags:
  - "clippings"
---
关于LangGraph的PostgreSQL实现（PGSaver / PGStore），目前主要有官方实现和一个社区复刻版。

### 📦 官方实现：LangGraph Checkpoint Postgres

这是由LangChain官方维护的实现，是目前最主流且稳定的选择，位于 `langchain-ai/langgraph` 仓库下。

- **功能** ：它提供了一个 `langgraph-checkpoint-postgres` 包，其中包含了将LangGraph状态持久化到PostgreSQL数据库的 `PostgresSaver` （同步）和 `AsyncPostgresSaver` （异步）类。
- **Python版本** ：该包在PyPI上发布，可通过 `pip install langgraph-checkpoint-postgres` 安装 [30](https://pypi.org/project/langgraph-checkpoint-postgres/1.0.6/) 。
	- **示例代码** ：
		```
		from langgraph.checkpoint.postgres import PostgresSaver
		DB_URI = "postgres://user:pass@localhost:5432/db"
		with PostgresSaver.from_conn_string(DB_URI) as checkpointer:
		    # 首次使用需调用.setup()创建表
		    checkpointer.setup()
		    # 将checkpointer传入你的Graph
		    # graph = builder.compile(checkpointer=checkpointer)
		```
		[30](https://pypi.org/project/langgraph-checkpoint-postgres/1.0.6/)
- **JavaScript/TypeScript版本** ：也有对应的npm包 `@langchain/langgraph-checkpoint-postgres` 。
	- **示例代码** ：
		```
		import { PostgresSaver } from "@langchain/langgraph-checkpoint-postgres";
		const checkpointer = await PostgresSaver.fromConnString(
		  "postgres://user:pass@localhost:5432/db"
		);
		// 首次使用需调用.setup()
		await checkpointer.setup();
		```
- **Store (存储) 支持** ：官方实现还提供了用于长期记忆存储的 `PostgresStore` 和 `AsyncPostgresStore` [13](https://deepwiki.com/langchain-ai/langgraph/4.3-store-system) 。它支持向量搜索，需要PostgreSQL的 `pgvector` 扩展。

### 👤 社区复刻版

除了官方版本，也有一个社区版本，可作为参考或备选。

- **项目** ： `baudm/langgraph-checkpoint-postgres`
- **描述** ：这是一个对官方PostgreSQL Saver的复刻（Fork），同样使用Python编写 [8](https://github.com/baudm/langgraph-checkpoint-postgres) 。项目的关注度不高（3个Star，1个Watch，0个Fork） [8](https://github.com/baudm/langgraph-checkpoint-postgres) 。

### 💡 关键特性与注意事项

| 特性 | 官方实现 (`langgraph-checkpoint-postgres`) |
| --- | --- |
| **生产就绪** | 是，为LangGraph Cloud优化，官方维护 |
| **核心功能** | `PostgresSaver` / `AsyncPostgresSaver` |
| **轻量级选项** | 提供 `shallow` 版（仅保存最新状态，不支持时间旅行） [43](https://reference.langchain.com/python/langgraph.checkpoint.postgres/shallow) |
| **Store支持** | 支持，提供 `PostgresStore` / `AsyncPostgresStore` |
| **并发支持** | 支持，官方实现提供异步版本（如 `AsyncPostgresSaver` ） |
| **清理/删除** | 无原生API，需手动执行SQL或通过第三方库处理 [33](https://github.com/langchain-ai/langgraphjs/issues/1138) [34](https://github.com/langchain-ai/langgraphjs/issues/1272) |

### 🔍 如何获取更多信息

- **官方文档与源码** ：
	- **GitHub 主仓库** ： [`langchain-ai/langgraph`](https://github.com/langchain-ai/langgraph)
		- **Checkpoint Postgres 模块源码路径** ： `libs/checkpoint-postgres/`
		- **Store 实现源码** ： `libs/checkpoint-postgres/langgraph/store/postgres/` [13](https://deepwiki.com/langchain-ai/langgraph/4.3-store-system)
		- **PyPI 项目页** ： [`langgraph-checkpoint-postgres`](https://pypi.org/project/langgraph-checkpoint-postgres/) [30](https://pypi.org/project/langgraph-checkpoint-postgres/1.0.6/)
- **官方教程** ：
	- Python 持久化指南： [How to add persistence ("memory") to your graph](https://langchain-ai.github.io/langgraph/how-tos/persistence_postgres/) [30](https://pypi.org/project/langgraph-checkpoint-postgres/1.0.6/)
		- JavaScript 持久化指南： [How to add persistence ("memory") to your graph](https://langchain-ai.github.io/langgraphjs/how-tos/persistence_postgres/) [30](https://pypi.org/project/langgraph-checkpoint-postgres/1.0.6/)
- **相关讨论与问题** ：
	- 关于Postgres Checkpointer的讨论可见： [Postgres memory on a MultiAgent](https://github.com/langchain-ai/langgraph/discussions/1881) [11](https://github.com/langchain-ai/langgraph/discussions/1881)
		- 遇到问题可查阅GitHub Issues，例如 `AsyncPostgresSaver` 的连接池问题或PostgreSQL连接管理问题。

