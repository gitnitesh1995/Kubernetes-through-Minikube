**Kubernetes through Minikube**

****![](https://lh7-us.googleusercontent.com/NNoiaMtfRYOluLkH-FzQK67cQF26uHJEgJ5g-pTn69viGvSBoy46ZkpvutWwLwCgDvR8-Xxm60dXlKaJC4twkUjxSnGwGooTanvwndd2r2ZVdc7OlTwsApLQfYOrh8ViBF8BZAakehjm-MDRouKsxpA)****

****![](https://lh7-us.googleusercontent.com/ryiJNr2L19L6LX46ABw2lzW-bHUBJNaTSFbD4gUz7IpQYbBbNACGLdUUl9guPpxLoQvkrqy2Pi3rg-hIaXTw8LK778O75BUqJm7_z0eP5XvUh9QIJYioVvfk12YwfiTePUHArwwwrA8QHM40CZqoUOI)****

****![](https://lh7-us.googleusercontent.com/iU4MpnC3qO3Ee_CZAMPIWh9VkUjwtm0hV8B3OchXsBjS9h9mnYckD9G_OKOyUDuicraxIFeqZhrXEQdxYARmmgFRa2g9nr-z9CKSlHwQJWrFOgVjiXmY6hzMGDRm0QJgXSWkhagyckuSwiGwWR2Ysjo)****

**Table of Contents**

[System Requirements](#system-requirements)

[Pre- requisite](#pre--requisite-)

[Install Docker ](#install-docker)

[Install kubectl ](#install-kubectl)

[Install Minikube](#install-minikube)


# System Requirements<a id="system-requirements"></a>

**Operating System :** Ubuntu 22.04.3 LTS

**CPU :** 2 Cores or more

**RAM :** 2 GB or More

**Storage :** At Least 20 GB


# Pre- requisite :<a id="pre--requisite-"></a>

Install curl


# Install Docker<a id="install-docker"></a>
```
sudo apt update && sudo apt upgrade -y
```
This command updates the local package database, ensuring your system has the latest information about available packages and their versions and upgrade command upgrades all installed packages to their latest versions. The -y flag is used to automatically answer "yes" to any prompts, making the upgrade process non-interactive
```
sudo apt-get install ca-certificates curl gnupg
```
**sudo :**

It stands for "superuser do" and  permits user to execute a command as the superuser 

**apt-get :**

apt-get is a command-line tool used for package management on Debian-based systems. It allows users to install, upgrade, or remove software packages.

**install :**

This is an argument specifying that the operation to be performed is the installation of one or more packages.

**ca-certificates :**

This is the name of the first package to be installed. It includes a set of trusted certificate authorities (CAs) that the system can use to verify the authenticity of SSL/TLS certificates.

**curl :**

This is the name of the second package to be installed. curl is a command-line tool for making HTTP requests. It is often used for downloading files, interacting with APIs, and testing web services.

**gnupg :**

This is the name of the third package to be installed. gnupg (GnuPG) is a complete and free implementation of the OpenPGP standard. It is used for secure communication and data integrity verification.
```
sudo install -m 0755 -d /etc/apt/keyrings
```
**sudo :**

It stands for "superuser do" and  permits user to execute a command as the superuser 

**install :**

install is a Unix command that is typically used for copying files and setting attributes during the copy process. In this case, it's being used to create a directory.

**-m 0755 :**

The -m flag specifies the permissions (mode) to set for the directory being created. In this case, 0755 represents the octal notation for the permissions. Here's the breakdown:
0: No special permissions.
7: Read, write, and execute permissions for the owner.
5: Read and execute permissions for the group.
5: Read and execute permissions for others (users not in the owner or group).

**-d :**

The -d flag is used to indicate that the install command should treat the destination as a directory. It ensures that the specified path is treated as a directory, and the directory is created if it doesn't exist.
/etc/apt/keyrings:

This is the path of the directory being created. In Linux, the /etc directory is typically used for system-wide configuration files, and /etc/apt/keyrings is a specific directory path where keyring files related to package management (APT) may be stored.
 
```
curl -fsSL https\://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```
 This downloads the Docker GPG key, and gpg --dearmor converts it into a format suitable for APT. The output is saved to /etc/apt/keyrings/docker.gpg.
```
sudo chmod a+r /etc/apt/keyrings/docker.gpg 
```
**sudo :**

It stands for "superuser do" and  permits user to execute a command as the superuser.

**chmod :**

chmod is a Unix command used to change the permissions of a file or directory.

**a+r :**

The a+r specifies the permissions to be added. In this case, it stands for "all users" (owner, group, and others) and "read" permission.

**/etc/apt/keyrings/docker.gpg :**

This is the path of the file for which the permissions are being modified. /etc/apt/keyrings is the directory, and docker.gpg is the specific file.

```
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
**echo : **

This command is used to print the Docker repository configuration to the console.

**deb \[arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https\://download.docker.com/linux/ubuntu $(. /etc/os-release && echo "$VERSION\_CODENAME") stable :**

This is the actual configuration line that specifies the Docker repository. It includes information about the system architecture, the GPG key for signature verification, the Docker repository URL, and the Ubuntu version codename.

sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

This part of the command takes the output of the echo command and writes it to the file /etc/apt/sources.list.d/docker.list. tee is used to write to the file, and > /dev/null is used to suppress the output on the console.
```
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
This command installs the Docker engine (docker-ce), the Docker command-line interface (docker-ce-cli), and containerd (containerd.io). These are the core components needed to run Docker containers.

As for the additional components you mentioned (docker-buildx-plugin and docker-compose-plugin), they are not standard Docker packages. Docker Buildx and Docker Compose are separate tools that you might install and use depending on your specific needs.
```
sudo apt-get update
```
**sudo :**

It stands for "superuser do" and  permits user to execute a command as the superuser.

**apt-get :**

This is the package management command-line tool on Debian-based systems. It's used for handling packages—installing, updating, and removing them.

update: This specific sub-command is telling apt-get to update its package information. It doesn't actually update the packages themselves; instead, it fetches the latest information about available packages from the repositories.
```
sudo docker run hello-world
```
**sudo :**

It stands for "superuser do" and  permits user to execute a command as the superuser.

**docker run :**

This command is used to run a Docker container.

**hello-world :**

This is the name of the Docker image you are running. In this case, it's a simple and lightweight image provided by Docker called "hello-world."


# Install kubectl<a id="install-kubectl"></a>
```
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
```
**curl -s [**https://dl.k8s.io/release/stable.txt**](https://dl.k8s.io/release/stable.txt) :**

 This command fetches the latest stable version of Kubernetes from the stable.txt file on the Kubernetes release page.

**$(curl -L -s [**https://dl.k8s.io/release/stable.txt**](https://dl.k8s.io/release/stable.txt)**) :**

 This part of the command uses command substitution to include the version obtained in step 1 in the URL.<https://dl.k8s.io/release/>\<version>/bin/linux/amd64/kubectl

 This is the URL structure for the kubectl binary for Linux amd64 architecture.
```
curl -LO "https\://dl.k8s.io/release/$(curl -L -s [https://dl.k8s.io/release/stable.txt](https://dl.k8s.io/release/stable.txt))/bin/linux/amd64/kubectl"
```
 This final command downloads the kubectl binary using the constructed URL and the -LO flags to save the file with the same name as the remote file.
```
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
```
**sudo :**

It stands for "superuser do" and  permits user to execute a command as the superuser.

**install :**

 This is the install command, used to copy files and set attributes.

**-o root -g root :**

 This sets the owner (-o) to root and the group (-g) to root. It ensures that the kubectl binary is owned by the root user and root group.

**-m 0755 :**

 This sets the file permissions (-m) to 0755. It grants read, write, and execute permissions to the owner (root) and read and execute permissions to others. This makes the kubectl binary executable by everyone.

**kubectl :**

This is the source file (the kubectl binary you downloaded).

**/usr/local/bin/kubectl :**

 This is the destination path where the kubectl binary will be installed.
```
kubectl version --client
```

The kubectl version --client command is used to check the client-side version of kubectl installed on your machine. It will display information about the Kubernetes client and the Kubernetes API server it interacts with.


# Install Minikube <a id="install-minikube"></a>
```
curl -LO https\://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
```
curl -LO [https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64](https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64)

This uses curl to download the latest Minikube binary for Linux (minikube-linux-amd64) from the specified URL.

sudo install minikube-linux-amd64 /usr/local/bin/minikube

 This install the downloaded binary into the /usr/local/bin directory, making it accessible system-wide. The install command is used with sudo to ensure the necessary permissions.
```
sudo usermod -aG docker $USER && newgrp docker
```
**sudo :**

It stands for "superuser do" and  permits user to execute a command as the superuser.

**usermod :**

Modifies a user account.

**-aG docker :** 

Adds the user to the specified groups. Here, it's adding the user to the "docker" group.

**$USER :**  

Represents the current username.

So, this part is making you a member of the "docker" group.

**newgrp :**  

This command is used to change your current group ID during a login session.

**docker :**

The group you want to switch to.
```
minikube start
```
**minikube** 

This is the command-line tool for managing and interacting with Minikube, which is a tool that helps you run Kubernetes clusters locally for development and testing purposes.

**start**

This subcommand is telling Minikube to start a new Kubernetes cluster. When you run minikube start, it sets up a single-node Kubernetes cluster on your local machine.

**Create a file named “nginx-deployment.yaml”**
```
vi nginx-deployment.yaml
```
**vi**

This is a command-line text editor available on many Unix-like systems. It stands for Visual Editor.

**nginx-deployment.yaml**

This is the filename you want to open in the vi editor. It suggests that you're dealing with a YAML file, commonly used for defining Kubernetes resources like deployments.

Press i for “Write the following script”
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:latest
        ports:
        - containerPort: 80

````
 Press “Esc  :wq” to save

```
kubectl apply -f app-deployment.yaml
```
**kubectl :** This is the command-line tool for interacting with Kubernetes clusters.

**apply :** This subcommand is used to apply a configuration to a resource. It's commonly used to create, update, or delete resources described in a YAML or JSON file.

**-f :** This flag is followed by the filename or URL of the resource configuration file in YAML or JSON format. It specifies the file to be applied to the cluster.

 **nginx-deployment.yaml  :** This is the YAML file that contains the specifications for your application deployment, such as the container image, replicas, ports, etc. It is the deployment file name.

**Create nginx-service.yaml** 
```
vi nginx-service.yaml
```
**vi :**

This is a command-line text editor available on many Unix-like systems. It stands for Visual Editor.

**nginx-service.yaml :**

This is the filename you want to open in the vi editor. The file extension ".yaml" suggests that you're dealing with a YAML file, which is commonly used for defining Kubernetes resources, and in this case, it could be a service configuration.

Press i for “Write the following script”
```
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  selector:
    app: nginx
  ports:
  - protocol: TCP
    port: 80
    targetPort: 80
  type: NodePort

```
Press “Esc  :wq” to save

```
kubectl apply -f nginx-service.yaml
```
**kubectl :** 

This is the command-line tool for interacting with Kubernetes clusters.

**apply :**

This subcommand is used to apply a configuration to a resource. It's commonly used to create, update, or delete resources described in a YAML or JSON file.

**-f :** 

This flag is followed by the filename or URL of the resource configuration file in YAML or JSON format. It specifies the file to be applied to the cluster.

**nginx-service.yaml :**

This is the YAML file that contains the configuration for your Kubernetes service. It specifies how the service should be set up, including details like the service type (NodePort, LoadBalancer, ClusterIP), ports, selectors to route traffic to pods, etc.
```
minikube service nginx-service
```
**minikube :** 

The command-line tool for managing Minikube and Kubernetes clusters.

**service :**

 This is a subcommand of Minikube used to expose a Kubernetes service.

**nginx-service :**

 The name of the Kubernetes service you want to expose. Replace this with the actual name of the service you have deployed in your cluster.
```
kubectl get pods,svc,deploy
```
**kubectl :** 

The command-line tool for interacting with Kubernetes clusters.

**get :**

 This is a command to retrieve resources from the cluster.

**pods,svc,deploy :** 

These are the resource types you're asking for:

**pods :**

Fetches information about running pods in the cluster.

**svc or services :**

Retrieves details about services.

**deploy or deployments :**

Fetches information about deployments.
```
minikube stop
```
**minikube :**

The command-line tool for managing Minikube and Kubernetes clusters.

**stop :**

This is a subcommand of Minikube used to stop a running cluster.
```
 minikube delete
```
**minikube :**

The command-line tool for managing Minikube and Kubernetes clusters.

**delete :**

This subcommand is used to delete an existing Minikube cluster.
