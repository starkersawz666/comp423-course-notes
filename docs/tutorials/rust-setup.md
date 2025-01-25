# Setting up a dev container for Rust

* Primary author: [Zixin Wei](https://github.com/starkersawz666)
* Reviewer: [tang zoey](https://github.com/tangzoey)

## Prerequisites

Before we start on this tutorial, there are some configurations that should be done:

- **Docker**: Docker is containerization platform. If Docker has not been installed, please go to [Docker Desktop](https://www.docker.com/products/docker-desktop/) to downlaod and install.

- **Visual Studio Code**: [VSCode](https://code.visualstudio.com/) is the Integrated Development Environment (IDE) recommended here. 

- **Dev Containers Extension**: to be installed inside Visual Studio Code.

## Git Initialization

Create and enter a blank directory with the following commands:

```bash
mkdir comp423-rust-container
cd comp423-rust-container
```

Then, initialize a new git repository:

```bash
git init
```

## Dev Container Configuration

To quickly configurate a dev container, we need to create a folder named `.devcontainer` inside the project directory:

```bash
mkdir .devcontainer
```

Inside `.devcontainer`, we need to create a `devcontainer.json` file:

```bash
touch .devcontainer/devcontainer.json
```

and add the following content:

```json
{
    "name": "Rust Dev Container",
    "image": "mcr.microsoft.com/devcontainers/rust:latest",
    "customizations": {
        "vscode": {
            "extensions": [
                "rust-lang.rust-analyzer"
            ]
        }
    },
    "postCreateCommand": "rustc --version"
}
```

In the JSON content above:

- **`image`** specifies the container image we use for the project, which is from Microsoft's Dev Container repository for Rust;

- **`customizations.vscode.extensions`** helps add VSCode extensions of rust automatically in the dev container

- **`postCreateCommand`** is the command run after the container is created. You can fill in other commands if you want to build your own rust environment.

## Build and Open Dev Container

Reopen the project folder, press `Ctrl+Shift+P` on Windows or `Cmd+Shift+P` on Mac, type `Dev Containers: Reopen in Container`, and select the corresponding option. Then, the image will be downloaded (may take a few minutes) and the project will be reopened in dev container. To verify Rust version, run `rustc --version` (1.83.0 on Jan. 26).