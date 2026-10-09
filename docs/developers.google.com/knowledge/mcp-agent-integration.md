---
name: documents/developers.google.com/knowledge/mcp-agent-integration
uri: https://developers.google.com/knowledge/mcp-agent-integration
title: Integrate Developer Knowledge MCP server with custom AI agents
description: The Developer Knowledge API and MCP server provide access to Google's developer knowledge.
data_source: developers.google.com
---

This tutorial shows you how to connect the remote Developer Knowledge MCP server to custom AI agent frameworks built with LangChain, LlamaIndex, and AutoGen.

By connecting your custom AI agents to the remote Model Context Protocol (MCP) server, your agents can dynamically search and retrieve authoritative, up-to-date Google developer documentation covering Google Cloud, Firebase, Android, Google Maps Platform, Chrome, and more.

## Prerequisites

Complete the following prerequisites before you begin:

1.  **Generate a Developer Knowledge API key** : enable the Developer Knowledge API and create an API key in your Google Cloud project by following the [API key setup guide](https://developers.google.com/knowledge/mcp#api-key-setup) .

2.  **Generate a Gemini API key** : create an API key in [Google AI Studio](https://aistudio.google.com/apikey) to authenticate Gemini models, or reuse your Google Cloud API key if the Generative Language API is enabled on it.

3.  **Set your environment variables** : set your API keys as environment variables in your terminal:

    ```
    export DEVELOPERKNOWLEDGE_API_KEY="YOUR_API_KEY"
    export GEMINI_API_KEY="YOUR_GEMINI_API_KEY"
    ```

4.  **Install Python** : verify that your development environment uses Python 3.10 or higher.

## Connect using LangChain

LangChain applications can connect to remote HTTP MCP servers using the `langchain-mcp-adapters` package or standard MCP client transports.

### Install dependencies

Install the required Python packages for LangChain, Gemini, and MCP:

```
pip install langgraph langchain-google-genai langchain-mcp-adapters mcp
```

### Configure the LangChain agent

The following example connects the Developer Knowledge MCP server to a LangChain ReAct agent powered by Gemini. The script instantiates `MultiServerMCPClient` using the `streamable_http` transport, attaches the `X-Goog-Api-Key` HTTP header, and loads the remote tools into `create_react_agent` :

```
import asyncio
import os

from langchain_google_genai import ChatGoogleGenerativeAI
from langchain_mcp_adapters.client import MultiServerMCPClient
from langgraph.prebuilt import create_react_agent

async def run_langchain_agent():
    api_key = os.environ.get("DEVELOPERKNOWLEDGE_API_KEY")
    if not api_key:
        raise ValueError(
            "DEVELOPERKNOWLEDGE_API_KEY environment variable is required."
        )

    gemini_api_key = os.environ.get("GEMINI_API_KEY")
    if not gemini_api_key:
        raise ValueError("GEMINI_API_KEY environment variable is required.")

    # Configure remote MCP connection for Developer Knowledge
    client = MultiServerMCPClient(
        {
            "google-developer-knowledge": {
                "url": "https://developerknowledge.googleapis.com/mcp",
                "transport": "streamable_http",
                "headers": {
                    "X-Goog-Api-Key": api_key,
                },
            }
        }
    )
    tools = await client.get_tools()

    # Initialize Gemini model and ReAct agent
    llm = ChatGoogleGenerativeAI(
        model="gemini-2.5-flash",
        temperature=0,
        google_api_key=gemini_api_key,
    )
    agent = create_react_agent(llm, tools)

    # Run agent query
    response = await agent.ainvoke(
        {
            "messages": [
                (
                    "user",
                    "How do I list Google Cloud Storage buckets in Python?",
                )
            ]
        }
    )
    print("\nAgent Response:\n", response["messages"][-1].content)

if __name__ == "__main__":
    asyncio.run(run_langchain_agent())
```

## Connect using LlamaIndex

LlamaIndex supports MCP server integration through tool specifications, allowing retrieval agents to query Developer Knowledge documents during reasoning.

### Install dependencies

Install the LlamaIndex core packages, Gemini LLM, and MCP tools integration:

```
pip install llama-index llama-index-tools-mcp llama-index-llms-google-genai
```

### Configure the LlamaIndex agent

The following example connects to the remote MCP server using `BasicMCPClient` , wraps it with `McpToolSpec` , and binds the retrieved tools to a LlamaIndex `FunctionAgent` powered by Gemini:

```
import asyncio
import os

from llama_index.core.agent.workflow import FunctionAgent
from llama_index.llms.google_genai import GoogleGenAI
from llama_index.tools.mcp import BasicMCPClient, McpToolSpec

async def run_llamaindex_agent():
    api_key = os.environ.get("DEVELOPERKNOWLEDGE_API_KEY")
    if not api_key:
        raise ValueError(
            "DEVELOPERKNOWLEDGE_API_KEY environment variable is required."
        )

    gemini_api_key = os.environ.get("GEMINI_API_KEY")
    if not gemini_api_key:
        raise ValueError("GEMINI_API_KEY environment variable is required.")

    # Connect to the remote Developer Knowledge MCP endpoint
    mcp_client = BasicMCPClient(
        "https://developerknowledge.googleapis.com/mcp",
        headers={"X-Goog-Api-Key": api_key},
    )
    mcp_tool_spec = McpToolSpec(client=mcp_client)
    tools = await mcp_tool_spec.to_tool_list_async()

    # Create LlamaIndex FunctionAgent with Gemini
    llm = GoogleGenAI(model="gemini-2.5-flash", api_key=gemini_api_key)
    agent = FunctionAgent(tools=tools, llm=llm)

    # Query the agent
    response = await agent.run(
        "What are the default limits and quotas for the Developer Knowledge"
        " API?"
    )
    print("\nAgent Response:\n", str(response))

if __name__ == "__main__":
    asyncio.run(run_llamaindex_agent())
```

## Connect using AutoGen

Microsoft AutoGen agents can interface with remote MCP servers using the `autogen-ext` MCP extension, enabling multi-agent collaboration with access to official Google developer documentation.

### Install dependencies

Install AutoGen core and MCP extension packages:

```
pip install autogen-agentchat "autogen-ext[mcp,openai]"
```

### Configure the AutoGen agent

The following example connects to the remote MCP server using `StreamableHttpServerParams` and registers Developer Knowledge tools with an AutoGen `AssistantAgent` powered by Gemini:

```
import asyncio
import os

from autogen_agentchat.agents import AssistantAgent
from autogen_agentchat.teams import RoundRobinGroupChat
from autogen_ext.models.openai import OpenAIChatCompletionClient
from autogen_ext.tools.mcp import StreamableHttpServerParams, mcp_server_tools

async def run_autogen_agent():
    api_key = os.environ.get("DEVELOPERKNOWLEDGE_API_KEY")
    if not api_key:
        raise ValueError(
            "DEVELOPERKNOWLEDGE_API_KEY environment variable is required."
        )

    gemini_api_key = os.environ.get("GEMINI_API_KEY")
    if not gemini_api_key:
        raise ValueError("GEMINI_API_KEY environment variable is required.")

    # Retrieve remote MCP tools for Developer Knowledge by using Streamable HTTP
    server_params = StreamableHttpServerParams(
        url="https://developerknowledge.googleapis.com/mcp",
        headers={"X-Goog-Api-Key": api_key},
    )
    dk_tools = await mcp_server_tools(server_params)

    # Initialize model client with Gemini and assistant agent
    model_client = OpenAIChatCompletionClient(
        model="gemini-2.5-flash",
        api_key=gemini_api_key,
        base_url="https://generativelanguage.googleapis.com/v1beta/openai/",
    )
    developer_assistant = AssistantAgent(
        name="google_docs_assistant",
        model_client=model_client,
        tools=dk_tools,
        system_message=(
            "You are a developer assistant specializing in Google APIs and"
            " SDKs. Use Developer Knowledge tools to retrieve verified"
            " documentation."
        ),
    )

    # Run query with team runner
    team = RoundRobinGroupChat([developer_assistant], max_turns=5)
    stream = team.run_stream(
        task=(
            "Explain how to configure Firebase Cloud Messaging topic"
            " subscriptions."
        )
    )

    async for message in stream:
        print(message)

if __name__ == "__main__":
    asyncio.run(run_autogen_agent())
```

## Best practices for agent integration

When building custom AI agents with the Developer Knowledge MCP server, follow these guidelines:

- **Refine search queries** : include specific product names and relevant keywords in the natural language query rather than generic terms, because the `search_documents` and `answer_query` tools match on query semantics.
- **Manage context window tokens** : use `answer_query` for direct answers drawn from the documentation corpus, and avoid requesting full page contents with `get_documents` unless snippet details from `search_documents` are insufficient.
- **Secure API keys** : store your Developer Knowledge API and Gemini API keys in environment variables or standard secret management systems, and never hardcode credentials in code.

## What's next

Explore the following resources to learn more about the Developer Knowledge MCP server:

- Read the complete [Developer Knowledge MCP server installation guide](https://developers.google.com/knowledge/mcp) .
- Review the available [corpus domains](https://developers.google.com/knowledge/reference/corpus-reference) .
- Learn how to [generate answers from documentation](https://developers.google.com/knowledge/answer-query) .
