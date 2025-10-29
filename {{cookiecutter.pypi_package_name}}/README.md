# {{ cookiecutter.project_name }}

![PyPI version](https://img.shields.io/pypi/v/{{ cookiecutter.package_name }}.svg)
[![Documentation Status](https://readthedocs.org/projects/{{ cookiecutter.package_name }}/badge/?version=latest)](https://{{ cookiecutter.package_name }}.readthedocs.io/en/latest/?version=latest)

{{ cookiecutter.project_short_description }}

* PyPI package: https://pypi.org/project/{{ cookiecutter.package_name }}/
* Free software: MIT License
* Documentation: https://{{ cookiecutter.package_name }}.readthedocs.io

---

## Overview

**{{ cookiecutter.project_name }}** is a general-purpose Python agent that provides a sandboxed environment for executing Python code to accomplish user-defined tasks. It leverages a Large Language Model (LLM) to interpret natural language instructions, generate Python code, and execute it securely within a Docker container. The agent interacts through an embedded [Jupyter kernel](https://docs.jupyter.org/en/latest/projects/kernels.html), iteratively writing and running code until the task is complete.

This project was initialized using [Cookiecutter](https://github.com/audreyfeldroy/cookiecutter) and the [audreyfeldroy/cookiecutter-pypackage](https://github.com/audreyfeldroy/cookiecutter-pypackage) project template.

---

## Intended Use

The agent is designed for any workflow where Python can be used to automate, analyze, or solve problems.  
It is ideal for:

- Automated data processing
- Experimentation and code execution in isolation
- Safe evaluation of generated or external code
- Dynamic and iterative problem-solving guided by an LLM

---

## Environment Requirements

To run this agent, a Docker daemon must be available and running on the host machine.  
The agent itself is a Python command-line application that pulls a specified Docker image (default: [jupyter/datascience-notebook:latest](https://hub.docker.com/r/jupyter/datascience-notebook/)) to create a secure execution environment.

---

## Tools

The agent exposes several core tools for operation:

- `execute_code`: Runs Python code within the Jupyter kernel session.
- `restart_kernel`: Restarts the interactive session to reset the execution state.
- `complete_task`: Marks a task as complete, providing a summary of the results.

---

## Features

- **Sandboxed Execution**: All code runs inside an isolated Docker container to protect the host system.
- **Customizable Environment**: Choose any Docker image as the runtime, and mount local directories as volumes for persistence.
- **LLM-Powered Automation**: Accepts high-level natural language tasks and translates them into executable Python code.
- **Interactive Execution Loop**: Allows for iterative reasoning, executing code step by step while maintaining session state.
- **Task Completion Reporting**: Provides explicit success/failure outcomes and structured summaries of execution.
- **Controlled Iteration**: The agent enforces a `max_steps` limit to guarantee termination of tasks.
- **Artifact Logging**: Optionally logs the working directory and outputs to Dreadnode or other systems for record-keeping.

---

## Future Work

* Implement enhanced debugging and tracing tools.
* Add multi-language kernel support.
* Integrate configurable logging backends and observability hooks.

---

## Credits

This package was created with [Cookiecutter](https://github.com/audreyfeldroy/cookiecutter) and the  
[audreyfeldroy/cookiecutter-pypackage](https://github.com/audreyfeldroy/cookiecutter-pypackage) template.

---

## References

- [Jupyter Kernel Documentation](https://docs.jupyter.org/en/latest/projects/kernels.html)
- [Docker Hub: jupyter/datascience-notebook](https://hub.docker.com/r/jupyter/datascience-notebook/)
