# Chinese AI Agent Platforms (中国 AI 智能体平台)

## Overview

China has become a global leader in AI agent development with multiple major platforms competing for market share. The Chinese market is projected to reach 852 billion yuan by 2028 with 72.7% annual growth.

## Market Landscape

| Company | Platform | Focus |
|---------|----------|-------|
| 智谱AI (Zhipu) | AutoGLM, GLM-PC | Autonomous agents |
| 百度 (Baidu) | 文心智能体 | General purpose |
| 阿里 (Alibaba) | 通义千问 | Enterprise |
| 腾讯 (Tencent) | 元器 | Platform ecosystem |
| 字节 (ByteDance) | Coze/扣子 | No-code builder |
| MiniMax | MiniMax Agent | Expert marketplace |

## Zhipu AI (智谱AI)

### Overview
Founded from Tsinghua University's Knowledge Engineering Lab. Creator of ChatGLM and AutoGLM.

### Key Products
- **AutoGLM**: Autonomous agent for phone/computer control
- **GLM-PC**: Desktop AI assistant
- **GLM-4-Voice**: Emotional voice model

### Capabilities
- Voice-controlled app navigation
- Cross-app task execution
- WeChat integration
- Food ordering,红包 sending

### Platform Features
```json
{
  "platform": "zhipu",
  "models": ["GLM-4", "GLM-4-Voice"],
  "capabilities": [
    "autonomous_execution",
    "voice_control",
    "cross_app_navigation",
    "task_automation"
  ],
  "api_access": "https://open.bigmodel.cn"
}
```

## Baidu Wenxin (百度文心)

### Overview
Baidu's AI platform powered by the ERNIE model series.

### Key Products
- **文心智能体平台**: Agent development platform
- **文心一言**: Conversational AI
- **文心快码**: Code generation

### Agent Features
- Full-scenario intelligent interaction
- Industry-specific solutions
- Enterprise integration

### Best For
- Enterprise deployments
- Industry verticals
- Government applications

## Alibaba Tongyi (阿里通义)

### Overview
Alibaba's AI assistant integrated with their cloud ecosystem.

### Key Products
- **通义千问**: Conversational AI
- **通义灵码**: Code assistant
- **通义听悟**: Meeting assistant

### Integration Points
- Alibaba Cloud
- DingTalk
- Taobao/Tmall ecosystem

### Best For
- E-commerce applications
- Cloud-native deployments
- Business process automation

## Tencent Yuanqi (腾讯元器)

### Overview
Tencent's agent platform with social ecosystem integration.

### Key Features
- WeChat integration
- QQ connectivity
- Gaming applications
- Social commerce

### Best For
- Social applications
- Gaming industry
- Consumer-facing bots

## ByteDance Coze (扣子)

### Overview
No-code AI agent builder from ByteDance.

### Key Features
- Visual agent builder
- Plugin marketplace
- Knowledge base integration
- Multi-channel deployment

### Agent Creation
```yaml
agent:
  name: "Customer Service Bot"
  model: "doubao-pro"
  plugins:
    - knowledge_base
    - order_lookup
    - ticket_creation
  triggers:
    - webhook
    - wechat
    - app
```

### Best For
- No-code development
- Quick deployment
- Content creation
- Customer service

## MiniMax China

### Overview
Leading AI company with expert marketplace and agent platform.

### Key Products
- **MiniMax Agent**: Desktop agent app
- **Expert Marketplace**: Paid expert agents
- **Skill Creator**: Custom skill building
- **MaxClaw**: Claw-like coding tool

### Market Position
- Strong in credit-based expert marketplace
- Developer-friendly tools
- Open-source skills repository

## Platform Comparison

| Platform | Code-Free | Enterprise | Voice | Mobile |
|----------|-----------|------------|-------|--------|
| Zhipu | ✓ | ✓ | ✓ | ✓ |
| Baidu | ✓ | ✓✓ | ✓ | ✓ |
| Alibaba | ✓ | ✓✓ | ✓ | ✓ |
| Tencent | ✓ | ✓ | ✓ | ✓✓ |
| Coze | ✓✓ | ✓ | ✗ | ✓ |
| MiniMax | ✓ | ✓ | ✓ | ✓ |

## Monetization Opportunities

### 1. Expert Agent Marketplace
Create specialized agents for:
- Industry-specific tasks
- Enterprise workflows
- Consumer applications

### 2. Enterprise Solutions
Build custom agents for:
- Manufacturing
- Healthcare
- Finance
- Government

### 3. Integration Services
Help companies integrate:
- WeChat mini-programs
- Enterprise systems
- Cloud platforms

### 4. Content & Skills
Create and sell:
- Skill packages
- Knowledge bases
- Agent templates

## Regulatory Considerations

- AI regulations in China are evolving
- Content approval requirements
- Data localization laws
- Algorithm registration

## Language & Cultural Notes

- Chinese language optimization is critical
- Cultural context in responses
- Local business practices
- Holiday and event awareness

## Key Resources

- 智谱AI: https://www.zhipuai.cn
- 百度文心: https://yiyan.baidu.com
- 阿里通义: https://tongyi.aliyun.com
- 腾讯元器: https://yuanqi.tencent.com
- 扣子: https://www.coze.cn
- MiniMax: https://www.minimaxi.com

## Recommended Agents for Chinese Platforms

1. **Fishing Industry Suite** - `agents/vertical/fishing-industry/` (industry vertical)
2. **Customer Support Suite** - `agents/combined-suites/customer-support-suite/`
3. **Financial Analysis Suite** - `agents/combined-suites/financial-analysis-suite/`
4. **Translation Agent** - `agents/communication/translator-agent/`

## Market Trends (2026)

- 72.7% annual growth rate
- Enterprise adoption accelerating
- Voice-first interfaces gaining share
- Mobile agent integration standard
- OpenClaw ecosystem emerging
