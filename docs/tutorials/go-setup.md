# Setting up a dev container for Go

* Primary author: [Max Yu](https://github.com/myu123)
* Reviewer: [Ayush Pai](https://github.com/ayushTheunc)

## Prerequisites

Before starting, ensure you have the following installed on your system:

- [Git](https://git-scm.com/)
- [Docker](https://www.docker.com/)
- [Visual Studio Code (VS Code)](https://code.visualstudio.com/)
- [Dev Containers extension for VS Code](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)

## Step-by-Step Instructions

### Step 1: Create a New Project Directory

1. Open your terminal and create a new directory for your Go project:
   ```bash
   mkdir go-project
   cd go-project
   ```
2. Initialize a new Git repository locally:
   ```bash
   git init
   echo "# Go Project" > README.md
   git add README.md
   git commit -m "Initial commit with README"
   ```

### Step 2: Create a Remote Repository and Link It

1. Go to [GitHub](https://github.com/) and create a new repository named `go-project`.
2. Do not initialize the repository with a README, .gitignore, or license.
3. Back in your terminal, add the remote repository to your local Git repository:
   ```bash
   git remote add origin https://github.com/YourGitHubUsername/go-project.git
   ```
4. Push your initial commit to GitHub:
   ```bash
   git branch -M main
   git push -u origin main
   ```

### Step 3: Configure the Development Container in VS Code

1. Open the project in VS Code by selecting **File > Open Folder** and navigating to your `go-project` directory.
2. In the Explorer pane, right-click and select **New Folder**, then name it `.devcontainer`.
3. Inside the `.devcontainer` folder, create a new file named `devcontainer.json` and add the following content:
   ```json
   {
     "name": "Go Dev Container",
     "image": "mcr.microsoft.com/vscode/devcontainers/go:1",
     "customizations": {
       "vscode": {
         "extensions": ["golang.go"]
       }
     }
   }
   ```
4. Use the integrated terminal (Ctrl+` or View > Terminal) to add and commit the new files:
   ```bash
   git add .devcontainer
   git commit -m "Add dev container configuration"
   ```

#### Explanation of the `devcontainer.json` file

- **`name`**: Specifies the name of the dev container, making it easy to identify in VS Code.
- **`image`**: Defines the base Docker image used for the development environment. Here, it specifies a Go development image provided by Microsoft.
- **`customizations`**: Customizes VS Code settings for the container. The example enables the Go extension for better Go language support.

### Step 4: Open the Dev Container in VS Code

1. From the Command Palette:
   - **Windows/Linux**: Press `Ctrl+Shift+P`.
   - **Mac**: Press `Cmd+Shift+P`.
2. Select **Reopen in Container**.
3. Wait for the container to build and initialize.

### Step 5: Initialize a Go Project in the Dev Container

1. Inside the integrated terminal in VS Code, verify your Go installation by checking the version:
   ```bash
   go version
   ```
   Ensure the displayed version is recent and supported.

2. Initialize a new Go module:
   ```bash
   go mod init github.com/YourGitHubUsername/go-project
   ```
   Replace `github.com/YourGitHubUsername/go-project` with the actual URL of your GitHub repository. This ensures your module path matches its hosting location and avoids potential conflicts when sharing or publishing your code.

3. Create a new file named `main.go` with the following content:
   ```go
   package main

   import "fmt"

   func main() {
       fmt.Println("Hello COMP423")
   }
   ```
4. Add and commit the Go project files:
   ```bash
   git add main.go go.mod
   git commit -m "Add basic Go project with Hello COMP423"
   ```

### Step 6: Compile and Run the Project in the Dev Container

1. Compile the project:
   ```bash
   go build -o hello-comp423
   ```
   This generates a binary file named `hello-comp423`. The `go build` command is similar to the `gcc` command in C programming (as used in COMP211). Like `gcc`, `go build` compiles your source code into a machine-readable binary file that can be executed without needing the Go runtime environment to interpret the code.

2. Run the compiled binary directly:
   ```bash
   ./hello-comp423
   ```
   You should see:
   ```
   Hello COMP423
   ```

3. Alternatively, run the project without building:
   ```bash
   go run main.go
   ```
   The `go run` command compiles and executes the code in a single step, but it does not produce a binary file. This is useful for quick testing but is less efficient if you plan to run the program multiple times.

   **Key Difference**: `go build` creates a reusable binary file, whereas `go run` executes the program directly without saving a binary.

### Step 7: Push Updates to GitHub from VS Code

1. Push the latest changes to GitHub using the integrated terminal:
   ```bash
   git push
   ```

## Final Steps

Congratulations! Your Go project is now set up with a dev container and linked to a GitHub repository.

For additional help, consult the [official Go documentation](https://golang.org/doc/).

