#　やったことまとめ

## 手順

サーバの立ち上げ
```
SSE % python mini_server.py 
INFO:     Started server process [65628]
INFO:     Waiting for application startup.
INFO:     Application startup complete.
INFO:     Uvicorn running on http://0.0.0.0:8080 (Press CTRL+C to quit)
```

クライアントの起動
```
SSE % python mini_client.py 
tools: meta=None nextCursor=None tools=[Tool(name='hello_world', description='Say hello to someone', inputSchema={'properties': {'name': {'title': 'Name', 'type': 'string'}}, 'required': ['name'], 'title': 'hello_worldArguments', 'type': 'object'}), Tool(name='goodbye', description='Say goodbye to someone', inputSchema={'properties': {'name': {'title': 'Name', 'type': 'string'}}, 'required': ['name'], 'title': 'goodbyeArguments', 'type': 'object'})]
Tool result: [TextContent(type='text', text='Hello, MCP!', annotations=None)]
```

サーバ側の標準出力にINFOログが記録された。
```
SSE % python mini_server.py 
INFO:     Started server process [65628]
INFO:     Waiting for application startup.
INFO:     Application startup complete.
INFO:     Uvicorn running on http://0.0.0.0:8080 (Press CTRL+C to quit)
INFO:     127.0.0.1:61919 - "GET /sse HTTP/1.1" 200 OK
INFO:     127.0.0.1:61921 - "POST /messages/?session_id=01f25789c88849dbb06fa2b5cd06494a HTTP/1.1" 202 Accepted
INFO:     127.0.0.1:61921 - "POST /messages/?session_id=01f25789c88849dbb06fa2b5cd06494a HTTP/1.1" 202 Accepted
INFO:     127.0.0.1:61921 - "POST /messages/?session_id=01f25789c88849dbb06fa2b5cd06494a HTTP/1.1" 202 Accepted
[04/26/25 09:31:25] INFO     Processing request of type ListToolsRequest                  server.py:534
INFO:     127.0.0.1:61921 - "POST /messages/?session_id=01f25789c88849dbb06fa2b5cd06494a HTTP/1.1" 202 Accepted
                    INFO     Processing request of type CallToolRequest                   server.py:534
```