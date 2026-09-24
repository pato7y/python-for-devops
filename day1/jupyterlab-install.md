

# Documentation: Setting Up a Python Virtual Environment & Jupyter Lab



### Step 1: Creating a Virtual Environment

To isolate project dependencies from the global system Python, a virtual environment named `my-project` is created inside the working directory:

```bash
python -m venv my-project

```

### Step 2: Activating the Virtual Environment

Activate the environment to ensure that any installed packages reside locally within the project folder:

```bash
source my-project/bin/activate

```

*(Prompt indicator changes to `(my-project)` upon successful activation).*

### Step 3: Upgrading `pip`

Before installing heavy data science tools, `pip` is upgraded to its latest version to ensure compatibility and smooth dependency resolution:

```bash
pip install --upgrade pip

```

**Execution Log / Output:**

```text
Requirement already satisfied: pip in ./my-project/lib/python3.10/site-packages (22.0.2)
Collecting pip
  Using cached pip-26.2.1-py3-none-any.whl (1.8 MB)
Installing collected packages: pip
  Attempting uninstall: pip
    Found existing installation: pip 22.0.2
    Uninstalling pip-22.0.2:
      Successfully uninstalled pip-22.0.2
Successfully installed pip-26.2.1

```

### Step 4: Installing Jupyter Lab

With an updated package manager, `jupyterlab` and its extensive ecosystem (including `ipykernel`, `tornado`, `Jinja2`, and `jupyter-server`) are installed:

```bash
pip install jupyterlab

```

*Note: The package manager automatically resolves dependencies, downloads the required wheel files, and registers all components successfully into the virtual environment.*

### Step 5: Launching Jupyter Lab

Start the Jupyter Lab server from the working directory:

```bash
jupyter lab

```

**Server Startup Details:**

* **Local URL:** `http://localhost:8888/lab?token=sss`
* **Root Directory:** `/home/sero/python-for-devops/python-for-devops/day1`

If a system web browser is not detected (`No web browser found`), the server provides a secure token URL that can be copied and pasted directly into any external browser to access the development workspace.