# Dockerfile Bug: Missing Test Dependencies

This repository demonstrates a common error in Dockerfiles: failing to include necessary dependencies for the application's build and execution.  The original `Dockerfile` attempts to run unit tests using `unittest`, but fails because the `unittest` module, and even the Python interpreter, are not included in the base `ubuntu:latest` image.  This leads to a runtime error in the Docker container.

The solution demonstrates the use of a more appropriate base image such as `python:3.9-slim-buster` which contains Python and pip. 

## How to Reproduce the Bug
1. Clone this repository.
2. Build the original Dockerfile using `docker build -f Dockerfile -t test-image .`
3. Attempt to run the container using `docker run test-image`.
4. Observe the error indicating that the `python3` command is not found.

## Solution
The corrected `Dockerfile.fixed` uses a more appropriate Python-based base image, thereby avoiding the dependency issue.  Build the corrected Dockerfile using `docker build -f Dockerfile.fixed -t test-image-fixed .` and run using `docker run test-image-fixed`. The tests should now run successfully.