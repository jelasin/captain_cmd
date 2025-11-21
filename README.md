# Captain CMD Tools

## 简介

Captain CMD Tools 是一个基于 LangChain 和 LangGraph 的命令行工具，用于与 LLM 进行交互。支持长上下文存储，保存用户对话历史。按量调用LLM，支持自定义模型，无调用限制。

## 使用方法

### 1. config.toml 配置文件

将 mcpServers 配置文件放在 mcp_servers.content 中即可，使用json格式存储，放在这里并不会启用。

* model_config.tool_names 是需要启用的mcp server的名称，需要与 mcp_servers.content 中的 mcpServers 中的 key 一致。
* model_config.model_name 是模型名称，需要与模型提供商的名称一致。
* model_config.api_key 是模型API密钥，需要与模型提供商的API密钥一致。
* model_config.base_url 是模型API地址，需要与模型提供商的API地址一致。
* model_config.system_prompt 是系统提示词。

```toml
[mcp_servers]
content = '''
{
    "mcpServers": {
        "example-stdio-mcp-name": {
            "transport": "stdio", 
            "command": "python.exe", 
            "args": ["path/to/example_mcp.py"]
        },
        "example-tcp-mcp-name": {
            "transport": "streamable_http",
            "url": "http://mcp-server:port/mcp"
        }
     }
}
'''

[model_config]
model_name = ""
api_key = ""
base_url = ""
tool_names = ["example-stdio-mcp-name", "example-tcp-mcp-name"]
system_prompt = ""
```

### 2. 运行命令

* --config 是配置文件路径，默认是 config.toml。
* --workspace 是工作空间路径。

```bash
python main.py --config config.toml --workspace workspace
```

