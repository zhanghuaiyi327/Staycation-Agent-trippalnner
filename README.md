**Staycation智能旅行助手**是一个基于多智能体协作的全栈Web应用，旨在为用户提供个性化的旅行规划服务。项目采用前后端分离架构，结合AI智能体、地图服务和社交功能，打造一站式的旅行规划体验。

### 核心价值
- 🗺️ **智能行程规划** - 基于用户偏好生成个性化旅行计划
- 🤖 **多智能体协作** - 四个专业Agent协同工作
- 🌍 **实时地图服务** - 集成高德地图API
- 👥 **社交互动** - 发现圈分享和实时聊天
- ⏰ **时区感知** - 全球时间同步管理

---

## 技术架构

### 后端技术栈 (Python)
| 技术 | 版本 | 用途 |
|------|------|------|
| **FastAPI** | 0.115.0+ | Web框架，提供RESTful API |
| **Uvicorn** | 0.32.0+ | ASGI服务器，高性能异步 |
| **SQLAlchemy** | 2.0.0+ | ORM，数据库操作 |
| **LangChain** | 0.2.0+ | AI智能体框架 |
| **Pydantic** | 2.0.0+ | 数据验证和序列化 |
| **JWT** | 内置 | 用户认证和授权 |
| **WebSocket** | 内置 | 实时通信和时间同步 |

### 前端技术栈 (Vue.js)
| 技术 | 版本 | 用途 |
|------|------|------|
| **Vue 3** | 3.5.13+ | 前端框架 |
| **TypeScript** | 5.7.3+ | 类型安全的JavaScript |
| **Vite** | 6.0.7+ | 构建工具和开发服务器 |
| **Ant Design Vue** | 4.2.6+ | UI组件库 |
| **Pinia** | 3.0.4+ | 状态管理 |
| **Vue Router** | 4.5.0+ | 前端路由 |
| **Axios** | 1.7.9+ | HTTP客户端 |
| **高德地图JS API** | 1.0.1+ | 地图展示和交互 |

### 数据库
- **主数据库**: SQLite (开发环境) / MySQL (生产环境)
- **文件存储**: 本地文件系统 (头像、图片上传)
- **缓存**: 内存缓存 (智能体结果缓存)

- ## 核心功能模块

### 1. 智能旅行规划系统
**文件**: `backend/app/agents/trip_planner_agent_v2.py`

#### 多智能体架构
- **景点搜索Agent**: 使用高德地图API搜索景点
- **天气查询Agent**: 查询目的地天气信息
- **酒店推荐Agent**: 推荐合适的住宿
- **行程规划Agent**: 整合信息生成完整计划

#### 工作流程
1. 用户输入旅行需求（城市、日期、偏好等）
2. 景点搜索Agent搜索相关景点
3. 天气查询Agent获取天气信息
4. 酒店推荐Agent推荐住宿
5. 行程规划Agent生成详细行程
6. 结果缓存提升后续性能

#### 特色功能
- **智能缓存**: MD5哈希缓存键，避免重复计算
- **重试机制**: 网络请求失败自动重试
- **备用方案**: Agent失败时生成基础计划
- **性能监控**: API调用统计和性能分析

### 2. 用户认证系统
**文件**: `backend/app/api/routes/auth.py`, `backend/app/services/auth_service.py`

#### 功能特性
- JWT令牌认证（Access Token + Refresh Token）
- 图形验证码防止暴力破解
- 登录失败锁定机制
- 记住登录功能（30天有效期）
- 密码重置和安全验证

#### 安全措施
- 密码哈希存储（bcrypt）
- 登录尝试次数限制
- 验证码过期时间控制
- Token自动刷新机制

### 3. 实时聊天系统
**文件**: `backend/app/api/routes/chat.py`, `backend/app/services/websocket_manager.py`

#### 技术实现
- WebSocket实时双向通信
- 消息持久化存储
- 未读消息计数
- 在线状态管理
- 消息历史记录

#### 前端集成
- 自动重连机制
- 消息发送状态反馈
- 实时消息推送
- 聊天界面优化

### 4. 发现圈社交功能
**文件**: `backend/app/api/routes/discover.py`, `backend/app/services/discover_service.py`

#### 功能特性
- 用户发布旅行分享
- 图片上传和展示
- 点赞和评论互动
- 关注用户动态
- 热门内容推荐

#### 技术实现
- 多图片上传支持
- 图片压缩和优化
- 分页加载
- 实时互动通知

### 5. 时间管理系统
**文件**: `backend/app/api/routes/time.py`, `backend/app/services/time_service.py`

#### 核心功能
- 时区感知的时间显示
- WebSocket时间同步
- 自动时间校准
- 全球时间转换

#### 技术实现
- 时区中间件自动处理
- 客户端-服务器时间同步
- 时间漂移自动修正
- 实时时钟组件
- ## 安装和运行

### 后端启动
```bash
# 进入后端目录
cd backend

# 安装依赖
pip install -r requirements.txt

# 初始化数据库
python init_db.py

# 启动开发服务器
python run.py
# 或
uvicorn app.api.main:app --reload --host 0.0.0.0 --port 8000
```

### 前端启动
```bash
# 进入前端目录
cd frontend

# 安装依赖
npm install

# 启动开发服务器
npm run dev
```

### 访问地址
- **前端应用**: http://localhost:5173
- **后端API**: http://localhost:8000
- **API文档**: http://localhost:8000/docs
- **ReDoc文档**: http://localhost:8000/redoc

---

## 开发指南

### 代码规范
1. **Python**: 遵循PEP 8规范，使用Black格式化
2. **TypeScript**: 使用ESLint + Prettier
3. **Git提交**: 遵循Conventional Commits规范
4. **文档**: 所有公共API必须有文档字符串

### 测试
```bash
# 后端测试
cd backend
pytest tests/

# 前端测试
cd frontend
npm test
```

### 部署
#### 生产环境建议
1. **数据库**: 使用MySQL或PostgreSQL
2. **文件存储**: 使用云存储服务（如AWS S3、阿里云OSS）
3. **缓存**: 使用Redis
4. **反向代理**: Nginx + Gunicorn/Uvicorn
5. **容器化**: Docker + Docker Compose

#### 环境变量管理
- 开发环境: `.env` 文件
- 生产环境: 使用环境变量或配置管理服务
