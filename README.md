A modular AI agent system built with Google's Gemini API, implementing Perception, Memory, Decision-Making, and Action modules to solve complex problems through iterative reasoning.

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Architecture](#architecture)
- [Installation](#installation)
- [Usage](#usage)
- [Project Structure](#project-structure)
- [Modules](#modules)
  - [main.py](#mainpy)
  - [Perception.py](#perceptionpy)
  - [Memory.py](#memorypy)
  - [Decision_Making.py](#decision_makingpy)
  - [Action.py](#actionpy)
- [Execution Flow](#execution-flow)
- [Logging](#logging)

## 🎯 Overview

GPTAssingment6 is an intelligent agent system that leverages Google's Gemini AI to process queries through four core modules:

- **Perception**: Analyzes and extracts information from user queries
- **Memory**: Maintains state and history across iterations
- **Decision-Making**: Uses AI to generate informed decisions
- **Action**: Executes decisions and manages tool calls

The system orchestrates these modules through `main.py` to solve complex problems iteratively.

### Example Use Case

**Query:** "Find the ASCII values of characters in INDIA and then return sum of exponentials of those values"

**Solution:** The agent will:
1. **Perception**: Identify query type (mathematical) and extract key concepts
2. **Decision-Making**: Select appropriate tools to solve the problem
3. **Action**: Execute tools to calculate ASCII values and exponential sum
4. **Memory**: Store iterations and results for context-aware reasoning

## ✨ Features

- **Modular Architecture**: Clean separation of concerns across five core modules
- **Intelligent Reasoning**: Uses Gemini AI for step-by-step problem solving
- **Memory Management**: Tracks iterations, tool calls, and execution history
- **State Persistence**: Maintains context across multiple iterations
- **Comprehensive Logging**: Detailed logs for debugging and monitoring
- **Iterative Problem Solving**: Automatically breaks down complex problems into steps

## 🏗️ Architecture

```
┌─────────────────────────────────────────┐
│           main.py                       │
│  (Orchestrates all modules)             │
└──────────────┬──────────────────────────┘
               │
       ┌───────┴───────┬──────────┬──────────┐
       │               │          │          │
       ▼               ▼          ▼          ▼
┌──────────┐    ┌──────────┐  ┌──────────┐  ┌──────────┐
│Perception│    │  Memory  │  │ Decision │  │  Action  │
│   .py    │    │   .py    │  │_Making.py│  │   .py    │
└──────────┘    └──────────┘  └──────────┘  └──────────┘
```

### Module Responsibilities

1. **main.py**: Orchestrates execution flow, manages MCP server connection
2. **Perception.py**: Processes user input, extracts facts, determines query type
3. **Memory.py**: Stores iterations, tool calls, results, and performance metrics
4. **Decision_Making.py**: Uses Gemini AI to analyze context and generate decisions
5. **Action.py**: Executes tools, handles visualization, manages execution flow

## 📦 Installation

### Prerequisites

- Python 3.10 or higher
- Google Gemini API key

### Setup Steps

1. **Install dependencies**:
```bash
pip install google-generativeai python-dotenv mcp
```

2. **Configure API key**:
Create a `config.env` file:
```env
GEMINI_API_KEY=your_actual_api_key_here
```

Get your API key from: https://makersuite.google.com/app/apikey

## 🚀 Usage

Run the agent system:
```bash
python main.py
```

The system will process queries iteratively, making decisions based on context and executing appropriate actions.

## 📁 Project Structure

```
Gemini4/
├── main.py                  # Main orchestration script
├── Perception.py            # Input processing module
├── Memory.py                # Memory and state management
├── Decision_Making.py       # AI decision generation
├── Action.py                # Tool execution module
├── config.env               # API key configuration (create this)
├── agent_logs.log           # Execution logs (auto-generated)
└── README.md                # This file
```

## 🔧 Modules

### main.py

**Purpose**: Orchestrates the complete agent execution flow

**Key Responsibilities**:
- Initializes all modules (Perception, Memory, Decision-Making, Action)
- Establishes connection to MCP server
- Manages main execution loop
- Coordinates data flow between modules
- Handles iteration control and termination

**Key Components**:
- `AgentSystem`: Main orchestrator class
- `run()`: Sets up MCP connection and starts execution
- `_execute_main_loop()`: Core execution loop with module coordination

### Perception.py

**Purpose**: Process user input and observe the environment

**Key Methods**:
- `process_user_input(query)`: Extracts facts, identifies query type
- `observe_environment(context)`: Collects current state information
- `extract_facts_from_prompt()`: Parses instructions and requirements
- `get_student_prompt(tools_description)`: Formats prompt with tools

**Output**: Dictionary containing:
- Query type (mathematical, visual, etc.)
- Key concepts and keywords
- Visualization requirements
- Prompt facts and requirements

### Memory.py

**Purpose**: Comprehensive state and history management

**Key Methods**:
- `store_iteration()`: Records each agent iteration
- `store_tool_call()`: Tracks tool executions
- `store_facts()`: Stores extracted facts by category
- `store_variable()`: Manages variables across scopes
- `track_method_call()`: Logs method invocations
- `get_memory_summary()`: Provides overview of stored data

**Data Store**: Uses efficient data structures:
- `defaultdict` for categorized data
- `deque` with maxlen=1000 for bounded history
- Standard dict for key-value pairs

### Decision_Making.py

**Purpose**: AI-powered decision generation using Gemini

**Key Methods**:
- `generate_decision()`: Main decision generation entry point
- `_analyze_inputs()`: Analyzes perception and memory data
- `_build_enhanced_context_query()`: Constructs AI prompt
- `_parse_decision()`: Parses AI response into actions

**Output**: 
- Decision type (`function_call` or `final_answer`)
- Structured decision data (function name, arguments, or final answer)

### Action.py

**Purpose**: Execute decisions and manage tool calls

**Key Methods**:
- `execute_decision()`: Executes decision with memory integration
- `execute_tool()`: Calls external tools via MCP server
- `execute_visualization()`: Handles visualization tasks
- `execute_complete_action()`: Orchestrates complete action flow

## 🔄 Execution Flow

1. **Initialization** (`main.py`):
   - Load API key from `config.env`
   - Initialize all modules
   - Connect to MCP server

2. **Perception** (`Perception.py`):
   - Process user query
   - Extract facts and identify query type
   - Determine visualization needs

3. **Memory** (`Memory.py`):
   - Store query and facts
   - Retrieve iteration history
   - Track performance metrics

4. **Decision-Making** (`Decision_Making.py`):
   - Analyze context from Perception and Memory
   - Generate AI-powered decision
   - Return function call or final answer

5. **Action** (`Action.py`):
   - Execute the decision
   - Call appropriate tools
   - Handle visualization if needed

6. **Memory Update**:
   - Store iteration results
   - Update performance metrics
   - Prepare for next iteration

7. **Iteration**: Repeat steps 2-6 until completion or max iterations

8. **Termination**: Display results and exit

## 📊 Logging

The system generates detailed logs in `agent_logs.log`:

- Perception processing steps
- Memory storage operations
- Decision generation reasoning
- Action execution results
- Performance metrics

Logs follow this format:
```
TIMESTAMP - LEVEL - MODULE - MESSAGE
```

Example:
```
2025-10-27 00:47:05,852 - INFO - __main__ - Action result: ['5.052393630276104e31']
```

## 🤝 Contributing

This project demonstrates:
- Modular agent architecture
- Integration with Gemini AI
- MCP (Model Context Protocol) implementation
- Comprehensive logging and monitoring
- State management patterns

## 📝 License

Educational/Research project - Free to use and modify

## 🙏 Acknowledgments

- Google Generative AI (Gemini) for AI capabilities
- MCP library for tool communication
- Python community for excellent libraries

---

**Status**: ✅ Production-ready for educational use

**Last Updated**: October 2024
