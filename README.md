# Evidence Based Medicine MCP

This is a Model Context Protocol (MCP) server for grounding LLM answers in up-to-date evidence-based medicine.

With this you can ask an LLM medical queries and receive answers which are based solely on validated, evidence-based medical information, with references to the original source material.

<!-- TODO: add example of how it can work. With screenshot / short video -->



## Installation

### Prerequisites

- **Node.js** (version 18.0.0 or higher)
- **npm** (comes with Node.js) or **yarn** for package management
- **MCP-compatible client** such as:
  - Claude Desktop (for desktop use)
  - Cursor IDE (for development environments)
  - Any other MCP-compatible LLM interface



### Steps

1. **Clone this repository**

    ```
    git clone https://github.com/chris-lovejoy/evidence-based-medicine-mcp
    cd evidence-based-medicine-mcp
    ```

2. **Connect to the MCP server**

    Copy the below json with the appropriate {{PATH}} values:

    ```
    {
        "mcpServers": {
            "evidence-based-medicine-mcp": {
                "command": "{{PATH_TO_NPX}}",  // Run 'which npx' and place the output here
                "args": [
                    "-y",
                    "tsx",
                    "{{PATH_TO_SRC}}/evidence-based-medicine-mcp/index.ts" // cd into the repo and run 'pwd'
                ]
            }
        }  
    }
    ```

    For Claude, save this as `claude_desktop_config.json` in your Claude Desktop configuration directory at:

    ```
    ~/Library/Application Support/Claude/claude_desktop_config.json
    ```

    For Cursor, save this as `mcp.json` in your Cursor configuration directory at:

    ```
    ~/.cursor/mcp.json
    ```

3. **Restart Claude Desktop / Cursor**

    Open Claude Desktop / restart Cursor and you should now see Evidence Based Medicine MCP as an available integration.



## How to Use

### Getting the LLM to use the MCP Server

This MCP server will typically be used by the LLM whenever a user asks for medical advice or mentions they want responses to be grounded on up-to-date medical information.

For example, questions such as "Please give me medical advice about X" or "What are the treatment options for my diabetes, based on the medical evidence" will typically trigger it.

However, asking for a direct answer (e.g., "What should for my back pain?") typically does not - the LLM opts to answer the question directly.


## How it Works

The server operates by using the following tools in sequence:

1. `return_available_topics`
    - Shows all the high-level topics for which guidance exists, enabling the LLM to select the most relevant topics to identify articles/guides from


2. `get_articles_for_topic`
    - Returns all article titles and URLs for selected topics

3. `return_full_content_for_articles`
    - Returns full article content for all articles selected by the LLM, while advising the LLM to ground it's answer in the evidence and include URLs to all the original articles


## Potential Future Work

This MCP Server is anchored on the comprehensive resources available from [Patient.info](https://patient.info/). Additional authoritative sources could be incorporated, including [UpToDate](https://www.uptodate.com/), [Cochrane Reviews](https://www.cochranelibrary.com/), [BMJ Best Practice](https://bestpractice.bmj.com/) and others.

