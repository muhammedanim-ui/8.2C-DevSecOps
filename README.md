# 8.2C-DevSecOps

## Jenkins DevSecOps Pipeline

This repository contains the `nodejs-goof` vulnerable Node.js application used for the **8.2C DevSecOps assessment**.

The project is used to demonstrate security testing and DevSecOps practices using Jenkins and npm.

## Project

The original project is:

https://github.com/snyk-labs/nodejs-goof

`nodejs-goof` is an intentionally vulnerable Node.js application designed for security testing and demonstration purposes.

## Jenkins Pipeline

The Jenkins pipeline performs the following stages:

1. **Checkout** – Retrieves the project from GitHub.
2. **Install Dependencies** – Installs the required npm dependencies.
3. **Run Tests** – Runs the project's npm tests.
4. **Generate Coverage Report** – Generates the test coverage report.
5. **NPM Audit (Security Scan)** – Uses `npm audit` to identify known vulnerabilities in project dependencies.

## Technologies Used

* GitHub
* Jenkins
* Node.js
* npm
* npm audit
* JUnit
* JavaScript

## Purpose

The purpose of this repository is to demonstrate basic DevSecOps practices by integrating security testing into a Jenkins CI pipeline.

The project intentionally contains vulnerable dependencies so that security vulnerabilities can be identified using `npm audit`.

## Assessment

**Unit:** DevSecOps
**Task:** Part 1 – Task 2: DevSecOps Basics
**Repository:** `8.2C-DevSecOps`

