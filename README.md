# wslDockerWithoutDockerDesktop
Configure Windows to have Docker wihtout DockerDesktop

## Install
- WSL: https://docs.microsoft.com/es-es/windows/wsl/install-manual
- Install Docker https://dev.to/bowmanjd/install-docker-on-windows-wsl-without-docker-desktop-34m9
```
  sudo apt update
  sudo apt install --no-install-recommends apt-transport-https ca-certificates curl gnupg2
  curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
  echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
  sudo apt-get update
  sudo apt-get install -y docker-ce docker-ce-cli containerd.io
  sudo usermod -aG docker $USER
  sudo service docker start  / stop / status
  sudo docker run hello-world
```

- Docker client (o https://github.com/StefanScherer/docker-cli-builder o https://download.docker.com/)
```
 choco install docker-cli
```

- Poweshell client to startup docker (execute as admin in x64):
```
  $ip = (wsl sh -c "hostname -I").Split(" ")[0]
  netsh interface portproxy add v4tov4 listenport=2375 connectport=2375 connectaddress=$ip
  wsl sh -c "sudo dockerd -H tcp://$ip -H unix:///var/run/docker.sock"
```

- Configure clients (IntelliJ, VisualStudio): tcp://localhost:2375
- Deploy Docker Monitoring+Desktop alternative: https://docs.portainer.io/v/ce-2.9/start/install/server/docker/wsl 
- Add environment variable DOCKER_HOST=tcp://localhost:2375

#### Docker on Windows
- https://docs.docker.com/engine/install/binaries/#install-server-and-client-binaries-on-windows

#### Docker compose
- https://docs.docker.com/compose/cli-command/#install-on-linux
