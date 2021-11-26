# An OpenAI Gym docker that can render on Windows
This image starts from the jupyter/tensorflow-notebook, and has atari_py installed. Therefore, many environments can be played.

This image is made for running OpenAI Gym on Windows. But in general, it works on other OS like Linux, MacOS etc. as well.

## Prerequisite
* [Windows Subsystem for Linux WSL](https://docs.microsoft.com/en-us/windows/wsl/install)
* [Docker Desktop](https://www.docker.com/products/docker-desktop)
* [VcXsrv Windows X Server](https://sourceforge.net/projects/vcxsrv/)

## Description
* [Dockerfile](./Dockerfile): Dockerfile to build the OpenAI Gym image
* [example](./example): Some example notebooks for testing
* [example/env_render.ipynb](./example/env_render.ipynb): Test Gym environments rendering
* [example/18_reinforcement_learning.ipynb](./example/18_reinforcement_learning.ipynb): This is a copy from Chapter 18 in Géron, Aurélien's book: Hands-On Machine Learning with Scikit-Learn, Keras, and TensorFlow.  Source code is [here](https://github.com/ageron/handson-ml2/blob/master/18_reinforcement_learning.ipynb) in GitHub.

## Build the image
```
docker build -t openai_gym_docker:v1.0 .
```

## Create and run the instance of the container

Get the Network InterfaceAlias name using the below command
```
netsh interface ipv4 show interface
```

Customize the number of CPUs and Memory in the below command according to your system specifications. Also update Network InterfaceAlias from previous command
```
docker run -itd --name=openai-gym -p 8888:8888 --cpus='3' --memory='6g' --add-host=dockerhost:$(Get-NetIPAddress -AddressFamily IPv4 -InterfaceAlias 'Wi-Fi' | Select-Object -ExpandProperty 'IPAddress';) -e DISPLAY=dockerhost:0.0 openai_gym_docker:v1.0
```

## Get Jupyter token
```
docker exec -it openai-gym bash -c 'jupyter notebook list'
```

Once the docker instance starts running, open browser and visit [http://localhost:8888](http://localhost:8888) and login with the token from above.

Jupyter will promt you to set new password for future logins.

Create/Import Python Notebooks and start exploring Reinforcement Learning 🤖

## Stop the container
```
docker stop openai-gym
```

## Start the container
```
docker start openai-gym
```