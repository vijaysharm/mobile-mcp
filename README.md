## Mobile Next - MCP server for Mobile Automation

This is a [Model Context Protocol (MCP) server](https://github.com/modelcontextprotocol) that enables scalable mobile automation through a platform-agnostic interface, eliminating the need for distinct iOS or Android knowledge.
This server allows Agents and LLMs to interact with native iOS/Android applications and devices through structured accessibility snapshots or coordinate-based taps based on screenshots. 



<p align="center">
    <a href="https://github.com/mobile-next/">
        <img alt="mobile-mcp" src="https://raw.githubusercontent.com/mobile-next/mobile-next-assets/refs/heads/main/mobile-mcp-banner.png" width="600">
    </a>
</p>

### 🚀 Mobile MCP Roadmap: Building the Future of Mobile

Join us on our journey as we continuously enhance Mobile MCP! 
Check out our detailed roadmap to see upcoming features, improvements, and milestones. Your feedback is invaluable in shaping the future of mobile automation.

👉 [Explore the Roadmap](https://github.com/orgs/mobile-next/projects/1)

### Main use cases

How we help to scale mobile automation:

- 📲 Native app automation (iOS and Android) for testing or data-entry scenarios. 
- 📝 Scripted flows and form interactions without manually controlling simulators/emulators or physical devices (iPhone, Samsung, Google Pixel etc)
- 🧭 Automating multi-step user journeys driven by an LLM
- 👆 General-purpose mobile application interaction for agent-based frameworks
- 🤖 Enables agent-to-agent communication for mobile automation usecases, data extraction

## Main Features

- 🚀 **Fast and lightweight**: Uses native accessibility trees for most interactions, or screenshot based coordinates where a11y labels are not available. 
- 🤖 **LLM-friendly**: No computer vision model required in Accessibility (Snapshot).
- 🧿 **Visual Sense**: Evaluates and analyses what’s actually rendered on screen to decide the next action. If accessibility data or view-hierarchy coordinates are unavailable, it falls back to screenshot-based analysis.
- 📊 **Deterministic tool application**: Reduces ambiguity found in purely screenshot-based approaches by relying on structured data whenever possible.
- 📺 **Extract structured data**: Enables you to extract structred data from anything visible on screen. 

## Mobile MCP Architecture

<p align="center">
    <a href="https://raw.githubusercontent.com/mobile-next/mobile-next-assets/refs/heads/main/mobile-mcp-arch.png">
        <img alt="mobile-mcp" src="https://raw.githubusercontent.com/mobile-next/mobile-next-assets/refs/heads/main/mobile-mcp-arch.png" width="600">
    </a>
</p>



## How to install

```js
{
  "mcpServers": {
    "mobile-next": {
      "command": "npx",
      "args": [
        "@mobilenext/mobile-mcp@latest"
      ]
    }
  }
}
```

## Prerequisites

What you will need to connect MCP with your agent and mobile devices:

- [Xcode command line tools](https://developer.apple.com/xcode/resources/)
- [Android Platform Tools](https://developer.android.com/tools/releases/platform-tools)
- [node.js](https://nodejs.org/en/download/)
- [MCP](https://modelcontextprotocol.io/introduction) supported foundational models or agents, like [Claude MCP](https://modelcontextprotocol.io/quickstart/server), [OpenAI Agent SDK](https://openai.github.io/openai-agents-python/mcp/), [Copilot Studio](https://www.microsoft.com/en-us/microsoft-copilot/blog/copilot-studio/introducing-model-context-protocol-mcp-in-copilot-studio-simplified-integration-with-ai-apps-and-agents/)

### Simulators, Emulators, and Physical Devices

When launched, Mobile MCP can connect to:
	•	iOS Simulators on macOS/Linux
	•	Android Emulators on Linux/Windows/macOS
	•	Physical iOS or Android devices (requires proper platform tools and drivers)

Make sure you have your mobile platform SDKs (Xcode, Android SDK) installed and configured properly before running Mobile Next Mobile MCP.


### Running in "headless" mode on Simulators/Emulators

When you do not have an actual phone connected, you can run Mobile Next Mobile MCP with an emulator or simulator in the background.

For example, on Android:
	1.	Start an emulator (avdmanager / emulator command).
	2.	Run Mobile MCP with the desired flags

On iOS, you'll need Xcode and to run the Simulator before using Mobile MCP with that simulator instance.
`xcrun simctl list`
`xcrun simctl boot "iPhone 16"`


# Mobile Commands and interaction tools

These tools use accessibility-based element references on iOS or Android. By relying on the accessibility/automation IDs, you avoid the ambiguity of coordinate-based approaches.

## mobile_install_app
- **Description:** Installs an app onto the device/emulator
- **Parameters:**
  - `appPath` (string): Path or URL to the app file (e.g., .apk for Android, .ipa/.app for iOS)

## mobile_launch_app
- **Description:** Launches the specified app on the device/emulator
- **Parameters:**
  - `bundleId` (string): The application's unique bundle/package identifier like: com.google.android.keep	 or com.apple.mobilenotes )

## mobile_terminate_app
- **Description:** Terminates a running application
- **Parameters:**
  - `bundleId` (string): The application's bundle/package identifier

## mobile_element_tap
- **Description:** Taps on a UI element identified by accessibility locator
- **Parameters:**
  - `element` (string): Human-readable element description (e.g., "Login button")
  - `ref` (string): Accessibility/automation ID or reference from a snapshot

## mobile_tap
- **Description:** Taps on specified screen coordinates
- **Parameters:**
  - `x` (number): X-coordinate
  - `y` (number): Y-coordinate

## mobile_element_send_keys
- **Description:** Types text into a UI element (e.g., TextField)
- **Parameters:**
  - `element` (string): Human-readable element description
  - `ref` (string): Accessibility/automation ID of the element
  - `text` (string): Text to type
  - `submit` (boolean): Whether to press Enter/Return after typing

## mobile_element_swipe
- **Description:** Performs a swipe gesture from one UI element to another
- **Parameters:**
  - `startElement` (string): Human-readable description of the start element
  - `startRef` (string): Accessibility/automation ID of the start element
  - `endElement` (string): Human-readable description of the end element
  - `endRef` (string): Accessibility/automation ID of the end element
 
## mobile_swipe
- **Description:** Performs a swipe gesture between two sets of screen coordinates
- **Parameters:**
  - `startX` (number): Start X-coordinate
  - `startY` (number): Start Y-coordinate
  - `endX` (number): End X-coordinate
  - `endY` (number): End Y-coordinate

## mobile_press_key
- **Description:** Presses hardware keys or triggers special events (e.g., back button on Android)
- **Parameters:**
  - `key` (string): Key identifier (e.g., HOME, BACK, VOLUME_UP, etc.)

## mobile_take_screenshot
- **Description:** Captures a screenshot of the current device screen
- **Parameters:**
  - `raw` (boolean): Return a lossless image if true; otherwise, compressed by default

## mobile_get_source
- **Description:** Fetches the current device UI structure (accessibility snapshot) (xml format)
- **Parameters:** None

## mobile_wait
- **Description:** Waits for a specified time
- **Parameters:**
  - `time` (number): Time to wait in seconds (capped at 10 seconds)

## mobile_close_session
- **Description:** Closes the current device session
- **Parameters:** None


