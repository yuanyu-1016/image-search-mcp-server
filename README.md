<div align="center">

# 🖼️ Image Search MCP Server

**基于 Model Context Protocol (MCP) 的图片智能检索服务器**

[![Java](https://img.shields.io/badge/Language-Java_100%25-blue.svg?style=for-the-badge&logo=java)](https://github.com/yuanyu-1016/image-search-mcp-server)
[![Maven](https://img.shields.io/badge/Build-Maven-C71A22.svg?style=for-the-badge&logo=apache-maven)](https://github.com/yuanyu-1016/image-search-mcp-server)
[![Architecture](https://img.shields.io/badge/Protocol-MCP-success.svg?style=for-the-badge)](https://github.com/yuanyu-1016/image-search-mcp-server)
[![Stars](https://img.shields.io/github/stars/yuanyu-1016/image-search-mcp-server?style=for-the-badge&color=yellow)](https://github.com/yuanyu-1016/image-search-mcp-server/stargazers)
[![Issues](https://img.shields.io/github/issues/yuanyu-1016/image-search-mcp-server?style=for-the-badge&color=red)](https://github.com/yuanyu-1016/image-search-mcp-server/issues)
[![License](https://img.shields.io/github/license/yuanyu-1016/image-search-mcp-server?style=for-the-badge&color=blue)](https://github.com/yuanyu-1016/image-search-mcp-server/blob/main/LICENSE)

[描述](#-描述) • [核心特性](#-核心特性) • [应用场景](#-应用场景) • [安装](#-安装) • [使用](#-使用) • [贡献](#-贡献) • [作者](#-作者)

</div>

---

## 📝 描述

**Image Search MCP Server** 是一个专为大语言模型 (LLMs) 和 AI Agent 打造的外部能力扩展服务。

本项目完整实现了 **Model Context Protocol (MCP)** 标准协议，将复杂的“图片搜索”、“以图搜图”或“图片元数据检索”能力封装成了标准化工具 (Tools)。任何支持 MCP 协议的智能体（如 Claude Desktop, 开源 Agent 框架等）都可以通过该服务器，打破纯文本对话的限制，使其能够理解用户的图像检索需求，并在其海量图库中精准“捞取”目标图片。

> 💡 **什么是 MCP？**
> MCP (模型上下文协议) 是一个开放标准，它允许开发者构建标准化的服务器，向大模型提供安全、可控的本地化数据源、业务 API 或执行工具。

---

## 🎯 核心特性

- **🔌 标准 MCP 协议对接**：开箱即用，支持直接接入任何兼容 MCP 协议的客户端，实现零成本的工具集成。
- **🔍 强大的图片检索能力**：将后端的图像搜索引擎（如基于向量的以图搜图、基于标签的语义搜索）通过标准化接口暴露给 LLM。
- **☕ 纯正的 Java 生态**：基于 Java 与 Maven 构建，易于与企业现有的 Spring Boot 后端、图像识别微服务或数据库进行集成。
- **🛡️ 权限与上下文隔离**：遵循 MCP 的安全设计规范，确保大模型仅能访问授权的图片资源和检索工具。

---

## 💡 应用场景

本服务可以极大拓展您的 AI Agent 应用能力，例如：

- **设计资源助手**：让 AI 帮您在企业图库中寻找“一张带有蓝天白云和科技感的背景图”。
- **电商导购智能体**：用户上传一张喜欢的衣服照片，AI 调用该 MCP 服务检索商城中相似的商品图片并返回。
- **个人相册管家**：通过自然语言描述，让大模型在海量个人相册库中精准定位某年某月的特定场景照片。

---

## ⚙️ 安装

本项目基于标准 Java Maven 工程构建。在开始之前，请确保您的环境已安装 **JDK 1.8+** (推荐 JDK 17) 和 **Maven 3.6+**。

### 获取项目

1. 克隆本仓库到本地环境：
   ```bash
   git clone [https://github.com/yuanyu-1016/image-search-mcp-server.git](https://github.com/yuanyu-1016/image-search-mcp-server.git)
   ```

2. 进入项目目录：
   ```bash
   cd image-search-mcp-server
   ```

3. 使用 Maven 导入并下载依赖：
   ```bash
   mvn clean install
   ```

---

## 🚀 使用

### 1. 配置图片检索引擎
打开 `src/main/resources` 下的配置文件，配置您的图片存储介质（如云端 OSS 或本地路径）以及搜索引擎参数（例如 ElasticSearch 节点或向量数据库 Milvus 的连接信息）。

### 2. 启动 MCP 服务器
执行项目的主启动类，或通过 Maven 命令启动：
```bash
mvn spring-boot:run
```
> *默认情况下，服务将在特定的端口上以 HTTP/SSE 或 stdio 流的方式提供 MCP 协议交互接口。*

### 3. 客户端对接
将该服务配置到您的 MCP 客户端中。以 Claude Desktop 为例，在 `claude_desktop_config.json` 中添加如下配置：

```json
{
  "mcpServers": {
    "image-search-mcp": {
      "command": "java",
      "args": ["-jar", "/path/to/your/image-search-mcp-server.jar"]
    }
  }
}
```
配置完成后重启客户端，大模型即可识别并调用您的图片搜索能力！

---

## 🤝 贡献

如果您对 MCP 协议落地或图像检索优化有好的想法，欢迎参与贡献：

1. Fork 本仓库。
2. 创建您的特性分支：`git checkout -b feature/AddVectorSearch`
3. 提交您的更改：`git commit -m 'Add Milvus vector search support'`
4. 推送至该分支：`git push origin feature/AddVectorSearch`
5. 开启一个 Pull Request (PR)。

---

## 👨‍💻 作者

**何元玉 (@yuanyu-1016)**

- **GitHub**: [https://github.com/yuanyu-1016](https://github.com/yuanyu-1016)
- **专注领域**: AI 应用开发开发、Java 研发、复杂系统架构设计

---

## 📄 认证

本项目采用 [MIT License](https://opensource.org/licenses/MIT) 进行开源认证。详细信息请参阅项目根目录下的 `LICENSE` 文件。

> **免责声明**：使用本项目的源码时，请遵循相关开源协议，保留原作者的版权声明。

---
<p align="center">
  <i>如果这个 MCP 服务器框架对您有帮助，请给一个 ⭐️ 鼓励一下！</i>
</p>
