# MCP Client Agent

This agent acts as a client for an MCP (Model Context Protocol) server and is deployed to Google Cloud Agent Engine.

## Prerequisites

- Python 3.13 or later
- Google Cloud SDK (`gcloud`)

## Setup

1.  **Create a virtual environment**:
    ```bash
    python3 -m venv venv
    ```

2.  **Activate the virtual environment**:
    ```bash
    source venv/bin/activate
    ```

3.  **Install dependencies**:
    ```bash
    pip install -r requirements.txt
    ```

4.  **Authenticate with Google Cloud**:
    ```bash
    gcloud auth login
    gcloud auth application-default login
    ```

## Configuration

The agent is configured in `agent.py`. It connects to the MCP server at:
`https://mcp-weather-server-1005790925927.us-central1.run.app/sse`

If you need to change the URL or model, edit `agent.py`.

## Deployment

To deploy the agent to Agent Engine, run the following command from the directory containing `agent.py`:

```bash
PROJECT_ID=your-project-id
LOCATION_ID=us-central1
./venv/bin/adk deploy agent_engine \
  --project=$PROJECT_ID \
  --region=$LOCATION_ID \
  --display_name="MCP Weather Client" \
  .
```

*Note: Replace `your-project-id` with your actual Google Cloud Project ID.*
