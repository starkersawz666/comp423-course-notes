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

## Create New Rust Project

After entering the dev container, we can use the following command to create a new binary project:

```bash
cargo new hello-comp423 --vcs none
cd hello-comp423
```

- `Cargo` It is Rust's official package manager and build system. Cargo simplifies tasks like project creation, dependency management, and building. More about Cargo and Rust can be found at [Github](https://github.com/rust-lang/book).

- `Cargo new` This sub - command creates a new Rust project. In our case, we're creating a project named hello - comp423.
- `--vcs` stands for "Version Control System", which is not necessary here because we've already created a Git repository. Therefore, we use `--vcs none` to avoid the automatic initialization of vcs.

- The generated structure of the project contains:

```bash
hello-comp423/
└── src/
    └── main.rs
```

## Write the "Helloworld" Program

Open the `src/main.rs` file in VSCode, and replace its contents with:

```rust
fn main() {
    println!("Hello COMP423");
}
```

- The `fn` keyword is used to define a function, and `fn main()` defines a function `main`, which is the entry point of executable program.

- `println!("Hello COMP423");` print the given text to the standard output.

## Build and Run the Program

To build the program, use the `cargo build` command (which is similar to `gcc` command):

```bash
cargo build
```

The complied binary is in the `target/debug` directory, and it can be run directly:

```bash
./target/debug/hello-comp423
```

Alternatively, `cargo run` can build and immediately run the program in one step:

```bash
cargo run
```

## Result Following the Tutorial

An expected result of the Rust project is given at [Github](https://github.com/starkersawz666/comp423-rust-container).

## Congratulations!

You have successfully run your first Rust program!