# MCP Client Agent

This agent acts as a client for an MCP (Model Context Protocol) server and is deployed
 to Google Cloud Agent Engine.

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

To deploy the agent to Agent Engine without exceeding the payload size limit (which ha
ppens if the local `venv` directory is uploaded), do not deploy directly from the root
 directory with `.`. Instead, create a temporary clean directory, copy only the requir
ed files, and deploy from there.

Run the following commands:

```bash
PROJECT_ID=your-project-id
LOCATION_ID=us-central1

# 1. Create a temporary clean directory for deployment
mkdir -p /tmp/weather_deploy

# 2. Copy only required agent files
cp agent.py requirements.txt __init__.py /tmp/weather_deploy/

# 3. Deploy the agent from the temporary directory using adk in the venv
./venv/bin/adk deploy agent_engine \
  --project=$PROJECT_ID \
  --region=$LOCATION_ID \
  --display_name="MCP Weather Client" \
  /tmp/weather_deploy

# 4. Clean up the temporary directory
rm -rf /tmp/weather_deploy
```

*Note: Replace `your-project-id` with your actual Google Cloud Project ID.*
