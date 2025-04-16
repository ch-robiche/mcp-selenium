# MCP Selenium Server

<a href="https://glama.ai/mcp/servers/s2em7b2kwf">
  <img width="380" height="200" src="https://glama.ai/mcp/servers/s2em7b2kwf/badge" />
</a>

[![smithery badge](https://smithery.ai/badge/@angiejones/mcp-selenium)](https://smithery.ai/server/@angiejones/mcp-selenium)

A Model Context Protocol (MCP) server implementation for Selenium WebDriver, enabling browser automation through standardized MCP clients.

## Video Demo (Click to Watch)

[![Watch the video](https://img.youtube.com/vi/mRV0N8hcgYA/sddefault.jpg)](https://youtu.be/mRV0N8hcgYA)


## Features

- Start browser sessions with customizable options
- Navigate to URLs
- Find elements using various locator strategies
- Click, type, and interact with elements
- Perform mouse actions (hover, drag and drop)
- Handle keyboard input
- Take screenshots
- Upload files
- Support for headless mode

## Supported Browsers

- Chrome
- Firefox

## Selenium Grid Support

This MCP server can connect to a Selenium Grid instance for distributed browser automation. To use with Selenium Grid:

1. Provide the `gridUrl` parameter in the browser options to connect to your Selenium Grid hub
2. Optionally specify `platform` and `browserVersion` to request specific capabilities
3. The Selenium Grid handles browser session management, allowing for better scalability and parallel test execution

## LambdaTest Support

This MCP server also supports LambdaTest for cross-browser testing in the cloud:

1. Provide your LambdaTest credentials using `ltUsername` and `ltAccessKey` parameters
2. Optionally specify additional LambdaTest capabilities:
   - `platform` and `browserVersion` to select specific environments
   - `ltBuild` and `ltTestName` for better test organization
   - `ltNetwork`, `ltConsole`, and `ltVideo` for enhanced logging and recording
   - `ltTunnel` for testing internal or localhost websites

## Use with Claude

### Add to Claude Desktop

Add the Selenium MCP server to your Claude Desktop configuration:

1. Open your Claude Desktop configuration file
2. Add the following configuration:

```json
{
  "mcpServers": {
    "selenium": {
      "command": "npx",
      "args": ["-y", "@angiejones/mcp-selenium"]
    }
  }
}
```

### Use with other MCP clients
```json
{
  "mcpServers": {
    "selenium": {
      "command": "npx",
      "args": ["-y", "@angiejones/mcp-selenium"]
    }
  }
}
```

---

## Development

To work on this project:

1. Clone the repository
2. Install dependencies: `npm install`
3. Run the server: `npm start`

### Installation

#### Installing via Smithery

To install MCP Selenium for Claude Desktop automatically via [Smithery](https://smithery.ai/server/@angiejones/mcp-selenium):

```bash
npx -y @smithery/cli install @angiejones/mcp-selenium --client claude
```

#### Manual Installation
```bash
npm install -g @angiejones/mcp-selenium
```


### Usage

Start the server by running:

```bash
mcp-selenium
```

Or use with NPX in your MCP configuration:

```json
{
  "mcpServers": {
    "selenium": {
      "command": "npx",
      "args": [
        "-y",
        "@angiejones/mcp-selenium"
      ]
    }
  }
}
```



## Tools

### start_browser
Launches a browser session.

**Parameters:**
- `browser` (required): Browser to launch
  - Type: string
  - Enum: ["chrome", "firefox"]
- `options`: Browser configuration options
  - Type: object
  - Properties:
    - Local WebDriver options:
      - `headless`: Run browser in headless mode
        - Type: boolean
      - `arguments`: Additional browser arguments
        - Type: array of strings
    
    - Standard Selenium Grid options:
      - `gridUrl`: Selenium Grid hub URL
        - Type: string
        - Example: "http://selenium-hub:4444/wd/hub"
      - `platform`: Desired platform capability
        - Type: string
        - Example: "WINDOWS", "LINUX", "MAC"
      - `browserVersion`: Specific browser version to request from Grid
        - Type: string
        - Example: "114.0"
    
    - LambdaTest specific options:
      - `ltUsername`: LambdaTest username
        - Type: string
      - `ltAccessKey`: LambdaTest access key
        - Type: string
      - `ltBuild`: Build name for test organization
        - Type: string
      - `ltTestName`: Test name for reporting
        - Type: string
      - `ltNetwork`: Enable network logs
        - Type: boolean
      - `ltConsole`: Enable console logs
        - Type: boolean
      - `ltVideo`: Enable video recording
        - Type: boolean
      - `ltTunnel`: Enable LambdaTest tunnel for testing internal websites
        - Type: boolean

**Example (Local):**
```json
{
  "tool": "start_browser",
  "parameters": {
    "browser": "chrome",
    "options": {
      "headless": true,
      "arguments": ["--no-sandbox"]
    }
  }
}
```

**Example (Selenium Grid):**
```json
{
  "tool": "start_browser",
  "parameters": {
    "browser": "chrome",
    "options": {
      "gridUrl": "http://selenium-hub:4444/wd/hub",
      "platform": "LINUX",
      "browserVersion": "114.0"
    }
  }
}
```

**Example (LambdaTest):**
```json
{
  "tool": "start_browser",
  "parameters": {
    "browser": "chrome",
    "options": {
      "ltUsername": "your_username",
      "ltAccessKey": "your_access_key",
      "platform": "Windows 10",
      "browserVersion": "latest",
      "ltBuild": "Test Build 1",
      "ltTestName": "Homepage Test",
      "ltVideo": true,
      "ltConsole": true
    }
  }
}
```

### navigate
Navigates to a URL.

**Parameters:**
- `url` (required): URL to navigate to
  - Type: string

**Example:**
```json
{
  "tool": "navigate",
  "parameters": {
    "url": "https://www.example.com"
  }
}
```

### find_element
Finds an element on the page.

**Parameters:**
- `by` (required): Locator strategy
  - Type: string
  - Enum: ["id", "css", "xpath", "name", "tag", "class"]
- `value` (required): Value for the locator strategy
  - Type: string
- `timeout`: Maximum time to wait for element in milliseconds
  - Type: number
  - Default: 10000

**Example:**
```json
{
  "tool": "find_element",
  "parameters": {
    "by": "id",
    "value": "search-input",
    "timeout": 5000
  }
}
```

### click_element
Clicks an element.

**Parameters:**
- `by` (required): Locator strategy
  - Type: string
  - Enum: ["id", "css", "xpath", "name", "tag", "class"]
- `value` (required): Value for the locator strategy
  - Type: string
- `timeout`: Maximum time to wait for element in milliseconds
  - Type: number
  - Default: 10000

**Example:**
```json
{
  "tool": "click_element",
  "parameters": {
    "by": "css",
    "value": ".submit-button"
  }
}
```

### send_keys
Sends keys to an element (typing).

**Parameters:**
- `by` (required): Locator strategy
  - Type: string
  - Enum: ["id", "css", "xpath", "name", "tag", "class"]
- `value` (required): Value for the locator strategy
  - Type: string
- `text` (required): Text to enter into the element
  - Type: string
- `timeout`: Maximum time to wait for element in milliseconds
  - Type: number
  - Default: 10000

**Example:**
```json
{
  "tool": "send_keys",
  "parameters": {
    "by": "name",
    "value": "username",
    "text": "testuser"
  }
}
```

### get_element_text
Gets the text() of an element.

**Parameters:**
- `by` (required): Locator strategy
  - Type: string
  - Enum: ["id", "css", "xpath", "name", "tag", "class"]
- `value` (required): Value for the locator strategy
  - Type: string
- `timeout`: Maximum time to wait for element in milliseconds
  - Type: number
  - Default: 10000

**Example:**
```json
{
  "tool": "get_element_text",
  "parameters": {
    "by": "css",
    "value": ".message"
  }
}
```

### hover
Moves the mouse to hover over an element.

**Parameters:**
- `by` (required): Locator strategy
  - Type: string
  - Enum: ["id", "css", "xpath", "name", "tag", "class"]
- `value` (required): Value for the locator strategy
  - Type: string
- `timeout`: Maximum time to wait for element in milliseconds
  - Type: number
  - Default: 10000

**Example:**
```json
{
  "tool": "hover",
  "parameters": {
    "by": "css",
    "value": ".dropdown-menu"
  }
}
```

### drag_and_drop
Drags an element and drops it onto another element.

**Parameters:**
- `by` (required): Locator strategy for source element
  - Type: string
  - Enum: ["id", "css", "xpath", "name", "tag", "class"]
- `value` (required): Value for the source locator strategy
  - Type: string
- `targetBy` (required): Locator strategy for target element
  - Type: string
  - Enum: ["id", "css", "xpath", "name", "tag", "class"]
- `targetValue` (required): Value for the target locator strategy
  - Type: string
- `timeout`: Maximum time to wait for elements in milliseconds
  - Type: number
  - Default: 10000

**Example:**
```json
{
  "tool": "drag_and_drop",
  "parameters": {
    "by": "id",
    "value": "draggable",
    "targetBy": "id",
    "targetValue": "droppable"
  }
}
```

### double_click
Performs a double click on an element.

**Parameters:**
- `by` (required): Locator strategy
  - Type: string
  - Enum: ["id", "css", "xpath", "name", "tag", "class"]
- `value` (required): Value for the locator strategy
  - Type: string
- `timeout`: Maximum time to wait for element in milliseconds
  - Type: number
  - Default: 10000

**Example:**
```json
{
  "tool": "double_click",
  "parameters": {
    "by": "css",
    "value": ".editable-text"
  }
}
```

### right_click
Performs a right click (context click) on an element.

**Parameters:**
- `by` (required): Locator strategy
  - Type: string
  - Enum: ["id", "css", "xpath", "name", "tag", "class"]
- `value` (required): Value for the locator strategy
  - Type: string
- `timeout`: Maximum time to wait for element in milliseconds
  - Type: number
  - Default: 10000

**Example:**
```json
{
  "tool": "right_click",
  "parameters": {
    "by": "css",
    "value": ".context-menu-trigger"
  }
}
```

### press_key
Simulates pressing a keyboard key.

**Parameters:**
- `key` (required): Key to press (e.g., 'Enter', 'Tab', 'a', etc.)
  - Type: string

**Example:**
```json
{
  "tool": "press_key",
  "parameters": {
    "key": "Enter"
  }
}
```

### upload_file
Uploads a file using a file input element.

**Parameters:**
- `by` (required): Locator strategy
  - Type: string
  - Enum: ["id", "css", "xpath", "name", "tag", "class"]
- `value` (required): Value for the locator strategy
  - Type: string
- `filePath` (required): Absolute path to the file to upload
  - Type: string
- `timeout`: Maximum time to wait for element in milliseconds
  - Type: number
  - Default: 10000

**Example:**
```json
{
  "tool": "upload_file",
  "parameters": {
    "by": "id",
    "value": "file-input",
    "filePath": "/path/to/file.pdf"
  }
}
```

### take_screenshot
Captures a screenshot of the current page.

**Parameters:**
- `outputPath` (optional): Path where to save the screenshot. If not provided, returns base64 data.
  - Type: string

**Example:**
```json
{
  "tool": "take_screenshot",
  "parameters": {
    "outputPath": "/path/to/screenshot.png"
  }
}
```

### close_session
Closes the current browser session and cleans up resources.

**Parameters:**
None required

**Example:**
```json
{
  "tool": "close_session",
  "parameters": {}
}
```


## License

MIT
