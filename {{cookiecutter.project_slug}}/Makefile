# Makefile for {{cookiecutter.package_name}}

# Default target: show available commands
.PHONY: list requirements qa testall test pdb coverage build version tag clean clean-build clean-pyc clean-test
.SILENT: list requirements qa testall test pdb coverage build version tag clean clean-build clean-pyc clean-test

list:
	@echo "Available targets:"
	@awk -F: '/^[a-z0-9][^:]*:/ && $$1 != "VERSION" {print "  " $$1}' Makefile

# Install requirements
requirements:
	uv sync --all-extras --dev &&\
	find . -name '*.egg-info' -exec rm -fr {} +

# Run all the formatting, linting, and testing commands
qa:
	uv run --python=3.13 --extra test ruff format .
	uv run --python=3.13 --extra test ruff check . --fix
	uv run --python=3.13 --extra test ruff check --select I --fix .
	uv run --python=3.13 --extra test ty check .
	uv run --python=3.13 --extra test pytest .

# Run all the tests for all supported Python versions
testall:
	uv run --python=3.10 --extra test pytest
	uv run --python=3.11 --extra test pytest
	uv run --python=3.12 --extra test pytest
	uv run --python=3.13 --extra test pytest

# Run tests, allowing arguments to be passed (e.g., make test ARGS="tests/test_example.py")
test:
	@echo "Running with args: $(ARGS)"
	uv run --python=3.13 --extra test pytest $(ARGS)

# Run tests, dropping into the debugger on failure
pdb:
	@echo "Running with args: $(ARGS)"
	uv run --python=3.13 --extra test pytest --pdb --maxfail=10 --pdbcls=IPython.terminal.debugger:TerminalPdb $(ARGS)

# Run coverage and generate HTML report
coverage:
	uv run --python=3.13 --extra test coverage run -m pytest .
	uv run --python=3.13 --extra test coverage report -m
	uv run --python=3.13 --extra test coverage html

# Build the project
build:
	rm -rf build dist
	uv build

# Extract version number from pyproject.toml
VERSION := $(shell grep -m1 '^version' pyproject.toml | sed -E 's/version = "(.*)"/\1/')

# Print the current version of the project
version:
	@echo "Current version is $(VERSION)"

# Tag the current version in git and push to GitHub
tag:
	@echo "Tagging version v$(VERSION)"
	git tag -a v$(VERSION) -m "Creating version v$(VERSION)"
	git push origin v$(VERSION)

# Clean commands
clean: clean-build clean-pyc clean-test

clean-build:
	rm -fr build/ dist/ .eggs/
	find . -name '*.egg-info' -exec rm -fr {} +
	find . -name '*.egg' -exec rm -f {} +

clean-pyc:
	find . -name '*.pyc' -exec rm -f {} +
	find . -name '*.pyo' -exec rm -f {} +
	find . -name '*~' -exec rm -f {} +
	find . -name '__pycache__' -exec rm -fr {} +

clean-test:
	rm -f .coverage
	rm -fr htmlcov/ .pytest_cache
