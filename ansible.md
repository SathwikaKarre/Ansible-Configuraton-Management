## Overview of Ansible

Ansible is a powerful automation tool for IT configuration management, application deployment, and task automation. It is agentless, meaning it doesn’t require installing any agents on the target systems.

## Why Use Ansible?

  Simple to use and easy to learn.
  
  Doesn’t require agents on remote machines.
  
  Ideal for configuration management and application deployment at scale.
  

## Comparison with Shell and Python Scripting for Automation

  Shell scripting: Works well for small tasks but can become complex for large-scale automation.
  
  Python scripting: More powerful, but requires the installation of Python libraries and setup on remote systems.
  
  Ansible: Does not require agents or additional setup, works in an idempotent manner, and is much easier for system administrators to understand.


# Installing Ansible

## Ubuntu/Debian:

  sudo apt update
  sudo apt install ansible

## CentOS/Red Hat:

  sudo yum install ansible

## Windows: 
  
  Use WSL (Windows Subsystem for Linux) to install Ansible.


## IDE and Plugin Configuration

## VS Code:

  Install the Ansible extension from the marketplace to provide syntax highlighting, autocompletion, and other useful features for writing Ansible playbooks.



## Ansible Ad-Hoc Commands

Passwordless Authentication

Set up passwordless SSH authentication to allow Ansible to manage remote machines without needing to enter a password every time:

    ssh-keygen -t rsa
    ssh-copy-id user@remote_host

## Ansible Inventory

The inventory is where you define your hosts, whether it's a simple file or a dynamic script that fetches the host list.

Example of a Static Inventory:

[webservers]
192.168.1.10

[dbservers]
192.168.1.20


### Ad-Hoc Commands

Ansible allows you to run commands directly without creating playbooks.

Example: Install a package using apt:

    ansible webservers -m apt -a "name=nginx state=present"


Ad-hoc commands are ideal for quick one-off tasks like checking service status or installing packages.

## Writing Your First Ansible Playbook

YAML Basics and Playbook Structure

Ansible playbooks are written in YAML format, which is human-readable and easy to understand.

Basic structure of a Playbook:


- name: Install NGINX and Deploy Static App

  hosts: webservers
  
  become: yes
  
  tasks:
  
    - name: Install NGINX
      
      apt:
      
        name: nginx
  
        state: present
      
        update_cache: yes


## Understanding Playbook Structure:

Playbook: Contains one or more plays, and each play defines tasks to be run on a specific set of hosts.

Play: Defines a group of tasks that should be run on a particular set of hosts.

Modules: The building blocks in Ansible used to execute tasks (e.g., apt, service, copy).

Tasks: The individual actions that Ansible will perform (e.g., installing a package).

Collections: Collections allow you to group related playbooks, roles, and modules for easy reuse.


## Hands-on Example: Installing Apache2 and Deploying a Static App on AWS

1. Create a playbook (apache2_playbook.yml) to install Apache2.


2. Deploy a simple static HTML page on AWS instances.



### Understanding Ansible Roles

What Are Ansible Roles?

Roles are a way to organize your Ansible code into reusable components, making your playbooks more modular and easier to manage.

Folder structure of Ansible roles:

      roles/
      
        nginx/
        
          tasks/
          
            main.yml
            
          templates/
          
            nginx.conf.j2
            
          files/
          
            index.html
            
          handlers/
          
            main.yml
            
          defaults/
          
            main.yml


## Why Use Roles?

Reusability: A role can be reused in multiple playbooks.

Organization: Roles help organize tasks, templates, files, and other components in a standardized way.
Comparing Roles with Playbooks

Playbooks are used for orchestration and can reference roles.

Roles encapsulate logic and structure, promoting modularity.


## Hands-on: Creating a Simple Role

Create a role for setting up an NGINX server:

1. Define tasks to install and configure NGINX.


2. Use variables and templates for configuration.


3. Call the role in a playbook.



## Deep Dive into Ansible Roles with Demo

## Ansible Galaxy

Ansible Galaxy is a hub for finding, sharing, and reusing Ansible roles. You can search for popular roles on Ansible Galaxy.

Importing and Installing Roles from Ansible Galaxy

You can import roles from Galaxy into your project by using the following command:

      ansible-galaxy install <role-name>

## Demo: Advanced Usage of Ansible Roles

In this demo, we’ll showcase the use of Ansible roles with a real project. The project will involve installing and configuring NGINX with advanced settings using roles and templates.


Best Practices for Organizing Roles and Playbooks

Keep roles isolated and focused on a single task.

Use a defaults/main.yml file to define default variables.

Keep templates and files within appropriate subdirectories under the role.
