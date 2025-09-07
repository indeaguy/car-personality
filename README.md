# Car Personality - GM SDK App

A custom AI assistant app for GM's in-vehicle infotainment system built with the NGI SDK and React.

## Quick Start

This guide will help you set up the GM NGI SDK and emulator for development.

**Reference Documentation:**
https://developer.gm.com/docs/js-documentation/js_docs/js_platform%2Fsdk_guides%2Findex/sdk-quickstart

## Prerequisites

- macOS (for the NGI Emulator)
- Homebrew package manager
- Node.js version 8 (required for GM NGI SDK compatibility)
- Package manager: npm or yarn

> **Important**: The GM NGI SDK requires Node.js version 8. We'll use Homebrew to install nvm, then use nvm to manage Node versions.

## Setup Instructions

### 1. Setup Node.js Version 8

If you don't have Node.js version 8 installed:

1. **Install Homebrew** (if not already installed):
   ```bash
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
   ```

2. **Install nvm via Homebrew**:
   ```bash
   brew install nvm
   ```

3. **Setup nvm in your shell**:
   ```bash
   # Add nvm to your shell profile
   echo 'export NVM_DIR="$HOME/.nvm"' >> ~/.zshrc
   echo '[ -s "/opt/homebrew/share/nvm/nvm.sh" ] && \. "/opt/homebrew/share/nvm/nvm.sh"' >> ~/.zshrc
   echo '[ -s "/opt/homebrew/share/nvm/bash_completion" ] && \. "/opt/homebrew/share/nvm/bash_completion"' >> ~/.zshrc
   
   # Reload your shell configuration
   source ~/.zshrc
   ```

4. **Install and use Node.js version 8**:
   ```bash
   nvm install 8
   nvm use 8
   
   # Optional: Set Node 8 as default for this project
   echo "8" > .nvmrc
   ```

5. **Verify the version**:
   ```bash
   node --version  # Should output v8.x.x
   ```
   
   > **Tip**: With the `.nvmrc` file in place, you can run `nvm use` in the project directory to automatically switch to Node 8.

### 2. Download GM SDK Assets

The GM SDK and emulator files are too large for GitHub. Download them separately:

1. **NGI Emulator**: Download `js-emu_NGI-Emulator-1.10.0.dmg` from [GM Developer Downloads](https://developer.gm.com/docs/emu-downloads)
2. **NGI SDK**: Download `js-emu_ngi-sdk-1.10.0.tgz` from [GM Developer Downloads](https://developer.gm.com/docs/emu-downloads)
3. Place both files in a `gm_assets/` directory in your project root

> **Note**: These files are excluded from version control due to their large size (139MB + 61MB). If you need to include them in your repository, consider using [Git LFS](https://git-lfs.github.io/).

### 3. Install the NGI Emulator

The NGI Emulator allows you to test your GM apps without needing actual vehicle hardware.

1. Navigate to the `gm_assets` directory:
   ```bash
   cd gm_assets
   ```

2. Install the NGI Emulator:
   ```bash
   # Mount and install the emulator DMG
   open js-emu_NGI-Emulator-1.10.0.dmg
   ```
   
3. Follow the installer prompts to complete the emulator installation

### 4. Install the NGI SDK

The SDK provides the necessary tools and libraries for GM app development.

1. Install the NGI SDK locally in your project:
   ```bash
   # Using npm (recommended for GM SDK)
   npm install ./gm_assets/js-emu_ngi-sdk-1.10.0.tgz --verbose
   ```
   
   > **Note**: The GM SDK has dependencies on private GM repositories. If you encounter git clone errors, ensure you have SSH access to GM's Bitbucket repositories.
   
   *Make sure you've downloaded the SDK file to the `gm_assets/` directory first (see step 2)*

2. Initialize your project with the NGI SDK:
   ```bash
   # Use npx to run the locally installed ngi command
   npx ngi init
   ```

### 5. Project Setup

1. Install any additional project dependencies:
   ```bash
   # Using npm
   npm install
   ```

2. Your app configuration is defined in `gmapp.json`:
   - **Name:** Custom AI Assistant
   - **Template:** React
   - **Type:** RemoteHigh
   - **Category:** General

3. **Using GM SDK commands**: Since the SDK is installed locally, use `npx` to run GM commands:
   ```bash
   # Instead of: ngi command
   # Use: npx ngi command
   npx ngi --help  # View available commands
   ```

### 6. Development Workflow

1. **Start Development:**
   ```bash
   # Using npm
   npm start
   ```

2. **Launch NGI Emulator:**
   - Open the NGI Emulator application
   - Load your app for testing in the simulated vehicle environment

3. **Build for Production:**
   ```bash
   # Using npm
   npm run build
   ```

### 7. Testing

- Use the NGI Emulator to test your app in a simulated GM vehicle environment
- Test different screen sizes and orientations
- Verify functionality across different vehicle states

## Project Structure

```
car-personality/
├── src/                    # Source code
│   └── index.html         # Main app entry point
├── gm_assets/             # GM SDK and emulator files (not in git)
│   ├── js-emu_NGI-Emulator-1.10.0.dmg
│   └── js-emu_ngi-sdk-1.10.0.tgz
├── node_modules/          # Local dependencies (not in git)
├── .gitignore             # Git ignore file
├── .nvmrc                 # Node version specification (v8)
├── gmapp.json             # GM app configuration
├── package.json           # Project dependencies (generated after ngi init)
└── README.md              # This file
```

## Next Steps

1. Customize the app configuration in `gmapp.json`
2. Develop your React components in the `src` directory
3. Test regularly using the NGI Emulator
4. Follow GM's development guidelines for in-vehicle apps

For detailed API documentation and advanced features, refer to the GM Developer Portal.

## Troubleshooting

### Removing Global GM SDK Installation

If you previously installed the GM SDK globally and want to use local installation instead:

1. **Check for globally installed packages**:
   ```bash
   npm list -g --depth=0 | grep -i gm
   ```

2. **Remove global GM SDK packages** (if found):
   ```bash
   # Replace 'package-name' with the actual GM SDK package name
   npm uninstall -g package-name
   ```

3. **Follow the local installation steps** in section 4 above

### Node.js Version Issues

If you encounter errors with the GM SDK:

1. **Check your Node version**: `node --version` should show v8.x.x
2. **Switch to Node 8**: Use `nvm use 8` to switch to the correct version
3. **SDK installation fails**: Ensure you're using Node 8 before running the npm install command
4. **nvm not found**: Make sure you've sourced your shell configuration or restart your terminal
5. **Reinstall Node 8**: Use `nvm uninstall 8` then `nvm install 8` if needed

### General Setup Issues

- Ensure you've downloaded the correct version files from [GM Developer Downloads](https://developer.gm.com/docs/emu-downloads)
- Verify file permissions on the downloaded assets
- Make sure the NGI Emulator is properly installed before running `npx ngi init`
- Always use Node.js version 8 when working with the GM NGI SDK