```text
(.venv) PS E:\DM\captain_cmd> python .\main.py --config .\config.toml --workspace .

🚀 Welcome to Captain Cmd Tools

  Model          gpt-5-2025-08-07
  Tools          1 loaded
    →            ida-mcp-proxy
  Workspace      .
  CheckpointDB   .\.captain\checkpoint.db  
  StoreDB        .\.captain\store.db       


Type 'exit' or 'quit' to exit


> read requirements.txt

[ChatStream] Request: model=gpt-5-2025-08-07, tools=1
[init_resources] Database resources initialized
[build_agent] Loaded 40 tools for 'ida-mcp-proxy'
[build_agent] Initialized model 'gpt-5-2025-08-07' with base_url '******'
[build_agent] Agent created successfully with 40 tools
╭──────────────────────────────────── ✅ write_todos - Complete ────────────────────────────────────╮
│ 🔧 write_todos                                                                                    │
│ Args: {                                                                                           │
│   "todos": [                                                                                      │
│     {                                                                                             │
│       "content": "{ \"title\": \"Verify requirements.txt exists\", \"objective\": \"List project  │
│ root to confirm requirements.txt is present\", \"priority\": \"high\", \"requires_approval\":     │
│ false }",                                                                                         │
│       "status": "pending"                                                                         │
│     },                                                                                            │
│     {                                                                                             │
│       "content": "{ \"title\": \"Read requirements.txt\", \"objective\": \"Open and read the      │
│ requirements.txt file contents\", \"priority\": \"high\", \"requires_approval\": false }",        │
│       "status": "pending"                                                                         │
│     },                                                                                            │
│     {                                                                                             │
│       "content": "{ \"title\": \"Summarize dependencies\", \"objective\": \"Extract and list      │
│ libraries with pinned versions from requirements.txt\", \"priority\": \"medium\",                 │
│ \"requires_approval\": false }",                                                                  │
│       "status": "pending"                                                                         │
│     },                                                                                            │
│     {                                                                                             │
│       "content": "{ \"title\": \"Confirm next action\", \"objective\": \"Ask if user wants        │
│ installation instructions or dependency grouping\", \"priority\": \"low\", \"requires_approval\": │
│ false }",                                                                                         │
│       "status": "pending"                                                                         │
│     }                                                                                             │
│   ]                                                                                               │
│ }                                                                                                 │
│                                                                                                   │
│ ✅ Result:                                                                                        │
│ Updated todo list to [{'content': '{ "title": "Verify requirements.txt exists", "objective":      │
│ "List project root to confirm requirements.txt is present", "priority": "high",                   │
│ "requires_approval": false }', 'status': 'pending'}, {'content': '{ "title": "Read                │
│ requirements.txt", "objective": "Open and read the requirements.txt file contents", "priority":   │
│ "high", "requires_approval": false }', 'status': 'pending'}, {'content': '{ "title": "Summarize   │
│ dependencies", "objective": "Extract and list libraries with pinned versions from                 │
│ requirements.txt", "priority": "medium", "requires_approval": false }', 'status': 'pending'},     │
│ {'content': '{ "title": "Confirm next action", "objective": "Ask if user wants installation       │
│ instructions or dependency grouping", "priority": "low", "requires_approval": false }', 'status': │
│ 'pending'}]                                                                                       │
╰───────────────────────────────────────────────────────────────────────────────────────────────────╯
╭──────────────────────────────────────── ✅ ls - Complete ─────────────────────────────────────────╮
│ 🔧 ls                                                                                             │
│ Args: {                                                                                           │
│   "path": "/"                                                                                     │
│ }                                                                                                 │
│                                                                                                   │
│ ✅ Result:                                                                                        │
│ ["/\\.build/", "/\\.captain/", "/\\.git/", "/\\.github/", "/\\.gitignore", "/\\.venv/",           │
│ "/\\README.md", "/\\agent/", "/\\build.py", "/\\chat/", "/\\config.example.toml",                 │
│ "/\\config.toml", "/\\main.py", "/\\requirements.txt", "/\\test.py", "/\\tools/", "/\\utils/",    │
│ "/memories/"]                                                                                     │
╰───────────────────────────────────────────────────────────────────────────────────────────────────╯
╭───────────────────────────────────── ✅ read_file - Complete ─────────────────────────────────────╮
│ 🔧 read_file                                                                                      │
│ Args: {                                                                                           │
│   "file_path": "/requirements.txt"                                                                │
│ }                                                                                                 │
│                                                                                                   │
│ ✅ Result:                                                                                        │
│      1  # python version: 3.13.2                                                                  │
│      2  langchain==1.0.8                                                                          │
│      3  langgraph==1.0.3                                                                          │
│      4  deepagents==0.2.7                                                                         │
│      5  langchain-deepseek==1.0.1                                                                 │
│      6  langchain-mcp-adapters==0.1.13                                                            │
│      7  mcp==1.21.2                                                                               │
│      8  tavily-python==0.7.13                                                                     │
│      9  Nuitka==2.8.6                                                                             │
│     10  langgraph-checkpoint-sqlite==3.0.0                                                        │
│     11  aiosqlite==0.21.0                                                                         │
│     12  rich==14.2.0                                                                              │
│     13  prompt_toolkit==3.0.52                                                                    │
╰───────────────────────────────────────────────────────────────────────────────────────────────────╯
╭──────────────────────────────────── ✅ write_todos - Complete ────────────────────────────────────╮
│ 🔧 write_todos                                                                                    │
│ Args: {                                                                                           │
│   "todos": [                                                                                      │
│     {                                                                                             │
│       "content": "{ \"title\": \"Verify requirements.txt exists\", \"objective\": \"List project  │
│ root to confirm requirements.txt is present\", \"priority\": \"high\", \"requires_approval\":     │
│ false }",                                                                                         │
│       "status": "completed"                                                                       │
│     },                                                                                            │
│     {                                                                                             │
│       "content": "{ \"title\": \"Read requirements.txt\", \"objective\": \"Open and read the      │
│ requirements.txt file contents\", \"priority\": \"high\", \"requires_approval\": false }",        │
│       "status": "completed"                                                                       │
│     },                                                                                            │
│     {                                                                                             │
│       "content": "{ \"title\": \"Summarize dependencies\", \"objective\": \"Extract and list      │
│ libraries with pinned versions from requirements.txt\", \"priority\": \"medium\",                 │
│ \"requires_approval\": false }",                                                                  │
│       "status": "completed"                                                                       │
│     },                                                                                            │
│     {                                                                                             │
│       "content": "{ \"title\": \"Confirm next action\", \"objective\": \"Ask if user wants        │
│ installation instructions or dependency grouping\", \"priority\": \"low\", \"requires_approval\": │
│ false }",                                                                                         │
│       "status": "pending"                                                                         │
│     }                                                                                             │
│   ]                                                                                               │
│ }                                                                                                 │
│                                                                                                   │
│ ✅ Result:                                                                                        │
│ Updated todo list to [{'content': '{ "title": "Verify requirements.txt exists", "objective":      │
│ "List project root to confirm requirements.txt is present", "priority": "high",                   │
│ "requires_approval": false }', 'status': 'completed'}, {'content': '{ "title": "Read              │
│ requirements.txt", "objective": "Open and read the requirements.txt file contents", "priority":   │
│ "high", "requires_approval": false }', 'status': 'completed'}, {'content': '{ "title": "Summarize │
│ dependencies", "objective": "Extract and list libraries with pinned versions from                 │
│ requirements.txt", "priority": "medium", "requires_approval": false }', 'status': 'completed'},   │
│ {'content': '{ "title": "Confirm next action", "objective": "Ask if user wants installation       │
│ instructions or dependency grouping", "priority": "low", "requires_approval": false }', 'status': │
│ 'pending'}]                                                                                       │
╰───────────────────────────────────────────────────────────────────────────────────────────────────╯
╭───────────────────────────────────────── 💬 Model Answer ─────────────────────────────────────────╮
│ The project depends on the following Python libraries (Python 3.13.2):                            │
│                                                                                                   │
│  • langchain==1.0.8                                                                               │
│  • langgraph==1.0.3                                                                               │
│  • deepagents==0.2.7                                                                              │
│  • langchain-deepseek==1.0.1                                                                      │
│  • langchain-mcp-adapters==0.1.13                                                                 │
│  • mcp==1.21.2                                                                                    │
│  • tavily-python==0.7.13                                                                          │
│  • Nuitka==2.8.6                                                                                  │
│  • langgraph-checkpoint-sqlite==3.0.0                                                             │
│  • aiosqlite==0.21.0                                                                              │
│  • rich==14.2.0                                                                                   │
│  • prompt_toolkit==3.0.52                                                                         │
│                                                                                                   │
│ Would you like me to install them or group them by purpose (frameworks, adapters, storage,        │
│ tooling)?                                                                                         │
╰───────────────────────────────────────────────────────────────────────────────────────────────────╯

>
👋 Goodbye!
[cleanup] Store connection closed
[cleanup] Checkpoint connection closed
(.venv) PS E:\DM\captain_cmd> 
```
