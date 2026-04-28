# Flowchart - 任務管理系統

## 使用者流程圖 (User Flow)
```mermaid
flowchart LR
    A([使用者開啟網站]) --> B[首頁 - 任務列表]
    B --> C{選擇操作}
    C -->|新增任務| D[填寫任務表單]
    D --> E[提交表單]
    E --> F[任務建立成功，返回任務列表]
    C -->|查看任務| G[任務詳情頁]
    G --> H[可編輯或刪除]
    H --> I[更新任務或刪除]
    I --> F
    C -->|分配任務| J[選擇成員並設定比例]
    J --> K[任務分配成功]
    K --> F
    C -->|查看統計| L[儀表板]
    L --> M[顯示任務進度圖表]
    M --> F
```

## 系統序列圖 (Sequence Diagram)
```mermaid
sequenceDiagram
    participant User as 使用者
    participant Browser
    participant Flask as Flask Route
    participant Model as Model
    participant DB as SQLite
    User->>Browser: 開啟網站
    Browser->>Flask: GET /tasks
    Flask->>Model: fetch_tasks()
    Model->>DB: SELECT * FROM tasks
    DB-->>Model: 任務資料
    Model-->>Flask: 任務列表
    Flas​k-->>Browser: 渲染任務列表頁
    User->>Browser: 點擊新增任務
    Browser->>Flask: POST /tasks
    Flask->>Model: create_task(data)
    Model->>DB: INSERT INTO tasks
    DB-->>Model: 成功
    Model-->>Flask: 任務已建立
    Flask-->>Browser: 重導向至任務列表
```

## 功能清單對照表
| 功能 | URL 路徑 | HTTP 方法 |
|------|----------|-----------|
| 任務建立 | /tasks | POST |
| 任務分配 | /tasks/:id/assign | POST |
| 進度追蹤 | /tasks/:id | GET/PUT |
| 提醒通知 | /tasks/:id/remind | POST |
| 紀錄與查詢 | /tasks | GET |
