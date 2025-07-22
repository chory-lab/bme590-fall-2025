# 🚀 BME 590 - Laboratory Automation Class Repository

Welcome to the official class repository for Fall 2025 BME 590: Laboratory Automation!

**Professor**: Emma Chory, Ph.D.
**Teaching Assistant:** Benjamin Perry

---

This README will provide all the necessary steps to set up your computer for class assignments, tutorials, and projects. We will install all necessary tools, including Python and the `pylabrobot` library. Please follow these steps in order and if you run into any issues, please send an issue to the \#code channel in slack! Additionally, you can contact Ben or Professor Chory or attend office hours.

---

## Step 1: Install Foundational Tools (VS Code & Git)

Before we can work with Python, we need a code editor and a version control system.

1. **Install VS Code**: This is our recommended code editor for this class. Please install the version relevant to your operating system at the following link. After installation, you should be able to open Visual Studio Code on your computer.
    * [**code.visualstudio.com**](https://code.visualstudio.com/)

2. **Install Git**: This tool lets us download and manage the project code.
    * [**git-scm.com/downloads**](https://git-scm.com/downloads)
    * During installation, you can accept all the default settings.

3. **(Windows Users Only) Install WSL**: The Windows Subsystem for Linux (WSL) lets you run a Linux environment directly on Windows. It's highly recommended for a smoother experience.
    * Open **PowerShell as an Administrator** (search for PowerShell, right-click, and select "Run as administrator").
    * Run this single command:

        ```powershell
        wsl --install
        ```

    * After it finishes, **restart your computer**. When it reboots, it will ask you to create a username and password for your new Linux system. Remember these!

---

## Step 2: Install Conda for Python Management

Conda is a package manager that will install Python and all our required libraries in an isolated environment, preventing conflicts.

1. **Download Miniconda**: We'll use Miniconda, a minimal installer for Conda.
    * [**docs.conda.io/en/latest/miniconda.html**](https://docs.conda.io/en/latest/miniconda.html)
    * **Windows**: Download the **Windows installer**.
    * **macOS**: Download the **macOS (pkg)** installer for your chip (M1/M2/M3 is "Apple silicon").
    * **Linux/WSL**: Download the **Linux installer**.

2. **Run the Installer**:
    * **Windows/macOS**: Double-click the downloaded file and follow the on-screen instructions. Accept the default settings.
    * **Linux/WSL**: Open your Linux terminal and run the following command, replacing `<installer_name.sh>` with the name of the file you downloaded.

        ```bash
        bash <installer_name.sh>
        ```

        Press `Enter` and type `yes` to agree to the terms.

3. **Restart Your Terminal**: Close and reopen your terminal (or VS Code) for the changes to take effect.

---

## Step 3: Set Up the Project Environment

Now we will download the project code and create a dedicated Conda environment for it.

1. **Open Your Terminal**:
    * **Windows**: Open the **WSL terminal**. You can find it in your Start Menu (it will be named "Ubuntu" or similar).
    * **macOS/Linux**: Open the standard **Terminal** app.

2. **Clone the Project Repository**: Run the following command to download the project code. Replace `<your-class-repo-url>` with the actual URL for this repository.

    ```bash
    git clone <your-class-repo-url>
    ```

3. **Navigate into the Project Folder**:

    ```bash
    cd <name-of-the-cloned-folder>
    ```

4. **Create and Activate the Conda Environment**: This command creates a new, clean environment named `robotics-env` with Python 3.10.

    ```bash
    conda create --name robotics-env python=3.10 -y
    conda activate robotics-env
    ```

    ✅ Your terminal prompt should now start with `(robotics-env)`. You must do this every time you work on the project!

---

## Step 4: Install Project Libraries

With our environment active, we can now install the specific Python libraries we need.

1. **Install Jupyter and Core Libraries**: We'll install Jupyter Notebook from the trusted `conda-forge` channel.

    ```bash
    conda install jupyter notebook -c conda-forge -y
    ```

2. **Install `pylabrobot` with Extras**: This command installs the `pylabrobot` library located in this repository, along with the `visualizer` and `opentrons` modules.

    ```bash
    pip install -e "./pylabrobot[visualizer,opentrons]"
    ```

    * **-e** means "editable," so changes you make to the code are reflected immediately.
    * The `[...]` part installs the extra features we need.

🎉 **Setup complete!** Your environment is ready.

---

## How to Start Working (Daily Workflow)

Each time you want to work on the project, follow these simple steps:

1. Open your terminal (WSL for Windows).
2. Navigate to the project directory: `cd path/to/your/project/folder`
3. Activate the Conda environment: `conda activate robotics-env`
4. Launch Jupyter Notebook to start coding:

    ```bash
    jupyter notebook
    ```

This will open a new tab in your web browser where you can open and run your `.ipynb` notebooks.

To stop the server, go back to your terminal and press `Ctrl+C`. To exit the environment, just type `conda deactivate`.
