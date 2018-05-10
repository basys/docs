### Getting started

There are two ways to start a new Basys project:

#### Basys IDE (Visual Studio Code extension)

This is a recommended way to get started with Basys. The development environment provides a deep integration with Basys toolbox: sidebar panel for running toolbox commands, built-in linting, tests integration.

To get started install [Basys extension for VSCode](https://marketplace.visualstudio.com/items?itemName=basys.vscode-basys), open the Command Palette (`Ctrl+Shift+P` on Windows/Linux or `⇧⌘P` on MacOS) and run `Basys: Create project` command.

#### CLI

If you prefer to use other code editors - no problem! You can start a new project with Basys CLI

```bash
# Install Basys CLI
npm install -g basys-cli
# or
yarn global add basys-cli

# Scaffold a new project from a starter template
basys init
cd <project-dir>

# Launch the development server
basys dev
```
