# Project

This project was builded to run kubernetes and Bamboo running on local with vagrant, managing all configurations with ansible.

# Development

The project was developed by [Gustavo Apolinario](https://github.com/gustavoapolinario) and [Matheus Francallaci](https://github.com/MatheusFrancallaci1) in pair programming

# Dependencies

Vagrant, Ansible, Atlassian account (Bamboo)

# How to use

## Download the .tar.gz installation file

Download the bamboo installation file to folder bamboo.

ex: bamboo/atlassian-bamboo-9.2.8.tar.gz

## Create the servers

Create the environment with vagrant up. The bamboo agent will give error, it's because the jar file isn't commited on git.

```
vagrant up
```

## Start the configuration

Open the Bamboo on localhost:8085, configure the bamboo with postgresql on ip 192.168.56.51, port 5432.

## Download the bamboo agent .jar

After configured, the bamboo will tell you to configure agent. Download the agent jar file to folder bamboo.

ex: bamboo/atlassian-bamboo-agent-installer-9.2.8.jar

## Run the configuration again

Run the provision to install the agent

```
vagrant provision bamboo-worker
```

