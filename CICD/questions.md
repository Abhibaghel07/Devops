Q1: What is CI/CD and why is it important?
A: CI/CD stands for Continuous Integration and Continuous Deployment. It is a set of practices that enable development teams to deliver code changes more frequently and reliably. CI involves automatically testing and integrating code changes into a shared repository, while CD automates the deployment of these changes to production. This process reduces manual errors, improves software quality, and accelerates the release cycle.

Q2: How do you implement a CI/CD pipeline using Jenkins?
A: To implement a CI/CD pipeline using Jenkins, I would:

Set up a Jenkins server and configure necessary plugins.
Create a new pipeline job and define the pipeline script using either the declarative or scripted syntax.
Integrate version control systems like Git to trigger builds on code commits.
Define stages for building, testing, and deploying the application.
Use Jenkins agents to run builds in isolated environments.
Monitor the pipeline execution and set up notifications for failures.