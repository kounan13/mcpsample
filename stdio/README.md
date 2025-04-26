

```
stdio % python mini_server.py
```

```
stdio % python mini_client.py
[04/26/25 09:23:24] INFO     Processing request of type ListToolsRequest                                   server.py:534
tools: meta=None nextCursor=None tools=[Tool(name='hello_world', description='Say hello to someone', inputSchema={'properties': {'name': {'title': 'Name', 'type': 'string'}}, 'required': ['name'], 'title': 'hello_worldArguments', 'type': 'object'}), Tool(name='goodbye', description='Say goodbye to someone', inputSchema={'properties': {'name': {'title': 'Name', 'type': 'string'}}, 'required': ['name'], 'title': 'goodbyeArguments', 'type': 'object'})]
                    INFO     Processing request of type CallToolRequest                                    server.py:534
Tool result: [TextContent(type='text', text='Hello, MCP!', annotations=None)]
```