# 智能语义理解平台

## 项目简介

智能语义理解平台是一个功能强大的文本分析工具，提供语义分析和情感分析等核心功能，帮助用户深入理解文本内容的语义结构和情感倾向。

### 主要功能

#### 1. 语义分析
- **主题关键词提取**：自动识别文本中的核心主题和关键词
- **实体识别**：识别文本中的人名、组织、地点等实体信息
- **文本摘要**：自动生成文本的简要概括
- **意图分类**：分析文本的主要意图和目的

#### 2. 情感分析
- **整体情感分析**：评估文本的整体情感倾向（积极/中性/消极）
- **句子级别分析**：逐句分析文本的情感变化
- **情绪分布**：展示文本中各种情绪的分布情况
- **情感强度评估**：量化情感表达的强烈程度

#### 3. 历史记录管理
- **分析历史查看**：保存和查看所有分析记录
- **历史记录筛选**：按分析类型筛选历史记录
- **历史记录删除**：支持单条或批量删除历史记录

#### 4. 设置管理
- **API密钥配置**：管理外部API访问凭证
- **超时设置**：调整分析请求的超时时间
- **历史记录限制**：设置最大历史记录保存数量

## 技术架构

### 前端技术栈
- **框架**：Vue 3
- **构建工具**：Vite
- **路由**：Vue Router
- **样式**：CSS3 (自定义变量 + 响应式设计)
- **HTTP客户端**：Fetch API

### 后端技术栈
- **框架**：FastAPI (Python)
- **数据库**：SQLite
- **ORM**：SQLAlchemy
- **CORS支持**：FastAPI CORSMiddleware
- **API文档**：Swagger UI (自动生成)

## 项目结构

```
language-understand/
├── backend/                 # 后端代码
│   ├── main.py              # FastAPI应用入口
│   ├── routes/              # API路由定义
│   │   └── api.py           # 主要API路由
│   ├── models/              # 数据模型
│   │   ├── database.py      # 数据库模型
│   │   └── schemas.py       # 数据校验和序列化
│   ├── utils/               # 工具类
│   │   └── database.py      # 数据库操作工具
│   └── requirements.txt     # Python依赖
├── src/                     # 前端源代码
│   ├── views/               # 页面组件
│   │   ├── SemanticAnalysis.vue  # 语义分析页面
│   │   ├── SentimentAnalysis.vue # 情感分析页面
│   │   ├── History.vue      # 历史记录页面
│   │   └── Settings.vue     # 设置页面
│   ├── services/            # API服务
│   │   └── api.js           # API调用封装
│   ├── router/              # 路由配置
│   └── App.vue              # 应用主组件
├── index.html               # HTML入口
├── package.json             # npm依赖
└── vite.config.js           # Vite配置
```

## 安装与部署

### 前置条件
- Node.js 16+
- Python 3.10+
- pip (Python包管理器)

### 前端安装

1. 克隆项目
```bash
git clone <repository-url>
cd language-understand
```

2. 安装依赖
```bash
npm install
```

3. 开发环境运行
```bash
npm run dev
```

4. 构建生产版本
```bash
npm run build
```

### 后端安装

1. 进入后端目录
```bash
cd backend
```

2. 创建并激活虚拟环境（可选但推荐）
```bash
python -m venv env
# Windows
env\Scripts\activate
# Linux/Mac
source env/bin/activate
```

3. 安装依赖
```bash
pip install -r requirements.txt
```

4. 运行后端服务
```bash
python main.py
```

### 环境变量配置

后端服务可通过`.env`文件配置环境变量，主要配置项包括：
- `DATABASE_URL`：数据库连接URL
- `API_KEY`：外部API密钥（如使用）
- `TIMEOUT`：请求超时时间（秒）

## API文档

启动后端服务后，可通过以下地址访问自动生成的API文档：

- Swagger UI: http://localhost:9350/docs
- ReDoc: http://localhost:9350/redoc

