# **Setting Up a Dev Container for Rust** 

* **Primary author:** [Dennis Wang](https://github.com/DennisComp210)
* **Reviewer:** [Juktong](https://github.com/Juktong)

* **Contributions From/Reference:** [Starting a Static Website Project with MkDocs - Kris Jordan](https://comp423-25s.github.io/resources/MkDocs/tutorial/)

## **Introduction**
Welcome to this tutorial! In this guide, you will learn how to set up a basic Rust development container and write a simple Rust program that outputs "Hello COMP423!". 
Be sure to follow all instructions carefully from top to bottom to ensure that everything is set up correctly. By the end of this tutorial, you will have acquired the skills to:

* Create a new directory and initialize a Git repository.
* Create and connect a local repository to a remote repository on GitHub.
* Set up a basic Rust development container in Visual Studio Code.
* Write, compile, and run a Rust program.





## **Prerequisites**
Before diving into this tutorial, ensure you have the following tools installed and set up:

1. **GitHub Account** 
    * If you don't already have an account yet, create a free account on [GitHub](https://github.com/).
    * A GitHub account is essential for version control and hosting your remote project repository.

2. **Git** 
    * Ensure Git is accessible. Check if Git is installed by running the following command in your terminal:

        ```
        git --version
        ``` 

    * Download and install [Git](https://git-scm.com/) if it's not on your device. 

3. **Visual Studio Code (VS Code)**  
    * VS Code is the recommanded code editor for this tutorial.
    * Install the latest version of VS Code [here](https://code.visualstudio.com/).

4. **Docker** 
    * Docker is required to run dev containers. 
    * Download Docker [here](https://www.docker.com/). 
    * Verify Docker is correctly installed and working by running the following command in your terminal:

        ```
        docker --version
        ```

!!! Notes "Why Prerequisites Matter"
    
    These tools will enable a smooth experience for you to set up the Rust dev container and follow the steps in this guide.



## **Setting Up the Git Repository**

Follow the steps below to setup a Git Repository for the Rust dev container project

### **Step 1: Create a Local Directory and Initialize Git**

Create a new empty directory for this tutorial. 

**(A) Open** the terminal or command prompt on your device. 

**(B) Navigate** to a desired location/directory on your machine and create a new directory for this project using the following commands:

``` 
mkdir rust-dev-tutorial
cd rust-dev-tutorial
```

**(C) Initialize** the directory as a new Git repository using the following command:

```
git init
```

**(D) Create** a ```README.md``` file in the directory and commit it to the history of the repository using the following commands:

```
echo "# Rust Tutorial" > README.md
git add README.md
git commit -m "Initial commit with README"
```

!!! Notes "Why Add a README file?" 

    The README.md file provides an overview of your project and is displayed prominently on your remote GitHub repository. It’s a great place for explaining the purpose of this repository.



### **Step 2: Create a Remote Repository on Github**

**(A) Log** in to your GitHub account and click on the "**New**" button to create a new repository. 

**(B) Fill** out the details on the "Create a new repository" page as follows:

* **Repository Name**: rust-dev-tutorial
* **Description**: "Setting up a basic Rust dev container in VS Code"
* **Visibility**: Public

**(C) Do not** initialize the repository with a README, .gitignore, or license.

**(D) Click** **"Create Repository"** at the bottom.

!!! warning  "Avoid Duplicate Files" 
    
    Do not initialize a README file on GitHub since you have already created and committed one locally.



### **Step 3: Link your Local Repository to GitHub**

**(A) In** your terminal, add the GitHub Repository as a remote repository using the following command:

```
git remote add origin https://github.com/<your-username>/rust-dev-tutorial.git
```

Replace ```<your-username>``` with your GitHub username. 


**(B) Verify** that your default branch name is main with the subcommand: **git branch**. If it's not main (Old version of Git choose the name ```master``` for the primary branch), rename it to main with the following command: 

```
git branch -M main. 
```

**(C) Push** your local commits to the GitHub repository using the following command:

```
git push --set-upstream origin main
```

**(D) Return** back to your GitHub on your web browser and refresh the page, you should see that the same commit you made locally earlier has now been pushed and is visible in your remote repository on GitHub. Verify this is the case before proceeding. 

!!! success "All Set!"

    It you see your commit on GitHub, you have successfully linked your local and remote repository.





## **Setting Up the Rust Dev Container**

### **Step 1: Add Development Container Configuration**

Before preceeding, ensure that **Docker** is installed, running, and accessible in the background. 

**(A) Lauch** Visual Studio Code and open the rust-dev-tutorial directory you created earlier. You can do this using the menu: File > Open Folder, and select the directory. 

**(B) Go** to the extension tab in VS Code (click the square icon on the sidebar or press Ctrl+Shift+X) and search for and install the **Dev Containers** extension. 

**(C) At** the root of your rust-dev-tutorial directory, add a ```.devcontainer``` folder (This is a "hidden" configuration directory). 

**(D) Inside** the ```.devcontainer``` directory, create a file named ```devcontainer.json```. 

**(E) The** ```devcontainer.json``` files defines the configuration for your development environment. Open this file and add the following configurations to it: 

```
{
  "name": "Rust DevContainer Tutorial",
  "image": "mcr.microsoft.com/devcontainers/rust:latest",
  "customizations": {
    "vscode": {
      "extensions": [
        "rust-lang.rust-analyzer"
      ]
    }
  }
}
```

Configurations Explained:

!!! Notes "What are each of these configurations specifying:"

    **name**: A descriptive name for the dev container. Here we are naming it: *Rust DevContainer Tutorial*

    **image**: The Docker image to use. For our purpose, we are using the latest official version of a Rust environment.

    **customizations**: Adds useful configurations to VS Code, like installing the Rust extension. Adding extensions here ensures other developers on your project have them installed in their dev containers automatically. For this tutorial, the dev container will automatically installs the official rust-analyzer VSCode plugin by the Rust Programming Language Group through the configuration: "extensions": ["rust-lang.rust-analyzer"].



### **Step 2: Reopen the Project in a Dev Container**

**(A) Once** the .devcontainer/devcontainer.json file is set up. You will see a pop-up in the bottom right corner of your screen in VS Code that says "Folder contains a Dev Container configuration file. Reopen folder to develop in a container". Click on **"Reopen in Container"**. This will boot up a Docker container, a virtual environment that will have the correct version of Rust installed for you automatically. This may take a few minutes for the image to be downloaded and all the requirements to be installed. 

* If you do not see this pop-up, you can also open the VS Code Command Palette (Ctrl+Shift+P on Window or Cmd+Shift+P on Mac) and search for and select the **"Dev Containers: Reopen in Container"** option.


**(B) The** Docker container will be open once you see the blue "Dev Container" icon appear in the bottom left corner of your VS Code window! 

**(C) Once** you had the dev container open, open a new terminal in VS Code, and run to following command to ensure that rust is installed through the dev container: 

```
rustc --version
```
   
* This will output the installed version of Rust, confirming that the container and environment is set up correctly. Your output should be somthing similar to the following:

    ```
    rustc 1.83.0 (90b35a623 2024-11-26)
    ```
!!! success "Congratulations!"

    You’ve successfully set up a Rust Dev Container. You’re now ready to create, compile, and run Rust programs!





## **Create a Rust Project - Hello Comp 423!**

### **Helpful Commands** 

* ```cargo new```: Creates a new Rust project. The --vcs none flag prevents Cargo from initializing a Git repository.

* ```cargo build```: Compiles the program but does not run it. Similar to using gcc in COMP211 to compile a C program.

    * This command is similar to the gcc commands we learned in COMP211 to compile a C program to generate an executable file.
        * example in C:
            ```
            gcc -o output_name source_file.c
            ```
    * cargo build automates more of the process, including dependency management, and produces an executable.
    * Similar to what we learned in Comp 211 for C, we can run the compiled file for Rust using ```./```

* ```cargo run```: Combines both the build (compile) and run steps for convenience. Think of it as a single command to compile and execute a program.



### **Step 1: Use Cargo new**

**(A) Open** a new terminal in VS Code and navigate to the root of the ```rust-dev-tutorial``` directory. Run the following command to create a new Rust binary project without initializing a Git repository:

```
cargo new hello_comp423 --vcs none
cd hello_comp423
```

This should create the following structure:

```
hello_comp423
├── Cargo.toml
└── src
    └── main.rs
```

* ```Cargo.toml```: Contains metadata and dependencies for your Rust project.

* ```src/main.rs```: This is the main Rust file where your program logic/source code resides.



### **Step 2: Modify main.rs** 

**(A) Edit** and save the src/main.rs file to look like the following:

```
fn main() {
    println!("Hello COMP423!");
}
```



### **Step 3: Compile and Run the Project**

**(A) Rust** uses the **cargo build** command to compile your project. This command reads the ```Cargo.toml``` file for metadata and dependencies, then compiles the code into an executable file.

**(B) Make** sure you are in the or navigate to the root of the binary project directory (```hello_comp423```)  

**(C) Run** the ```cargo build``` command:

```
cargo build
```

This will:

* Compile the Rust source code located in src/main.rs.
* Create an executable file in the target/debug directory

**(D) Run the Compiled file:** Similar to running a C program compiled with gcc in COMP211 by using ```./```, type the following command into your terminal to run the Rust program you just compiled:

 ```
./target/debug/hello_comp423
 ```

This should output:

```
Hello, COMP423!
```

**(E) Alternative Method (Shortcut)**

Instead of building (compiling) and then running the file separately, you can use the ```cargo run``` command to do both in one step:

```
cargo run
```

This command:

* Compiles the project (if needed).
* Runs the executable immediately.

The output should be the same as above:

```
Hello, COMP423!
```

### **Final Step: Update, Commit and Push to Remote Repository**

After verifying your program works, do the following:

**Update**: Update the REAMDE.md in the root directory (```rust-dev-tutorial```) to include a link to this tutorial.

**Commit**: Add and commit all changes made to your local repository using the following commands: 
```
git add .
git commit -m "Rust Dev Container Tutorial Completed"
```

**Push**: Push your commits to your remote repository on GitHub using: 

```
git push 
```

!!! success "Congratulations!!!"

    **You’ve successfully completed this tutorial! You've learned how to setup a basic Rust Dev Container, create a new Rust project, and compile and run your first Rust program. You’re now ready to explore more about Rust development!**