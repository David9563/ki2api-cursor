# Ki2API - OpenAI兼容API (增强版)

> 🙏 **致谢**: 本项目基于 [zhalice2011/ki2api](https://github.com/zhalice2011/ki2api) 进行开发和增强，感谢原作者的贡献！

一个将 Kiro/AWS CodeWhisperer 的 Claude 模型转换为 OpenAI 兼容 API 的服务，支持 Cursor、ChatBox 等工具使用。

## ✨ 增强功能

相比原版，本 Fork 增加了以下功能：

- � ***多模型支持** - 支持 Claude Opus 4.5、Sonnet 4.5 等多种模型
- �️ **工具o调用支持** - 完整支持 Function Calling / Tool Use
- 🔄 **双格式兼容** - 同时支持 OpenAI 和 Anthropic 格式的工具调用
- 🖼️ **图片支持** - 支持多模态图片输入
- 🎯 **Cursor 适配** - 专门优化了与 Cursor IDE 的兼容性
- 📝 **调试功能** - 可保存请求到文件便于调试

## 支持的模型

| 模型别名 | 实际模型 |
|---------|---------|
| `claude-sonnet-4-5-20250929` | Claude Sonnet 4.5 |
| `claude-opus-4-5-20251101` | Claude Opus 4.5 |
| `claude-4.5-opus-high-thinking` | Claude Opus 4.5 (Cursor) |
| `claude-4-sonnet` | Claude Sonnet 4.5 (Cursor) |
| `gpt-4` / `gpt-4o` | 映射到 Claude Sonnet 4.5 |

## 快速开始

### 1. 确保已登录 Kiro

Token 文件位置：
- **Windows**: `%USERPROFILE%\.aws\sso\cache\kiro-auth-token.json`
- **macOS/Linux**: `~/.aws/sso/cache/kiro-auth-token.json`

### 2. 读取 Token

```bash
python token_reader.py
```

### 3. 启动服务

**方式一：直接运行**
```bash
pip install -r requirements.txt
python app.py
```

**方式二：Docker**
```bash
docker-compose up -d
```

服务将在 http://localhost:8989 启动

### 4. 配置 Cursor

由于 Cursor 会阻止 localhost 连接，需要使用 ngrok：

```bash
ngrok http 8989
```

然后在 Cursor 设置中：
- **API Key**: `ki2api-key-2024`
- **Base URL**: `https://xxx.ngrok-free.dev/v1`

## API 端点

| 端点 | 方法 | 说明 |
|-----|------|-----|
| `/v1/models` | GET | 获取模型列表 |
| `/v1/chat/completions` | POST | 聊天补全 |
| `/health` | GET | 健康检查 |

## 测试

```bash
curl -X POST http://localhost:8989/v1/chat/completions \
  -H "Authorization: Bearer ki2api-key-2024" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "claude-sonnet-4-5-20250929",
    "messages": [{"role": "user", "content": "你好"}],
    "max_tokens": 1000
  }'
```

## 环境变量

| 变量名 | 默认值 | 说明 |
|--------|--------|------|
| `API_KEY` | `ki2api-key-2024` | API 访问密钥 |
| `KIRO_ACCESS_TOKEN` | - | Kiro 访问令牌 |
| `KIRO_REFRESH_TOKEN` | - | Kiro 刷新令牌 |

## ⚠️ 免责声明

- 本项目仅供**学习和研究**使用
- 使用本项目时请遵守 [AWS 服务条款](https://aws.amazon.com/service-terms/) 和 [Anthropic 使用政策](https://www.anthropic.com/policies)
- 本项目通过 Kiro 的认证机制访问 AWS CodeWhisperer，请确保你有合法的使用权限
- **请勿**将本项目用于任何商业用途或违反服务条款的行为
- 作者不对任何滥用行为或由此产生的后果负责
- 使用本项目即表示你已理解并同意以上条款

## 许可证

GPL-3.0 License

## 致谢

- 原项目: [zhalice2011/ki2api](https://github.com/zhalice2011/ki2api)
