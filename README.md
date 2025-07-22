# 🚀 BME 590 - Laboratory Automation Class Repository

Welcome to the official class repository for Fall 2025 BME 590: Laboratory Automation!

**Professor**: Emma Chory, Ph.D.

**Teaching Assistant:** Benjamin Perry

---

This README will provide all the necessary steps to set up your computer for class assignments, tutorials, and projects. We will install all necessary tools, including Python and the `pylabrobot` library, which is the core Python library we will use to control laboratory equipment. Please follow these steps in order and if you run into any issues, please send an issue to the \#code channel in slack! Additionally, you can contact Ben or Professor Chory or attend office hours.

---

## Step 1: Install Foundational Tools (VS Code & Git)

Before we can work with Python, we need a code editor and a version control system. [**If you already have these installed, you may skip to Step 2.**]

1. **Install VS Code**: This is our recommended code editor for this class. Please install the version relevant to your operating system at the following link. After installation, you should be able to open Visual Studio Code on your computer. We ask, unless you certainly know what you are doing, to stick with VS code for this class as it will make debugging IDE issues consistent.

    - [**code.visualstudio.com**](https://code.visualstudio.com/)

If you have installed it properly, you should see a setup screen similar to the screenshot below:

![Screenshot of VS Code Setup Screen on Mac](/figs/vscode_ss.png)

From here, we recommend **creating a folder** somewhere on your computer (e.g. docs/classes/bme-590-fall/) to store your code and project. You can open that folder in VS Code by simply **Open Folder -> \<path_to_folder_you_created\>**

2. **Install Git**: This tool lets us download and manage the project code from GitHub. Additionally, although we will not make heavy use of version control in this class, managing versions of software as they involve is critical in software engineering, especially when working on a team on a project that needs to be collaborative and reproducible (as science often is). If you are interested in reading more about Git, see [here](https://git-scm.com/book/en/v2/Getting-Started-What-is-Git%3F).
    - [**git-scm.com/downloads**](https://git-scm.com/downloads)
        - For Mac, open the **terminal** then install [brew](https://brew.sh/) if not installed, then follow the **Homebrew Git Install Instructions** on the link above.
        - For Windows users, it is **highly recommended** to install Windows Subsystem for Linux (WSL) first (see below) then follow the **Debian/Ubuntu Git Install Instructions**. To do this, first follow **Step 1.3** below, then return to install Git. But, if you wish to use Windows, utilize the **Click here to download** button on the Windows install page.
        - To confirm you have installed Git successfully, run the following in either **PowerShell, WSL, or the Mac Terminal**. You should see something similar to `git version 2.XX.X`

            ```bash
            git --version
            ```

3. **(Windows Users Only) Install WSL**: The Windows Subsystem for Linux (WSL) lets you run a Linux environment directly on Windows. It's highly recommended for a smoother experience overall. Most coding packages may work on Windows, but all coding packages (with extremely few exceptions) work on Linux. If you'd like to read more on WSL, see [here](https://learn.microsoft.com/en-us/windows/wsl/about). For more information on how to use WSL with VS Code (**recommended reading!**), see [here](https://code.visualstudio.com/docs/remote/wsl)
    - Open **PowerShell as an Administrator** (search for PowerShell, right-click, and select "Run as administrator").
    - Run this single command:

        ```powershell
        wsl --install
        ```

    - After it finishes, **restart your computer**. When it reboots, it will ask you to create a username and password for your new Linux system. Remember these! Optionally, do not set a password so you don't have to deal with downstream issues to forgetting your Linux password.
    - Finally, to use with VS Code, navigate within VS Code to **Extensions -> Search -> WSL -> Install** (it is the one authored by Microsoft). You can then use VS Code with the following pattern:

        1. Open WSL from Windows Explorer (this should open a terminal window)
        2. Using the change directory (`cd`) command, navigate to your projects folder [you may have to make this with the make directory command (`mkdir`)].
        3. Once in your target folder, simply run `code .` and VS Code will open.
        4. Optionally, you can open WSL from VS Code (i.e. the converse to this process just described)

---

## Step 2: Install Conda for Python Management

Conda is a package manager that will install Python and all our required libraries in an isolated environment. Because different projects require different **versions** of different packages and Python, using the same set of software for all your projects will likely lead to **conflicts**. Conda allows us to create an individualized environemtn **specific to this class**, with its own version of Python, NumPy, PyLabRobot, and other packages that are independent from the other packages you may have installed on your system. **Again, if you already have conda installed, you may skip this step.**

1. **Download Miniconda**: We'll use Miniconda, a minimal installer for Conda.
    - [**Install Link**](https://docs.conda.io/en/latest/miniconda.html)
    - **Windows**: Again, it is **highly recommended** to use **WSL**, in which case you can follow the Linux/WSL instructions two bullets down. However, if using Windows, navigate to the **Windows PowerShell** install option. Open **Windows PowerShell** and copy/paste the commands listed.
    - **macOS**: Navigate to the code block for your chip (M1/M2/M3/M4 is "Apple silicon") and copy/paste the commands listed.
    - **Linux/WSL**: Navigate to the **Linux** tab and copy-paste the commands listed.
    - Make sure to enter `yes` when agreeing to the terms of service.

2. **Restart Your Terminal**: Close and reopen your terminal (or VS Code) for the changes to take effect.

3. Test your install by running `conda --version`. At this point if you get an error along the lines of `conda command not found` then please raise an issue in slack or contact Ben.

---

## Step 3: Set Up the Project Environment

Now we will download the project code and create a dedicated Conda environment for it.

1. **Open Your Terminal**:
    - **Windows**: Open the **WSL terminal**. You can find it in your Start Menu (it will be named "Ubuntu" or similar).
    - **macOS/Linux**: Open the standard **Terminal** app.

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

    - **-e** means "editable," so changes you make to the code are reflected immediately.
    - The `[...]` part installs the extra features we need.

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