### 主要API端点

1. **语义分析**
   - 端点：`POST /api/semantic-analysis`
   - 功能：对输入文本进行语义分析
   - 参数：文本内容和分析选项

2. **情感分析**
   - 端点：`POST /api/sentiment-analysis`
   - 功能：对输入文本进行情感分析
   - 参数：文本内容和分析选项

3. **历史记录**
   - 获取：`GET /api/history`
   - 清空：`DELETE /api/history`
   - 删除单条：`DELETE /api/history/{id}`

4. **设置管理**
   - 获取：`GET /api/settings`
   - 更新：`PUT /api/settings`

## 使用指南

### 语义分析使用

1. 在左侧输入框中输入要分析的文本
2. 选择需要的分析选项（可多选）：
   - 提取主题关键词
   - 实体识别
   - 生成文本摘要
   - 意图分类
3. 点击"开始分析"按钮
4. 右侧面板将显示分析结果，包括：
   - 主题关键词（标签形式展示）
   - 实体列表（表格形式展示）
   - 文本摘要（段落形式展示）
   - 意图分类结果

### 情感分析使用

1. 在左侧输入框中输入要分析的文本
2. 选择分析级别：
   - 整体分析：评估整个文本的情感
   - 句子级别分析：逐句分析情感变化
3. 选择是否显示详细分析（情绪分布）
4. 点击"开始分析"按钮
5. 右侧面板将显示分析结果，包括：
   - 整体情感倾向和强度
   - 情感得分可视化（进度条）
   - 句子级别情感分析（逐句展示）
   - 情绪分布统计（如选择详细分析）

### 历史记录管理

1. 导航至"历史记录"页面
2. 查看所有分析记录，包括语义分析和情感分析
3. 可按类型筛选历史记录
4. 可删除单条记录或清空所有历史记录

### 设置管理

1. 导航至"设置"页面
2. 配置API密钥（如使用外部API）
3. 调整请求超时时间
4. 设置最大历史记录保存数量
5. 保存设置以应用更改

## 功能特点

1. **用户友好的界面**：直观的布局和交互设计，易于使用
2. **实时分析**：快速响应的分析过程，提供即时反馈
3. **可定制的分析选项**：根据需求选择所需的分析功能
4. **详细的分析结果**：提供全面而深入的文本分析信息
5. **响应式设计**：适配不同屏幕尺寸的设备
6. **历史记录追踪**：保存和管理分析历史，方便查阅

## 浏览器兼容性

- Chrome (推荐)
- Firefox
- Safari
- Edge

## 开发与调试

### 前端开发

1. 启动开发服务器：`npm run dev`
2. 访问：http://localhost:5173
3. 开发过程中支持热重载

### 后端开发

1. 启动开发服务器：`python main.py`
2. API服务地址：http://localhost:9350
3. API文档：http://localhost:9350/docs
4. 开发模式支持自动重载

## 部署建议

### 开发环境
- 前端：使用Vite开发服务器
- 后端：直接运行Python脚本

### 生产环境
1. 前端：
   - 构建生产版本：`npm run build`
   - 部署dist目录到Web服务器（如Nginx、Apache）

2. 后端：
   - 使用Gunicorn或uWSGI作为WSGI服务器
   - 配置反向代理（如Nginx）
   - 建议使用环境变量管理敏感配置

3. 数据库：
   - 生产环境考虑使用PostgreSQL或MySQL替代SQLite
   - 定期备份数据库

## 版本历史

- **v1.0.0** (2024-01-XX)
  - 初始版本发布
  - 实现语义分析和情感分析核心功能
  - 支持历史记录和设置管理

## 许可证

[MIT License](LICENSE)

## 联系方式

如有问题或建议，请通过以下方式联系：

- 项目仓库：<repository-url>
- 维护者：<maintainer-contact>

## 致谢

感谢所有为项目开发和改进做出贡献的开发者和用户！
