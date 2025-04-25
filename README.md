# Tavily Research System

## Overview

The project is a simple Python tool I created for web-based research automation, organization, and summarization. The tool uses the Tavily API to search for information, group results by topic, and generate a nicely-formatted read through.

- **Topic Grouping:** Scans titles and contents for keywords (e.g., innovation, algorithm) and assigns each result under a descriptive topic name. 
- **Markdown Report:** Combines summaries with topics and source links into a single Markdown document viewable in Colab or any Markdown viewer. 
- **User-Friendly:** Very simple to set up—it just works in virtually any Python 3.7+ environment. 

## Prerequisites

- **Python 3.7+**
- **Tavily API Key** (Store it as an environment variable called `TAVILY_API_KEY` or as a secret in Google Colab. 

## Install

1. **Clone the repo**:
   ```bash
   git clone https://github.com/your-username/tavily-research-system.git
   cd tavily-research-system
   ```
2. **Install dependencies**:
   ```bash
   pip install langchain-community tavily-python
   ```
3. **Set your API key**:
   - **Local**: `export TAVILY_API_KEY="YOUR_API_KEY"`
   - **Colab**: Go to **Edit → Notebook settings → Secrets** and add `TAVILY_API_KEY`.

## Usage

1. Open `research.py` in your editor or in a Colab notebook.
2. Run the script:
   ```bash
   python research.py
   ```
3. At the prompt, type in your question of search and hit Enter. In case you want to leave it blank, the default will be:
   > *What are the latest advancements in quantum computing?*
4. A Markdown report is printed to the console comprising the organized findings and a list of URL sources.

## Code Explanations

This is an attempt to gently touch on some of the main aspects of the code:

1. **`TavilyResearchSystem`**** class**

   - **`__init__`**: Initializes the search tool by your API key assigned during setup. It sets also, k=8, and advanced depth. 
   - **`search(query)`**: Interacts with the Tavily API, downloading raw results (title, URL, contents) and gracefully handling errors.
   - **`organize_by_topic(data)`**: It looks for keywords (such as "development" or "method") in each result's title or its first 200 characters of content before proceeding to group them. If no matches are found, it defaults to "General." 
   - **`generate_research_report(query)`**: Runs `search()`, then `organize_by_topic()`, and stitches together a Markdown report with:
     - **Summary**: Number of sources and query text.
     - **Topics**: Each topic section shows titles, source links, and the first 800 characters of content.
     - **Sources list** at the end.

2. **`main()`**** function**

   - Installs required packages if missing.
   - Reads the `TAVILY_API_KEY` from Colab secrets or environment.
   - Prompts the user for a query (with a default).
   - Runs the research system and displays the report using Jupyter’s Markdown renderer.

## Example Output

```markdown
# Research Report: Quantum Computing

## Summary
This report gathers insights from 8
