# Gemini4 - AI Agent System

A modular AI agent system built with Google's Gemini API, implementing Perception, Memory, Decision-Making, and Action modules to solve complex problems through iterative reasoning and tool execution.

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Architecture](#architecture)
- [Installation](#installation)
- [Configuration](#configuration)
- [Usage](#usage)
- [Project Structure](#project-structure)
- [Modules](#modules)
- [Tools](#tools)
- [Examples](#examples)
- [Logging](#logging)
- [Troubleshooting](#troubleshooting)

## 🎯 Overview

Gemini4 is an intelligent agent system that leverages Google's Gemini AI to:
- Process and understand natural language queries
- Perform step-by-step mathematical calculations
- Execute visualization tasks using Turtle graphics
- Maintain state and memory across iterations
- Make informed decisions based on context and history

### Example Use Case

**Query:** "Find the ASCII values of characters in INDIA and then return sum of exponentials of those values"

**Solution:** The agent will:
1. Convert "INDIA" to ASCII values: [73, 78, 68, 73, 65]
2. Calculate the exponential sum: `5.052393630276104e31`
3. Visualize the result using Turtle graphics

## ✨ Features

- **Modular Architecture**: Clean separation of concerns with Perception, Memory, Decision-Making, and Action modules
- **Intelligent Reasoning**: Uses Gemini AI for step-by-step problem solving
- **Memory Management**: Tracks iterations, tool calls, and execution history
- **Tool Integration**: 23+ built-in tools for mathematical operations and visualization
- **Visualization**: Turtle graphics for displaying results
- **Comprehensive Logging**: Detailed logs for debugging and monitoring
- **Iterative Problem Solving**: Automatically breaks down complex problems into steps

## 🏗️ Architecture

```
┌─────────────┐
│   main.py   │ ← Orchestrates all modules
└──────┬──────┘
       │
       ├───► Perception.py ← Input processing & environment observation
       ├───► Memory.py ← State management & history tracking
       ├───► Decision_Making.py ← AI reasoning & decision generation
       └───► Action.py ← Tool execution & visualization
       
       ▼
       
example2.py (MCP Server) ← Provides 23+ tools for calculations & graphics
```

### Module Responsibilities

1. **Perception**: Processes user input, extracts facts, determines query type
2. **Memory**: Stores iterations, tool calls, results, and performance metrics
3. **Decision-Making**: Uses Gemini AI to analyze context and generate decisions
4. **Action**: Executes tools, handles visualization, manages execution flow

## 📦 Installation

### Prerequisites

- Python 3.10 or higher
- Google Gemini API key
- Windows OS (for Paint integration, optional)

### Setup Steps

1. **Clone the repository** (or use your existing directory):
```bash
cd Gemini4
```

2. **Create a virtual environment**:
```bash
python -m venv .venv

# On Windows
.venv\Scripts\activate

# On Unix/Mac
source .venv/bin/activate
```

3. **Install dependencies**:
```bash
# If using uv (recommended)
uv venv
uv pip install google-generativeai python-dotenv mcp pywinauto win32gui

# Or using pip
pip install google-generativeai python-dotenv mcp pywinauto pywin32
```

4. **Configure API key**:
Create a `config.env` file:
```env
GEMINI_API_KEY=your_actual_api_key_here
```

Get your API key from: https://makersuite.google.com/app/apikey

## 🚀 Usage

### Basic Usage

Run the agent system:
```bash
python main.py
```

The system will:
1. Process the predefined query about ASCII values in "INDIA"
2. Calculate the exponential sum
3. Display the Turtle graphics window with "TSAI" text
4. Close the window after 10 seconds

### Running Individual Modules

You can test individual modules:
```python
# Test Perception
from Perception import Perception
p = Perception('your_api_key')
data = await p.process_user_input("test query")

# Test Memory
from Memory import Memory
m = Memory()
m.store_iteration(1, "query", {}, "result")
print(m.get_memory_summary())
```

## 📁 Project Structure

```
Gemini4/
├── main.py                  # Main orchestration script
├── Perception.py            # Input processing module
├── Memory.py                # Memory and state management
├── Decision_Making.py       # AI decision generation
├── Action.py                # Tool execution module
├── example2.py              # MCP server with 23+ tools
├── config.env               # API key configuration (create this)
├── agent_logs.log           # Execution logs (auto-generated)
├── README.md                # This file
└── .venv/                   # Virtual environment
```

## 🔧 Modules

### Perception.py

**Purpose**: Process user input and observe the environment

**Key Methods**:
- `process_user_input(query)`: Extracts facts, identifies query type
- `observe_environment(context)`: Collects current state information
- `extract_facts_from_prompt()`: Parses instructions and requirements

**Output**: Dictionary with query type, key concepts, visualization needs, and prompt facts

### Memory.py

**Purpose**: Comprehensive state and history management

**Key Methods**:
- `store_iteration()`: Records each agent iteration
- `store_tool_call()`: Tracks tool executions
- `store_facts()`: Stores extracted facts by category
- `store_variable()`: Manages variables across scopes
- `track_method_call()`: Logs method invocations
- `get_memory_summary()`: Provides overview of stored data

**Data Store**: Uses `defaultdict`, `deque`, and standard dict for efficient storage

### Decision_Making.py

**Purpose**: AI-powered decision generation using Gemini

**Key Methods**:
- `generate_decision()`: Main decision generation entry point
- `_analyze_inputs()`: Analyzes perception and memory data
- `_build_enhanced_context_query()`: Constructs AI prompt
- `_parse_decision()`: Parses AI response into actions

**Output**: Decision type (function_call/final_answer) and structured decision data

### Action.py

**Purpose**: Execute decisions and manage tool calls

**Key Methods**:
- `execute_decision()`: Executes decision with memory integration
- `execute_tool()`: Calls MCP server tools
- `execute_visualization()`: Handles Turtle graphics
- `execute_complete_action()`: Orchestrates complete action flow

## 🛠️ Tools

The system includes 23+ tools through `example2.py`:

### Mathematical Operations
- `add(x, y)`: Addition
- `multiply(x, y)`: Multiplication
- `strings_to_chars_to_int(string)`: ASCII conversion
- `int_list_to_exponential_sum(int_list)`: Exponential sum
- And more...

### Visualization
- `draw_rectangle_with_turtle(width, height, text)`: Turtle graphics visualization

### Paint Integration (Windows)
- `open_paint_maximized()`: Open Paint in maximized mode
- `draw_rectangle_paint(width, height)`: Draw rectangle in Paint
- `add_text_in_paint(text)`: Add text to Paint canvas

## 💡 Examples

### Example 1: ASCII Conversion

**Input**: "Find ASCII values of INDIA"
**Process**:
1. Perception: Identifies query as mathematical
2. Decision-Making: Selects `strings_to_chars_to_int` tool
3. Action: Executes tool → Returns [73, 78, 68, 73, 65]
4. Memory: Stores result and iteration details

### Example 2: Exponential Sum

**Input**: "Sum of exponentials of [73, 78, 68, 73, 65]"
**Process**:
1. Decision-Making: Selects `int_list_to_exponential_sum` tool
2. Action: Executes tool → Returns `5.052393630276104e31`
3. Visualization: Opens Turtle window with "TSAI" text
4. Memory: Tracks all execution steps

## 📊 Logging

The system generates detailed logs in `agent_logs.log`:
- Perception processing steps
- Memory storage operations
- Decision generation reasoning
- Action execution results
- Performance metrics

Example log entry:
```
2025-10-27 00:47:05,852 - INFO - __main__ - Action result: ['5.052393630276104e31']
```

## 🐛 Troubleshooting

### Issue: "GEMINI_API_KEY not found"
**Solution**: Create `config.env` with your API key
```env
GEMINI_API_KEY=your_key_here
```

### Issue: "ModuleNotFoundError: No module named 'google'"
**Solution**: Install dependencies in virtual environment
```bash
.venv\Scripts\python.exe -m pip install google-generativeai
```

### Issue: Turtle window doesn't appear
**Solution**: Check if Turtle graphics is properly initialized. The window stays open for 10 seconds.

### Issue: Paint operations fail
**Solution**: Paint integration is Windows-specific. Use Turtle graphics instead.

### Issue: Decision parsing errors
**Solution**: The system includes fallback mechanisms. Check logs for detailed error information.

## 🔄 Execution Flow

1. **Initialization**: Load API key, create modules, connect to MCP server
2. **Perception**: Process user query, extract facts
3. **Decision**: Analyze context, generate AI-powered decision
4. **Action**: Execute tools, visualize results
5. **Memory**: Store iteration, update state
6. **Iteration**: Repeat until final answer or max iterations
7. **Termination**: Display results, close visualization

## 📈 Performance

- Average response time: ~1-2 seconds per iteration
- Memory efficiency: Uses bounded collections (deque with maxlen=1000)
- Log file rotation: Manual rotation recommended for production

## 🤝 Contributing

This project demonstrates:
- Modular agent architecture
- Integration with Gemini AI
- MCP (Model Context Protocol) implementation
- Comprehensive logging and monitoring
- State management patterns

## 📝 License

Educational/Research project - Free to use and modify

## 👤 Author

Created as part of AI agent development exercise

## 🙏 Acknowledgments

- Google Generative AI (Gemini) for AI capabilities
- MCP library for tool communication
- Python community for excellent libraries

---

**Status**: ✅ Production-ready for educational use

**Last Updated**: October 2024
