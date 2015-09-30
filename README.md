# dockerTTT_net19_presentation
Group session exercise to present about the new networking features in Docker 1.9

## Update kernel to 3.16
```
sudo apt-get install linux-image-generic-lts-utopic
sudo reboot
```

## Install docker 1.9 procedure
```
curl -sSL https://experimental.docker.com/ | sh
sudo usermod -aG docker ubuntu
docker --version
```
  > Docker version 1.9.0-dev, build 02ae137, 

## Install Consul 
```
curl -OL https://dl.bintray.com/mitchellh/consul/0.5.2_linux_amd64.zip
unzip 0.5.2_linux_amd64.zip
mv consul /usr/local/bin/
```
### On the first node:
```
consul agent -server -bootstrap -data-dir /tmp/consul -bind=<host-1-ip-address>
```

### On the other nodes:
```
consul agent -data-dir /tmp/consul -bind=$(ifconfig eth0 | grep "inet addr" | awk -F: '{print $2}' | awk '{print $1}') -node <mynodename>
consul join <host-1-ip-address>
```
Put the following in your `/etc/default/docker` file:
```
DOCKER_OPTS="-H unix:///var/run/docker.sock -H tcp://0.0.0.0:2375 --kv-store=consul:localhost:8500 --label=com.docker.network.driver.overlay.bind_interface=eth0 --label=com.docker.network.driver.overlay.neighbor_ip=<your local 10.0.10.xx IP>"
```
And restart the docker daemon `sudo service docker restart`.
