# BurpGPT - AI 增强的 Burp Suite 安全扫描插件

## 项目简介

BurpGPT 是一个强大的 Burp Suite 扩展，利用 AI 技术检测传统扫描器可能遗漏的安全漏洞。通过将 Web 流量发送到 AI 模型进行分析，提供定制化的安全评估和智能漏洞识别。

**本版本基于原项目进行了重大改进和扩展，支持多种 AI 服务商和灵活的配置选项。**

## 🚀 主要修改内容

### 1. **多 AI 服务商支持**
- ✅ **支持 Moonshot API**：默认配置为 Moonshot Kimi 模型
- ✅ **支持 OpenAI API**：兼容原有 OpenAI 接口
- ✅ **支持其他兼容服务**：可配置任何符合 OpenAI API 格式的服务
- ✅ **支持本地部署模型**：可连接本地 LLM 服务

### 2. **灵活的配置系统**
- ✅ **可配置 Base URL**：支持自定义 API 端点
- ✅ **可配置模型名称**：不再局限于预定义模型列表
- ✅ **完全自定义**：API Key、模型、端点全部可配置

### 3. **API 格式兼容**
- ✅ **Chat Completions 支持**：适配现代 AI API 格式
- ✅ **自动格式检测**：根据 URL 自动选择合适的 API 格式
- ✅ **向后兼容**：保持对传统 Completions API 的支持

### 4. **主动扫描集成**
- ✅ **主动扫描支持**：BurpGPT 现在支持 "Do active scan" 功能
- ✅ **扫描类型区分**：清晰区分被动扫描和主动扫描结果
- ✅ **增强的错误处理**：更详细的日志和错误信息

### 5. **用户体验优化**
- ✅ **详细的调试日志**：便于问题排查
- ✅ **中文文档支持**：提供完整的中文使用说明
- ✅ **配置验证**：防止配置错误

## 📦 安装使用

### 系统要求

- **Java**: JDK 11 或更高版本
- **Burp Suite**: Professional 或 Community Edition (版本 >= 2023.3.2)
- **Gradle**: 6.9 或更高版本（用于构建）

### 快速开始

1. **下载插件**
   ```bash
   git clone https://github.com/Kento-Sec/BurpGPT.git
   cd BurpGPT
   ```

2. **构建插件**
   ```bash
   chmod +x gradlew
   ./gradlew clean shadowJar
   ```

3. **加载到 Burp Suite**
   - 打开 Burp Suite
   - 转到 `Extensions` → `Add`
   - 选择 `lib/build/libs/burpgpt-all.jar`

4. **配置插件**
   - 点击菜单栏 `BurpGPT`
   - 配置以下参数：
     - **API Key**: 你的 AI 服务商 API 密钥
     - **Base URL**: API 端点地址
     - **Model**: 模型名称
     - **Maximum prompt size**: 最大提示长度
     - **Prompt**: 自定义分析提示词

## ⚙️ 配置示例

### Moonshot API 配置
```
API Key: sk-your-moonshot-api-key
Base URL: https://api.moonshot.cn/v1/chat/completions
Model: moonshot-v1-8k
Maximum prompt size: 2048
```

### OpenAI API 配置
```
API Key: sk-your-openai-api-key
Base URL: https://api.openai.com/v1/chat/completions
Model: gpt-4o
Maximum prompt size: 4000
```

### 本地模型配置
```
API Key: your-local-api-key
Base URL: http://localhost:8080/v1/chat/completions
Model: llama3-8b
Maximum prompt size: 2048
```

## 🔧 支持的 AI 服务商

| 服务商 | Base URL | 支持的模型 |
|--------|----------|-----------|
| **Moonshot** | `https://api.moonshot.cn/v1/chat/completions` | moonshot-v1-8k, moonshot-v1-32k, moonshot-v1-128k |
| **OpenAI** | `https://api.openai.com/v1/chat/completions` | gpt-3.5-turbo, gpt-4, gpt-4o |
| **Azure OpenAI** | `https://your-resource.openai.azure.com/openai/deployments/your-deployment/chat/completions?api-version=2023-05-15` | 根据部署配置 |
| **本地部署** | `http://localhost:8080/v1/chat/completions` | 任何兼容模型 |

## 📊 功能特性

### 被动扫描增强
- 🔍 **实时分析**：自动分析所有通过 Burp 的 HTTP 流量
- 🧠 **智能识别**：AI 驱动的漏洞检测
- 📝 **详细报告**：生成结构化的安全分析报告

