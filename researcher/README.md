# Researcher Crew

A multi-agent research and reporting system built with **CrewAI**. The project uses two specialized AI agents that collaborate to research a given topic and transform the findings into a detailed, structured report.

## Project Description

The **Researcher Crew** consists of two sequential agents:

1. **Senior Data Researcher** — searches for and identifies the most relevant and up-to-date information about a given topic.
2. **Reporting Analyst** — reviews the research findings and expands them into a comprehensive report, organizing the information into clear sections.

The workflow is:

```text
Topic
  ↓
Senior Data Researcher
  ↓
10 key research findings
  ↓
Reporting Analyst
  ↓
Detailed Markdown Report
```

The project demonstrates **multi-agent orchestration with CrewAI**, where each agent has a specific responsibility and the output of the research agent is passed as context to the reporting agent.

## Models Used

Both agents use **NVIDIA Nemotron 3 Super 120B A12B** through **OpenRouter**:

```text
openrouter/nvidia/nemotron-3-super-120b-a12b:free
```

### Researcher

**Role:** Senior Data Researcher

The researcher is responsible for:

* Investigating the requested topic
* Finding recent and relevant information
* Considering the current year when conducting research
* Selecting the 10 most relevant findings

### Reporting Analyst

**Role:** Reporting Analyst

The reporting analyst receives the researcher's findings as context and is responsible for:

* Reviewing the collected information
* Expanding each finding into a detailed section
* Organizing the information into a coherent report
* Producing the final report in Markdown format

## Tech Stack

* **Python** — Programming language
* **CrewAI** — Multi-agent orchestration framework
* **OpenRouter** — LLM API provider
* **NVIDIA Nemotron 3 Super 120B A12B** — LLM
* **uv** — Python dependency and environment management
* **YAML** — Agent and task configuration

## Installation

### Prerequisites

Make sure you have:

* Python `>=3.10, <3.14`
* An OpenRouter API key
* `uv` installed

### 1. Install uv

If you don't already have `uv`:

```bash
pip install uv
```

You can also follow the official `uv` installation instructions.

### 2. Clone the repository

```bash
git clone <your-repository-url>
cd researcher
```

### 3. Install dependencies

Create the virtual environment and install the project's dependencies using:

```bash
uv sync
```

Alternatively, if you're using the CrewAI CLI:

```bash
crewai install
```

### 4. Configure your API key

Create a `.env` file in the project root:

```env
OPENROUTER_API_KEY=your_openrouter_api_key
```

**Do not commit your `.env` file or API keys to GitHub.**

## Configuration

### Agents

Agent definitions are located in:

```text
src/researcher/config/agents.yaml
```

The project currently contains:

* `researcher`
* `reporting_analyst`

You can modify their roles, goals, backstories, and LLM configuration from this file.

### Tasks

Task definitions are located in:

```text
src/researcher/config/tasks.yaml
```

The workflow consists of:

* `research_task` — researches the requested topic
* `reporting_task` — uses the research task's output as context to generate the final report

### Customizing the Topic

The topic can be provided through the project's main entry point:

```text
src/researcher/main.py
```

The project uses the following inputs:

* `topic`
* `current_year`

These values are passed to the agents and tasks through CrewAI's configuration system.

## Running the Project

From the project root, run:

```bash
crewai run
```

The crew will:

1. Receive the research topic.
2. Run the Senior Data Researcher.
3. Collect 10 relevant findings.
4. Pass the findings to the Reporting Analyst.
5. Generate a detailed Markdown report.

The generated report is saved as:

```text
report.md
```

## Project Structure

```text
researcher/
├── knowledge/
├── src/
│   └── researcher/
│       ├── config/
│       │   ├── agents.yaml
│       │   └── tasks.yaml
│       ├── crew.py
│       └── main.py
├── tests/
├── .gitignore
├── .python-version
├── pyproject.toml
├── README.md
└── uv.lock
```

## CrewAI Concepts Demonstrated

This project demonstrates:

* Multi-agent systems
* Agent specialization
* Sequential task execution
* Task context passing
* YAML-based agent configuration
* YAML-based task configuration
* LLM integration through OpenRouter
* Automated report generation
* Dependency management with `uv`
