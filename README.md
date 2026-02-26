# MCP Server for Network Engineers

## Description:

By the end of this lab, students will understand how to use MCP Server to connect to your Network Devices and work with them using AI prompt.

## Agenda

1. Setup MCP client and MCP Server on your laptop
2. Integrate the MCP Server with the MCP Client
3. Try using some prompts to test the interaction between LLM and external device

## Pre-requisite

1. Basic understanding of AI and MCP Servers
2. Knowledge of working on MAC terminal or Windows command prompt
3. Understanding of Generative AI concepts like Prompt Engineering
5. Access to laptop.

# Tasks

1. Download "Claude Desktop" as MCP client and "Netmiko" as MCP Server and related dependencies/prerequisites
2. Enable this Netmiko MCP Server on Claude Desktop
3. Try using some prompts to test the interaction between LLM and Linux Server or ASR9K device

## ⚙️ Set Up Your Environment

### 1. Install `winget` or `brew`

winget is the command-line tool for Windows Package Manager, which allows users to discover, install, upgrade, and remove applications on Windows.
Homebrew installs the stuff you need that Apple (or your Linux system) didn’t.

Install "winget" on Windows or "brew" on MacOS if not already installed

Windows:

Download and install winget

    https://learn.microsoft.com/en-us/windows/package-manager/winget/

MacOS/Linux:

Open terminal and execute below commands to install brew

    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

### 2. Install `uv`

uv is an extremely fast Python package and project manager.
We are using uv to run our python script (MCP Server).

Windows:

Run below command from windows command promt

    winget install --id=astral-sh.uv  -e

MacOS/Linux:

    brew install uv

### 3. Install `git`

Windows:

    winget install --id Git.Git -e --source winget

MacOS/Linux:

    brew install git

> 🔁 Restart your terminal to ensure the `uv` and `git` command is available.

### 4. Install `Build Tools`

Windows:

    winget install -e --id Microsoft.VisualStudio.2022.BuildTools

MacOS/Linux:

    # No action required - build tools are already installed wit OS


### 5. Install Claude Desktop

1. Download and install Claud Desktop from https://claude.com/download
2. Sign up using your Google Account or any other possible means if you dont already have an account
3. Sign-in into your Claude account

### 6. Configure and Run Netmiko MCP Server

Windows: 

```console
# Open command line in administrator mode. Type "cmd" in Run and Right Click on Application Icon and select option to "Run as Administrator"
cmd

# Creat local directory where you want to make a local copy of the git code and change to that directory
mkdir C:\git
cd C:\git

git clone https://github.com/upa/mcp-netmiko-server
cd mcp-netmiko-server

# Fetch sample toml file that lists your devices eg. my-devices.network.toml
curl -LJO https://wwwin-github.cisco.com/raw/nipc/CX-Lighhouse-AI-Labs/refs/heads/MCP-Server-for-Network-Engineers/my-devices.network.toml

# Run via stdio and test that MCP server is running
uv run --python 3.13.9 --with "mcp[cli]" --with netmiko main.py my-devices.network.toml

# If command runs and stops at a blank screen, the MCP server is running successfully
# Exit the process by pressing Ctrl + C

```


MacOS/Linux:

```console
mkdir git
cd git

git clone https://github.com/upa/mcp-netmiko-server
cd mcp-netmiko-server

# Fetch sample toml file that lists your devices eg. eg. my-devices.network.toml
curl -LJO  https://wwwin-github.cisco.com/raw/nipc/CX-Lighhouse-AI-Labs/refs/heads/MCP-Server-for-Network-Engineers/my-devices.network.toml

# Run via stdio and test that MCP server is running
uv run --python 3.13.9 --with "mcp[cli]" --with netmiko main.py my-devices.network.toml

# If command runs and stops at a blank screen, the MCP server is running successfully
# Exit the process by pressing Ctrl + C

```



### 7. Check the path to uv executable

Windows:

    where uv

MacOS/Linux:

    which uv



### 8. Configure Netmiko MCP Server in Claude Desktop App (Claude app acts as MCP Client)

1.  Start the Claude Desktop App
2.  Click on File > Settings > Developer > Edit Config
3.  Edit the claude desktop config json and replace/add the contents as per below.
Note for Windows: **Update** the **path to uv **executable as per above step (See in bold below for Windows)
Note dor MacOS :  **Update** the **path to git folder** as per your username on MacOS (See in bold below for MacOS)

Windows:

```json
{
  "mcpServers": {
    "netmiko server": {
      "command": "C:/Users/**ashingal**/.local/bin/uv.exe",
      "args": [
        "run",
        "--python",
        "3.13.9",
        "--with",
        "mcp[cli]",
        "--with",
        "netmiko",
        "--directory",
        "C:/git/mcp-netmiko-server",
        "main.py",
        "my-devices.network.toml"
      ]
    }
  }
}
```

MacOS:

```json
{
  "mcpServers": {
    "netmiko server": {
      "command": "/opt/homebrew/bin/uv",
      "args": [
        "run",
        "--python",
        "3.13.9",
        "--with",
        "mcp[cli]",
        "--with",
        "netmiko",
        "--directory",
        "/Users/**masavali**/git/mcp-netmiko-server",
        "main.py",
        "my-devices.network.toml"
      ]
    }
  }
}
```

### 9. Restart computer if required

Windows:

    Restart Windows.

MacOS:

    Restart the Claude Desktop App - so that it reloads the new configuration.
    

### 10. Open Claude Desktop and verify MCP Server is enabled

1. Open Claude Desktop App.
2. Click on icon circled in red below and verify that MCP server is enabled as shown circled in yellow below

![image](https://wwwin-github.cisco.com/nipc/CX-Lighhouse-AI-Labs/assets/25303/49243cdd-2c9b-4156-8ebf-a8185a6f1394)

### 10. Test the interaction between LLM and Linux Server or ASR9K device

1. Sample toml file already contains a Linux Server called linux1 and an ASR9K call asr9k1
2. Test integration with these devices using prompts like:
   
   "what is the cpu utilization on linux1 ?"

   "how much free memory is available on linux1 ?"

   "how many interfaces are defined on asr9k1 ?"

   "what is the banner configured on asr9k1 ?"

4. Click on "Allow" when prompted to allow MCP Server tool to be triggered for the shown command execution

