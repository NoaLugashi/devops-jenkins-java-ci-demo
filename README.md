# DevOps Jenkins CI Demo

This repository contains a small Java project that I used to practice basic DevOps concepts with Jenkins and GitHub.

The goal of the project is not the Java code itself, but the CI pipeline around it: automatic compilation and execution using Jenkins jobs that are triggered by changes in the Git repository.

---

## Overview

The project includes two simple Java classes:

- `Hello.java` – prints "Hello World :)" multiple times.
- `NoaLugashi.java` – prints my name and an index in a loop.

Jenkins is configured with four freestyle jobs that work together as a simple CI pipeline.

---

## Technologies

- **Jenkins** – CI server (freestyle jobs)
- **Git & GitHub** – source code management
- **Java** – basic console application
- **Windows** – Jenkins node / agent

---

## Jenkins Jobs

The pipeline is built from four jobs:

1. **CI-Compile-Hello**  
   - Triggers on changes in this GitHub repository  
   - Checks out the code  
   - Compiles `Hello.java` using `javac`

2. **CI-Run-Hello**  
   - Triggered by *CI-Compile-Hello*  
   - Compiles and runs `Hello.java`  
   - Prints the output to the Jenkins console log

3. **CI-Compile-NoaLugashi**  
   - Triggered by *CI-Run-Hello*  
   - Compiles `NoaLugashi.java` using `javac`

4. **CI-Run-NoaLugashi**  
   - Triggered by *CI-Compile-NoaLugashi*  
   - Compiles and runs `NoaLugashi.java`  
   - Prints the output to the Jenkins console log

The jobs are configured as an upstream/downstream chain, so a single change in the repository can trigger the whole flow.

---

## How it works

1. I push a change to this repository on GitHub.
2. Jenkins detects the SCM change and runs **CI-Compile-Hello**.
3. If the compilation is successful, **CI-Run-Hello** runs and executes the program.
4. On success, the next jobs (**CI-Compile-NoaLugashi** and **CI-Run-NoaLugashi**) are triggered.
5. The full output can be seen in the Jenkins build logs.

This small setup demonstrates continuous integration basics:
- automatic build on source changes
- chaining jobs into a simple pipeline
- storing build history and logs on the CI server

---

## Repository Structure

```text
.
├── Hello.java
├── NoaLugashi.java
└── README.md
