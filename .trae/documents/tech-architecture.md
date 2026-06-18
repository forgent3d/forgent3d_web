## 1. 架构设计

```mermaid
flowchart LR
    subgraph Frontend ["前端层"]
        A["React组件"] --> B["Zustand状态管理"]
        B --> C["IndexedDB存储"]
        A --> D["Three.js 3D渲染"]
        A --> E["AI SDK"]
    end
    
    subgraph External ["外部服务"]
        F["OpenAI API"]
    end
    
    E --> F
```

## 2. 技术描述

- **前端**：React@18 + TypeScript + TailwindCSS@3 + Vite
- **状态管理**：Zustand
- **3D渲染**：Three.js + @react-three/fiber + @react-three/drei
- **AI SDK**：ai (Vercel AI SDK)
- **存储**：IndexedDB (idb库)
- **代码高亮**：@codemirror/state + @codemirror/view + @codemirror/lang-python

## 3. 路由定义

| 路由 | 用途 |
|------|------|
| / | 主页，对话+代码+预览 |

## 4. 数据模型

### 4.1 IndexedDB数据结构

**数据库名称**：build123d-app

**存储对象**：
- **conversations**：存储对话列表
- **messages**：存储消息列表

### 4.2 类型定义

```typescript
interface Conversation {
  id: string;
  title: string;
  createdAt: string;
  updatedAt: string;
}

interface Message {
  id: string;
  conversationId: string;
  role: 'user' | 'assistant';
  content: string;
  code: string;
  createdAt: string;
}
```

## 5. 项目结构

```
src/
├── components/
│   ├── Chat.tsx          # 对话组件
│   ├── CodeEditor.tsx    # 代码编辑器组件
│   └── ModelPreview.tsx  # 3D模型预览组件
├── hooks/
│   ├── useChat.ts        # 对话逻辑hook
│   └── useIndexedDB.ts   # IndexedDB操作hook
├── stores/
│   └── appStore.ts       # Zustand状态管理
├── utils/
│   ├── codeParser.ts     # 代码解析器
│   └── db.ts             # IndexedDB初始化
├── types/
│   └── index.ts          # TypeScript类型定义
├── App.tsx               # 主应用组件
├── main.tsx              # 入口文件
└── index.css             # 全局样式
```
