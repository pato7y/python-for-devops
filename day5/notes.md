## 1. Maintainability and Test Automation

* **The Need for Maintainability:** As software scales, manual testing, building, and deployment become time-consuming, repetitive, and prone to human error.
* **Continuous Delivery (CD):** Automatically ensures software can be released into production at any time by using a build pipeline for automated testing and deployment.
* **Automation Benefits:**
* Eliminates tedious manual click protocols.
* Allows confident, large-scale refactoring within seconds.
* Ensures high software quality through automated **Quality Gates** and the **Test Pyramid**.



---

## 2. Testing and Coverage with Nose & Coverage

* **Nose & Coverage Installation:**
```bash
$ pip install nose
$ pip install coverage

```



### Common Nose and Coverage Commands

* **Run tests:**
```bash
$ nosetests

```


* **Run tests and calculate coverage:**
```bash
$ nosetests --with-coverage --cover-package=handlers/ --cover-erase

```


* **Enforce minimum coverage percentage (e.g., 90%):**
```bash
$ nosetests --with-coverage --cover-package=handlers/ --cover-erase --cover-min-percentage=90

```


* **Generate an HTML coverage report (`cover/index.html`):**
```bash
$ nosetests --with-coverage --cover-package=handlers/ --cover-erase --cover-html

```



---

## 3. Standardizing Testing with Tox

* **What is Tox?** Tox is a generic virtual environment management and test command-line tool.
* **Key Features:**
* Checks that packages install correctly across different Python versions and interpreters.
* Runs tests in isolated environments, configuring testing tools of choice.
* Acts as a frontend to Continuous Integration (CI) servers, reducing boilerplate and merging local/CI testing.



---

## 4. Python Application Packaging Options

Python applications can be packaged and distributed in several formats depending on the target environment:

* **Python’s Native Packaging:** Wheel (`.whl`), source archives (`sdist`).
* **System Packages:** RPM or DEB packages.
* **Conda Packages.**
* **Freezers:** PyInstaller, PyOxidize (bundles Python interpreter and code into standalone binaries).
* **Container Images:** Docker.
* **Virtual Machines & Bare-Metal Hardware.**

---

## 5. Containerizing Python Applications with Docker

### Example `Dockerfile`

```dockerfile
# Set base image (host OS)
FROM python:3.8

# Set the working directory in the container
WORKDIR /code

# Copy the dependencies file to the working directory
COPY requirements.txt .

# Install dependencies
RUN pip install -r requirements.txt

# Copy the content of the local source directory to the working directory
COPY src/ .

# Command to run on container start
CMD [ "python", "./server.py" ]

```

### Building and Running the Container

```bash
# Build the Docker image
$ docker build -t my-python-app .

# Run the container interactively and remove it upon exit
$ docker run -it --rm --name my-running-app my-python-app

```

---

## 6. Docker Base Image Choices

Choosing the right base image affects security, compatibility, and image size:

* **Full Official Image (`python:x.x.x`):**
* Based on the latest stable Debian release.
* *Best for:* Starting new projects quickly where container size is not a primary concern. The safest and most compatible choice.


* **Slim Variants (`*-slim`):**
* Installs minimal packages required to run tools.
* *Requirements:* Needs Unix administration knowledge to configure and extend based on application needs.


* **Alpine Variants (`*-alpine`):**
* Built on Alpine Linux specifically for containers.
* *Pros/Cons:* Tiny image size, making it popular for saving space. However, it can sometimes cause hard-to-debug compatibility issues with certain Python packages (leading some teams to move away from it).