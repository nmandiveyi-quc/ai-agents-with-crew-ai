# CrewAI: AI Agent Orchestration Framework

CrewAI is a Python framework for building and orchestrating AI agent teams. It enables developers to create multiple specialized AI agents that can collaborate on complex tasks. Each agent can have distinct roles, behaviors, tools, and memory, allowing for dynamic and coordinated workflows.

## Key Features of CrewAI:
- **Multi-Agent Collaboration** – Allows multiple AI agents to work together on tasks.
- **Role-Based Specialization** – Agents can be assigned different roles with specific expertise.
- **Task Orchestration** – Tasks can be assigned in sequences or in parallel.
- **Integration with LLMs & Tools** – Works with various large language models (LLMs) and external tools.
- **Memory & State Management** – Agents can remember past interactions to improve performance.

## Using CrewAI to orchestrate and agentic architecture - AI Research Team with CrewAI

In this example, we use **CrewAI** to create an AI-driven research team. The team consists of three specialized agents:

1. **Researcher Agent** – Gathers information on a topic.
2. **Writer Agent** – Summarizes the research findings.
3. **Reviewer Agent** – Reviews and improves the summary.

## Installation

First, install the CrewAI package:

```bash
pip install crewai
```
## Define the LLM model
```python
from langchain.chat_models import ChatOpenAI

# Initialize OpenAI model
llm = ChatOpenAI(model_name="gpt-4", temperature=0.7)
```

## Define the agents
```python
from crewai import Agent

# Researcher Agent
researcher = Agent(
    role="Researcher",
    goal="Gather relevant and accurate information on a given topic.",
    backstory="A highly skilled researcher with expertise in analyzing data and finding key insights.",
    verbose=True,
    llm=llm
)

# Writer Agent
writer = Agent(
    role="Writer",
    goal="Summarize research findings into a clear, well-structured report.",
    backstory="A professional writer who excels in crafting informative and engaging summaries.",
    verbose=True,
    llm=llm
)

# Reviewer Agent
reviewer = Agent(
    role="Reviewer",
    goal="Review the summary and suggest improvements for clarity and coherence.",
    backstory="An experienced editor with a keen eye for details and quality writing.",
    verbose=True,
    llm=llm
)
```

## Define Tasks
```python
from crewai import Task

# Research Task
research_task = Task(
    description="Find the latest developments in AI-driven travel booking systems.",
    agent=researcher
)

# Writing Task
writing_task = Task(
    description="Write a structured summary based on the research findings.",
    agent=writer
)

# Reviewing Task
reviewing_task = Task(
    description="Review and improve the summary to ensure clarity and quality.",
    agent=reviewer
)
```

# Creating and running the crew
```python
from crewai import Crew

# Define the Crew with agents and tasks
ai_research_crew = Crew(
    agents=[researcher, writer, reviewer],
    tasks=[research_task, writing_task, reviewing_task]
)

# Run the Crew
results = ai_research_crew.kickoff()
print(results)
```

## Explanation

1. **The Researcher Agent** gathers information on AI-driven travel booking.  
2. **The Writer Agent** summarizes the research findings.  
3. **The Reviewer Agent** refines the summary for clarity and quality.  
4. **The Final Report** is produced and printed as output.  