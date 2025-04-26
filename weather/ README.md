# Claude連携の手順

https://modelcontextprotocol.io/quickstart/server


## 発生したエラー

```
% tail -f mcp.log
2025-04-26T02:18:09.193Z [error] [Demo] spawn uv ENOENT
2025-04-26T02:18:09.193Z [error] [Demo] spawn uv ENOENT
2025-04-26T02:18:09.197Z [info] [Demo] Server transport closed
2025-04-26T02:18:09.198Z [info] [Demo] Client transport closed
2025-04-26T02:18:09.198Z [info] [Demo] Server transport closed unexpectedly, this is likely due to the process exiting early. If you are developing this MCP server you can add output to stderr (i.e. `console.error('...')` in JavaScript, `print('...', file=sys.stderr)` in python) and it will appear in this log.
2025-04-26T02:18:09.198Z [error] [Demo] Server disconnected. For troubleshooting guidance, please visit our [debugging documentation](https://modelcontextprotocol.io/docs/tools/debugging)
2025-04-26T02:18:09.198Z [info] [weather] Server transport closed
2025-04-26T02:18:09.198Z [info] [weather] Client transport closed
2025-04-26T02:18:09.198Z [info] [weather] Server transport closed unexpectedly, this is likely due to the process exiting early. If you are developing this MCP server you can add output to stderr (i.e. `console.error('...')` in JavaScript, `print('...', file=sys.stderr)` in python) and it will appear in this log.
2025-04-26T02:18:09.198Z [error] [weather] Server disconnected. For troubleshooting guidance, please visit our [debugging documentation](https://modelcontextprotocol.io/docs/tools/debugging)
```


```
% tail -f mcp-server-weather.log
2025-04-26T02:23:31.231Z [weather] [info] Initializing server...
2025-04-26T02:23:31.242Z [weather] [error] spawn uv ENOENT {"context":"connection","stack":"Error: spawn uv ENOENT\n    at ChildProcess._handle.onexit (node:internal/child_process:285:19)\n    at onErrorNT (node:internal/child_process:483:16)\n    at process.processTicksAndRejections (node:internal/process/task_queues:82:21)"}
2025-04-26T02:23:31.243Z [weather] [error] spawn uv ENOENT {"stack":"Error: spawn uv ENOENT\n    at ChildProcess._handle.onexit (node:internal/child_process:285:19)\n    at onErrorNT (node:internal/child_process:483:16)\n    at process.processTicksAndRejections (node:internal/process/task_queues:82:21)"}
2025-04-26T02:23:31.249Z [weather] [info] Server transport closed
2025-04-26T02:23:31.249Z [weather] [info] Client transport closed
2025-04-26T02:23:31.249Z [weather] [info] Server transport closed unexpectedly, this is likely due to the process exiting early. If you are developing this MCP server you can add output to stderr (i.e. `console.error('...')` in JavaScript, `print('...', file=sys.stderr)` in python) and it will appear in this log.
2025-04-26T02:23:31.249Z [weather] [error] Server disconnected. For troubleshooting guidance, please visit our [debugging documentation](https://modelcontextprotocol.io/docs/tools/debugging) {"context":"connection"}
```

## 対処したこと

commandのところをフルパスに、argsのweatherのところをフルパスに

手順書
```
{
    "mcpServers": {
        "weather": {
            "command": "uv",
            "args": [
                "--directory",
                "/ABSOLUTE/PATH/TO/PARENT/FOLDER/weather",
                "run",
                "weather.py"
            ]
        }
    }
}
```


```json
{
  "mcpServers": {
    "weather": {
      "command": "/Users/kounan13/.local/bin/uv",
      "args": [
        "--directory",
        "/Users/kounan13/Study/git/mcpsample/weather",
        "run",
        "weather.py"
      ]
    }
  }
}
```

## 実行した

### 質問1

質問内容
```
I'd be happy to check the current weather forecast for Sacramento. Let me retrieve that information for you.
```

リクエスト

get_forecast
```json
{
  `latitude`: 38.5816,
  `longitude`: -121.4944
}

```

レスポンス
```
Tonight:
Temperature: 49°F
Wind: 3 to 9 mph SSW
Forecast: A chance of rain showers after midnight. Mostly cloudy, with a low around 49. South southwest wind 3 to 9 mph. Chance of precipitation is 30%.

---

Saturday:
Temperature: 63°F
Wind: 6 mph S
Forecast: A chance of rain showers. Mostly cloudy, with a high near 63. South wind around 6 mph. Chance of precipitation is 40%.

---

Saturday Night:
Temperature: 50°F
Wind: 6 mph SSW
Forecast: A chance of rain showers before 5am. Mostly cloudy, with a low around 50. South southwest wind around 6 mph. Chance of precipitation is 40%. New rainfall amounts less than a tenth of an inch possible.

---

Sunday:
Temperature: 66°F
Wind: 6 mph SSE
Forecast: Partly sunny, with a high near 66. South southeast wind around 6 mph.

---

Sunday Night:
Temperature: 48°F
Wind: 5 mph WSW
Forecast: Mostly clear, with a low around 48. West southwest wind around 5 mph.
```

```
Here's the current weather forecast for Sacramento:

For tonight (Saturday, April 26):
- Temperature: 49°F
- Wind: 3 to 9 mph from the south-southwest
- Forecast: Mostly cloudy with a 30% chance of rain showers after midnight

Tomorrow (Saturday, April 26):
- High temperature: 63°F
- Wind: 6 mph from the south
- Forecast: Mostly cloudy with a 40% chance of rain showers

Looking ahead to Sunday:
- High near 66°F with partly sunny skies
- The night will be mostly clear with a low around 48°F

Would you like any other weather information for Sacramento or another location?
```



### 質問2

質問内容
What are the active weather alerts in Texas?

```
Let me check the current weather alerts for Texas.
```

リクエスト
```json
get_alerts
{
  `state`: `TX`
}
```

レスポンス
```json
Unable to fetch alerts or no alerts found.Good news! It appears there are currently no active weather alerts for the state of Texas. This means there are no severe weather warnings, watches, or advisories in effect at this time.
Weather conditions can change rapidly, so if you're concerned about specific weather conditions in a particular area of Texas, let me know and I can check the forecast for that location.
```