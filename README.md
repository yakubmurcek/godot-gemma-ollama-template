# Godot + Gemma + Ollama Template

A minimal template for running **Google's Gemma models** in Godot 4.5+ via [Ollama](https://ollama.ai). Features both simple text generation with **Gemma3** and function/tool calling with **Functiongemma**.

## Features

- **Simple Chat** - Basic text generation with Gemma3
- **Function Calling** - Tool/function calling with Functiongemma
- **Self-contained scripts** - Copy-paste ready, no dependencies

## Prerequisites

1. [Godot 4.5+](https://godotengine.org/download)
2. [Ollama](https://ollama.ai) installed and running
3. Required models pulled:
   ```bash
   ollama pull gemma3:1b        # For simple chat
   ollama pull functiongemma    # For function calling
   ```

## Quick Start

1. Clone this repository
2. Start Ollama: `ollama serve`
3. Open project in Godot
4. Run the scene (F5)

## Scripts

### Simple Chat (`scripts/simple_chat.gd`)

Basic prompt → response flow using the `/api/generate` endpoint.

```gdscript
send_prompt("Tell me a joke")
```

### Function Calling (`scripts/function_calling.gd`)

Full round-trip: prompt → tool call → execute → response using `/api/chat` with tools.

```gdscript
send_message("What's the weather in Paris?")
# Model calls get_weather() → you execute it → send result back → get final answer
```

## Adding Your Own Tools

1. Define the tool in `_get_tool_definitions()`:
```gdscript
{
    "type": "function",
    "function": {
        "name": "your_function",
        "description": "What it does",
        "parameters": {
            "type": "object",
            "properties": {
                "param1": {"type": "string", "description": "..."}
            },
            "required": ["param1"]
        }
    }
}
```

2. Implement it in `_execute_tool()`:
```gdscript
"your_function":
    return _your_function(args)
```

## License

MIT License - see [LICENSE](LICENSE)