### 主动扫描集成
- ⚡ **深度分析**：对主动扫描的测试请求进行 AI 分析
- 🎯 **漏洞验证**：智能评估漏洞的真实性和可利用性
- 📈 **全面覆盖**：结合传统扫描和 AI 分析的优势

### AI 分析能力
- 🔐 **OWASP Top 10**：SQL 注入、XSS、CSRF 等常见漏洞
- 🛡️ **配置问题**：CORS、安全头、信息泄露等
- 🔍 **业务逻辑**：复杂的业务逻辑漏洞识别
- 📋 **合规检查**：安全最佳实践验证

## 🚨 注意事项

### 隐私和安全
- ⚠️ **数据传输**：HTTP 流量会发送到配置的 AI API 进行分析
- 🔒 **API 密钥安全**：请妥善保管你的 API 密钥
- 📜 **合规要求**：请确保符合你所在组织的数据安全政策

### 性能考虑
- 💰 **API 成本**：AI 分析会消耗 API 调用次数，请注意成本控制
- ⏱️ **响应时间**：AI 分析需要时间，可能影响扫描速度
- 🚫 **频率限制**：大量请求可能触发 API 频率限制

### 结果处理
- 🔍 **人工验证**：AI 分析结果需要安全专家进行人工复核
- ❌ **误报可能**：可能存在误报，建议结合传统扫描工具使用
- 📊 **持续改进**：可根据实际使用效果调整提示词

## 🆚 与原版本对比

| 功能 | 原版本 | 修改版本 |
|------|--------|----------|
| **API 支持** | 仅 OpenAI | 多服务商支持 |
| **配置灵活性** | 硬编码配置 | 完全可配置 |
| **模型选择** | 预定义列表 | 自定义输入 |
| **主动扫描** | 不支持 | 完全支持 |
| **API 格式** | Completions | Chat Completions + Completions |
| **错误处理** | 基础处理 | 增强的调试信息 |
| **中文支持** | 无 | 完整中文文档 |

## 🛠️ 开发信息

### 技术栈
- **编程语言**: Java 11+
- **构建工具**: Gradle
- **UI 框架**: Swing (Burp 原生)
- **HTTP 客户端**: OkHttp
- **API 框架**: Burp Suite Montoya API

### 项目结构
```
lib/src/main/java/
├── burp/                    # Burp 扩展入口
│   ├── MyBurpExtension.java # 主扩展类
│   └── MyScanCheck.java     # 扫描检查实现
├── burpgpt/
│   ├── gpt/                 # GPT 请求/响应模型
│   ├── gui/                 # 用户界面
│   ├── http/                # HTTP 客户端
│   └── utilities/           # 工具类
└── resources/               # 静态资源
```

### 构建命令
```bash
# 清理并构建
./gradlew clean shadowJar

# 仅构建
./gradlew shadowJar

# 运行测试
./gradlew test
```

## 📝 更新日志

### v1.1.0 (当前版本)
- ✅ 添加多 AI 服务商支持
- ✅ 实现可配置的 Base URL 和模型
- ✅ 支持 Chat Completions API 格式
- ✅ 添加主动扫描功能
- ✅ 增强错误处理和调试信息
- ✅ 添加中文文档支持

### v1.0.0 (原版本)
- ✅ 基础被动扫描功能
- ✅ OpenAI API 集成
- ✅ Burp Suite 集成

## 🤝 贡献指南

欢迎提交 Issue 和 Pull Request！

1. Fork 本项目
2. 创建功能分支 (`git checkout -b feature/amazing-feature`)
3. 提交更改 (`git commit -m 'Add some amazing feature'`)
4. 推送到分支 (`git push origin feature/amazing-feature`)
5. 打开 Pull Request

## 📄 许可证

本项目遵循原项目的许可证条款。

## 🙏 致谢

- 感谢原 [BurpGPT](https://github.com/aress31/burpgpt) 项目提供的基础框架
- 感谢 Burp Suite 团队提供的强大扩展 API
- 感谢所有 AI 服务提供商的支持

## 📞 联系方式

- **GitHub**: [Kento-Sec](https://github.com/Kento-Sec)
- **项目地址**: [BurpGPT](https://github.com/Kento-Sec/BurpGPT)

---

**⭐ 如果这个项目对你有帮助，请给个 Star！**
