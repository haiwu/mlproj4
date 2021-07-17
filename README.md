[![CircleCI](https://circleci.com/gh/haiwu/mlproj4/tree/main.svg?style=svg)](https://circleci.com/gh/haiwu/mlproj4/tree/main)

## Project Overview

In this project, you will apply the skills you have acquired in this course to operationalize a Machine Learning Microservice API. 

You are given a pre-trained, `sklearn` model that has been trained to predict housing prices in Boston according to several features, such as average rooms in a home and data about highway access, teacher-to-pupil ratios, and so on. You can read more about the data, which was initially taken from Kaggle, on [the data source site](https://www.kaggle.com/c/boston-housing). This project tests your ability to operationalize a Python flask app—in a provided file, `app.py`—that serves out predictions (inference) about housing prices through API calls. This project could be extended to any pre-trained machine learning model, such as those for image recognition and data labeling.

### Project Tasks

Your project goal is to operationalize this working, machine learning microservice using [kubernetes](https://kubernetes.io/), which is an open-source system for automating the management of containerized applications. In this project you will:
* Test your project code using linting
* Complete a Dockerfile to containerize this application
* Deploy your containerized application using Docker and make a prediction
* Improve the log statements in the source code for this application
* Configure Kubernetes and create a Kubernetes cluster
* Deploy a container using Kubernetes and make a prediction
* Upload a complete Github repo with CircleCI to indicate that your code has been tested

You can find a detailed [project rubric, here](https://review.udacity.com/#!/rubrics/2576/view).

**The final implementation of the project will showcase your abilities to operationalize production microservices.**

---

## Setup the Environment

* Create a virtualenv and activate it
  1. python3 -m venv ~/.devops
  2. source ~/.devops/bin/activate
* Run `make install` to install the necessary dependencies
  1. make install

### Running `app.py`

1. Standalone:  `python app.py`
2. Run in Docker:  `./run_docker.sh`
3. Run in Kubernetes:  `./run_kubernetes.sh`

### Kubernetes Steps

* Setup and Configure Docker locally (Note: I am using Ubuntu 21.04 OS)
  1. echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
  2. sudo apt-get update
  3. sudo apt-get install docker-ce docker-ce-cli containerd.io
  
* Setup and Configure Kubernetes locally (Note: I am using Ubuntu 21.04 OS)
  1. curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube_latest_amd64.deb
  2. sudo dpkg -i minikube_latest_amd64.deb
  3. minikube start
* Create Flask app in Container
* Run via kubectl
  1. kubectl run mlproj4 --generator=run-pod/v1 --image="haiwu/mlproj4" --port=80 --labels app=mlproj4

### Explanation of the files in the repository

  * .circleci/config.yml: CircleCI integration file
  * Dockerfile  A text file that contains all commands, in order, needed to build a given image
  * app.py: Python flask app that serves out predictions (inference) about housing prices through API calls
  * requirements.txt: Python dependancy requirements file
  * make_prediction.sh: Shell script to invokes prediction API to get the prediction
  * run_docker.sh: Shell script to run this app in Docker
  * run_kubernetes.sh: Shell script to run this app in Kubernetes
  * upload_docker.sh: Shell script to upload docker image to DockerHub repository
  * kubernetes_out.txt: Outputs after running and testing this app on Kubernetes
  * docker_out.txt / docker_output.txt: Outputs after running and testing this app on Docker
  * model_data: Folder containing files for pre-trained, `sklearn` model
  * Makefile: Linux well-known Makefile for building convenience for this project
  * output_txt_files: Folder containing output files of kubernetes_out.txt/docker_out.txt/docker_output.txt
