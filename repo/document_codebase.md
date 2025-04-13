Prompt:
Task:
You are a code analysis and documentation expert. Your objective is to analyze the provided codebase and generate a comprehensive documentation that outlines every folder, file, and—when applicable—every function and class defined in the code. Note that for some files (like templates, JSON data, and Markdown files), details about functions might not be applicable.

Instructions:

Introduction & Overview:
Start with an introductory paragraph explaining that this document provides a complete breakdown of the repositories.
Identify each repository and briefly describe its purpose.
Folder Structure Overview:
Present the entire folder structure in a tree-like format. Use lines and indents to represent the directory hierarchy.
Include paths (if available) and list all folders and files.
Detailed File & Folder Breakdown:
For each folder:
Provide a brief description of the folder’s purpose.
For each file within a folder:
State the file name and its purpose.
List the key components such as functions, classes, modules, or templates contained in the file.
For each function or class (if applicable), include:
Name: The function or class name.
Purpose: A summary or docstring (if available) explaining what it does.
Imports & Dependencies: Key libraries or modules imported.
Workflow & Key Parameters: A summary of its logic, parameters, or expected outputs.
If the file is a template, JSON, or Markdown file, note that detailed function breakdowns may not apply. 
Special Components & Core Functionality:
For files implementing core functionality (e.g., API endpoints, agent pipelines, search functions, logging), provide additional details:

Explain how different components interact.
Describe any configuration or model definitions used (e.g., Pydantic models, enums).
Mention execution blocks (such as “if name == 'main':”) and what they do.
Top-Level Files:
Provide a summary for additional top-level files such as:
LICENSE: Describe the license details.
README.md: Summarize the project’s overall description, installation instructions, usage, and contribution guidelines.
requirements.txt & setup.py: Explain their roles in listing dependencies and configuring the package.
Formatting & Hierarchical Organization:
Use hierarchical numbering (e.g., I, II, III or A, B, C) and bullet points to clearly delineate sections, folders, files, and detailed breakdowns.
Make sure the output is well-organized and easy to follow.
Input:
The complete codebase structure (including file names, directory paths, and content snippets where applicable).

Output:
A detailed, formatted documentation that includes:

An introductory overview.
A tree-like folder structure.
Detailed breakdowns for every folder and file (including key functions, classes, and components).
Additional summaries for any top-level configuration or documentation files.
-----