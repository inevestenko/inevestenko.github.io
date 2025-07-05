# C4D to ComfyUI Plugin User Guide (Version 0.1.11)

The **C4D to ComfyUI** plugin integrates Cinema 4D with ComfyUI, enabling advanced rendering workflows by combining Cinema 4D's 3D capabilities with ComfyUI's AI-driven image generation. This guide provides step-by-step instructions for installing, configuring, and using the plugin effectively.

---

## Table of Contents
1. [Overview](#overview)
2. [System Requirements](#system-requirements)
3. [Installation](#installation)
4. [Initial Setup](#initial-setup)
5. [Plugin Interface Overview](#plugin-interface-overview)
6. [Key Features and Usage](#key-features-and-usage)
   - [Managing the ComfyUI Server](#managing-the-comfyui-server)
   - [Selecting and Managing Workflows](#selecting-and-managing-workflows)
   - [Rendering in Cinema 4D](#rendering-in-cinema-4d)
   - [Image Input and Processing](#image-input-and-processing)
   - [Using Prompts and Settings](#using-prompts-and-settings)
   - [Drawing Masks](#drawing-masks)
   - [Viewing and Managing Outputs](#viewing-and-managing-outputs)
7. [Troubleshooting](#troubleshooting)
8. [Support and Contact](#support-and-contact)

---

## Overview

The **C4D to ComfyUI** plugin allows Cinema 4D users to:
- Connect to a ComfyUI server for AI-based image generation.
- Render scenes in Cinema 4D and use them as inputs for ComfyUI workflows.
- Load and manage ComfyUI workflows directly within Cinema 4D.
- Process images with custom prompts, settings, and masks.
- Preview inputs and outputs in a user-friendly interface.

The plugin supports two modes:
- **Pipeline Mode**: Combines Cinema 4D rendering with ComfyUI processing in a single workflow.
- **Workflow API Mode**: Directly uses ComfyUI workflows for image generation.

---

## System Requirements

- **Cinema 4D**: Version 2024 or newer.
- **Operating System**: Windows, macOS, or Linux.
- **ComfyUI**: Installed locally or accessible via a server (default: `http://127.0.0.1:8000`).
- **Python**: Required for running the ComfyUI server (Python 3.7+ recommended).
- **Internet Connection**: Required for activation and optional ComfyUI downloads.
- **Dependencies**: Libraries like `requests`, `deep_translator`, `Pillow`, and `websocket-client` (automatically handled by the plugin).

---

## Installation

1. **Download the Plugin**:
   - Obtain the plugin files from the official source (e.g., Boosty: [https://boosty.to/inevestenko](https://boosty.to/inevestenko)).
   - Ensure you have the plugin ZIP file or folder containing the Python script and resources.

2. **Install in Cinema 4D**:
   - Copy the plugin folder to the Cinema 4D plugins directory:
     - **Windows**: `C:\Users\[YourUsername]\AppData\Roaming\Maxon\Cinema 4D [Version]\plugins`
     - **macOS**: `~/Library/Preferences/MAXON/Cinema 4D [Version]/plugins`
     - **Linux**: `~/.config/MAXON/Cinema 4D [Version]/plugins`
   - Restart Cinema 4D to load the plugin.

3. **Install ComfyUI (if not already installed)**:
   - From the plugin menu, select **Server > Install ComfyUI > ComfyUI Web** to visit [https://www.comfy.org/download](https://www.comfy.org/download) or **ComfyUI GitHub** for [https://github.com/comfyanonymous/ComfyUI](https://github.com/comfyanonymous/ComfyUI).
   - Follow the instructions to set up ComfyUI locally or on a server.

4. **Activate the Plugin**:
   - Open the plugin in Cinema 4D (see [Initial Setup](#initial-setup)).
   - Sign in with your Boosty email to activate the plugin. A 30-day trial starts upon activation, after which a subscription may be required.

---

## Initial Setup

1. **Open the Plugin**:
   - In Cinema 4D, go to **Plugins > C4D to ComfyUI** to open the plugin window.
   - The plugin interface will appear with the title "C4D to ComfyUI (0.1.11)".

2. **Configure Settings**:
   - Go to **Settings > Open Settings** in the plugin menu.
   - In the **Settings Dialog**, configure:
     - **Boosty Email**: Enter your email for activation (if not activated).
     - **Port**: Set the ComfyUI server port (default: `8000`).
     - **ComfyUI Path**: Specify the path to your ComfyUI installation (e.g., `C:\ComfyUI` on Windows).
     - **Model Base Path**: Set the path to ComfyUI models (e.g., `C:\ComfyUI\models`).
     - **Input/Output Paths**: Define where input and output images are saved (e.g., `C:\ComfyUI\input` and `C:\ComfyUI\output`).
     - **Prefixes and Folders**: Optionally set prefixes (e.g., `C4D` for inputs, `ComfyUI` for outputs) and enable project-specific folders.
   - Click **OK** to save settings.

3. **Activate the Plugin**:
   - If not activated, enter your Boosty email in the **Settings Dialog** and click **Sign in**.
   - The plugin checks activation status via a GitHub Gist and stores it locally at `C:\Users\[YourUsername]\AppData\Local\C4DtoComfyUI\activation.json` (Windows) or equivalent.
   - Check the session status in **Help > About** (valid for 30 days from activation).

4. **Start the ComfyUI Server**:
   - Go to **Server > Start Server** to launch the ComfyUI server.
   - Verify the server status with **Server > Check Server**. A message will confirm if the server is running.

---

## Plugin Interface Overview

The plugin interface is divided into several sections:

- **Menu Bar**:
  - **Server**: Start, stop, check, or fix the ComfyUI server; install ComfyUI.
  - **Workflow**: Open or manage ComfyUI workflows.
  - **Settings**: Access settings or the preferences folder.
  - **Help**: View plugin information and session status.

- **Control Panel**:
  - **Server Controls**: Start/stop the server and select modes (Pipeline or Workflow API).
  - **Workflow Selection**: Choose or open workflows.
  - **Render Options**: Select rendering types (e.g., Alpha, Beauty, Depth).
  - **Run/Cancel**: Start or stop processing.

- **Main Area**:
  - **Input/Output Previews**: Display input renders/images and output results.
  - **View Transform**: Switch between Input-only, Side-by-Side, Stacked, or Output-only views.
  - **Sidebar**: Toggle to show/hide tabs (Info, Input, Output, Prompts, Settings, Tools, Workflow).

- **Tabs**:
  - **Info**: Displays server status, port, and workflow details.
  - **Input**: Configures input options (render, image, or both).
  - **Output**: Sets output types (e.g., image, HDRI, video).
  - **Prompts**: Manages positive/negative prompts with translation support.
  - **Settings**: Adjusts rendering parameters (width, height, seed, etc.).
  - **Tools**: Includes mask drawing tools.
  - **Workflow**: Manages workflow paths and model settings.

---

## Key Features and Usage

### Managing the ComfyUI Server

1. **Start the Server**:
   - Select **Server > Start Server** or click the "Start ComfyUI Server" button.
   - The server runs at the specified port (default: `8000`). The button toggles to "Stop ComfyUI Server" when active.

2. **Check Server Status**:
   - Use **Server > Check Server** to verify if the server is running.
   - A dialog confirms the status (e.g., "ComfyUI server is already running!").

3. **Stop the Server**:
   - Select **Server > Stop Server** or click the "Stop ComfyUI Server" button to halt the server.

4. **Fix Server Issues**:
   - If the server fails to start, use **Server > Fix Server** to update dependencies or resolve issues.

### Selecting and Managing Workflows

1. **Choose a Mode**:
   - In the **Control Panel**, select **Pipeline** or **Workflow API** from the mode dropdown.
     - **Pipeline**: Uses predefined templates for combined rendering and processing.
     - **Workflow API**: Directly uses ComfyUI JSON workflows.

2. **Load a Workflow**:
   - For **Pipeline Mode**:
     - Select a pipeline type, task, and specific pipeline from the dropdowns.
     - The plugin loads workflows from `C:\Users\[YourUsername]\AppData\Local\C4DtoComfyUI\pipeline_templates` (Windows) or equivalent.
   - For **Workflow API Mode**:
     - Click **Workflow > Open Workflow API** or the "Open Workflow API" button.
     - Choose a `.json` workflow file from your ComfyUI installation.
     - The workflow is added to the dropdown and saved in `comfyui_workflows.txt`.

3. **Manage Workflows**:
   - **Update**: Click the "Update Workflow API" button to save GUI changes to the current workflow.
   - **Reload**: Use the "Reload Workflow API" button to revert to the original workflow values.
   - **Clear**: Click the "Clear Workflow API" button to reset fields to defaults.
   - **Remove**: Select the "Remove Workflow API" button to delete the current workflow from the list.

### Rendering in Cinema 4D

1. **Select Render Type**:
   - In the **Control Panel**, choose a render type from the dropdown (e.g., Alpha, Beauty, Depth, Canny, Mask).
   - Each type corresponds to a specific pass (e.g., Beauty for full render, Depth for depth map).

2. **Set Render Parameters**:
   - In the **Settings Tab**, adjust:
     - **Width/Height**: Set resolution (default: 1024x1024, range: 256-1280, step: 16).
     - **Seed**: Use -1 for random or specify a value (0-2147483647).
     - **Steps**: Number of sampling steps (default: 1, range: 1-100).
     - **CFG/Guidance**: Control prompt adherence (default: 1.0/1.0, range: 0-100).
     - **Sampler/Scheduler**: Choose algorithms (e.g., Euler, Normal).
     - **Denoise**: Adjust noise reduction (default: 1.0, range: 0-1).

3. **Start Rendering**:
   - Click the **Render** button in the **Control Panel**.
   - The plugin renders the scene to the input path (e.g., `C:\ComfyUI\input\[Prefix]_[DocumentName]_*.png`).
   - Monitor progress in the **Input Status Area** (yellow during rendering, green when complete).

### Image Input and Processing

1. **Select Input Mode**:
   - In the **Input Tab**, choose an input option:
     - **Pipeline**: Uses predefined pipeline inputs.
     - **Render**: Uses a rendered image from Cinema 4D.
     - **Render+Image**: Combines a render and an external image.
     - **Image**: Uses an external image only.

2. **Load an Image**:
   - For **Render** or **Render+Image**:
     - Select a render from the **Render** dropdown (lists recent renders).
     - The image appears in the **Input Preview Area**.
   - For **Image** or **Render+Image**:
     - Click the "Open Image" button or enter a path in the **Image Path** field.
     - Choose a `.png`, `.jpg`, `.jpeg`, or `.bmp` file.
     - The image loads into the **Input Preview Area**.

3. **Adjust Image Settings**:
   - The plugin automatically updates **Width** and **Height** fields based on the loaded image or render.
   - Use the **Input Preview Area** to zoom, pan, or copy/paste images (right-click for options).

### Drawing Masks

1. **Enable Drawing Mode**:
   - In the **Tools Tab**, click **Draw Mask** to toggle drawing mode (available in **Image** or **Render** input modes).
   - The button text changes to "Stop Drawing" when active.

2. **Draw or Erase**:
   - Adjust the **Brush Size** slider (default: 20 pixels).
   - Click **Eraser** to toggle between drawing and erasing modes.
   - Click and drag in the **Input Preview Area** to draw or erase on the mask.
   - A preview circle shows the brush size during drawing.

3. **Manage Masks**:
   - **Undo/Redo**: Use the **Undo Mask** or **Redo Mask** buttons to revert changes (up to 50 steps).
   - **Clear Mask**: Click **Clear Mask** to reset the mask.
   - **Save Mask**: Use **Save Mask** to export the mask as a `.png` file.

### Viewing and Managing Outputs

1. **Run Generation**:
   - Click the **Run** button in the **Control Panel** to process the workflow.
   - In **Pipeline Mode**, the plugin renders the scene (if required) and sends it to ComfyUI.
   - In **Workflow API Mode**, the workflow is sent directly to ComfyUI.
   - Monitor progress in the **Output Status Area** (yellow during processing, green when complete).

2. **Preview Outputs**:
   - Results appear in the **Output Preview Area**.
   - Use **View Transform** to switch between **Input-only**, **Side-by-Side**, **Stacked**, or **Output-only** views.
   - Zoom, pan, or copy the output image via right-click options.

3. **Save Outputs**:
   - Outputs are saved to the specified output path (e.g., `C:\ComfyUI\output\[Prefix]_[DocumentName]_*.png`).
   - Enable **Save to Output Project Folder** in settings to organize outputs by project.

---

## Troubleshooting

- **Server Not Starting**:
  - Ensure ComfyUI is installed and the path is correct in **Settings**.
  - Use **Server > Fix Server** to update dependencies.
  - Check the port (default: `8000`) is not in use by another application.

- **Plugin Not Activated**:
  - Verify your Boosty email in **Settings > Sign in**.
  - Check session status in **Help > About**. If expired, re-activate via Boosty.

- **Workflow Errors**:
  - Ensure the `.json` workflow file is valid (use a text editor to check syntax).
  - Reload the workflow using **Workflow > Reload Workflow API**.

- **Rendering Issues**:
  - Confirm the active document has valid render settings.
  - Check input/output paths for write permissions.

- **Image Not Loading**:
  - Verify the file format (`.png`, `.jpg`, `.jpeg`, `.bmp`) and path.
  - Ensure the image has valid dimensions (non-zero width/height).

---

## Support and Contact

- **Developer Contact**: [inevestenko@gmail.com](mailto:inevestenko@gmail.com)
- **Boosty Subscription**: [https://boosty.to/inevestenko](https://boosty.to/inevestenko)
- **Session Status**: Check remaining days in **Help > About** (30-day trial from activation).
- **Documentation**: Refer to this guide or visit the Boosty page for updates.

For additional help, include error messages and steps to reproduce the issue when contacting support.

---

This guide covers the core functionality of the **C4D to ComfyUI** plugin. Experiment with different workflows, rendering options, and settings to unlock its full potential for your creative projects!