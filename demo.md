# Demo

## Step 1: Install Docker 1.9 experimental
Do this on one of your AWS nodes, e.g. node 2:

    curl -sSL https://experimental.docker.com/ | sh
    sudo usermod -aG docker ubuntu
    docker --version
  > Docker version 1.9.0-dev, build 02ae137, 

## Step 2: Install Consul
Consul 

    curl -OL https://dl.bintray.com/mitchellh/consul/0.5.2_linux_amd64.zip
    sudo apt-get install unzip
    unzip 0.5.2_linux_amd64.zip
    mv consul /usr/local/bin/
    
    

