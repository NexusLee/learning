#### 安装 Docker Machine
```
$ curl -L https://github.com/docker/machine/releases/download/v0.9.0/docker-machine-`uname -s`-`uname -m` >/tmp/docker-machine &&
  chmod +x /tmp/docker-machine &&
  sudo cp /tmp/docker-machine /usr/local/bin/docker-machine
```


```
$ cd /etc/bash_completion.d/
$ curl -O https://raw.githubusercontent.com/docker/machine/v0.15.0/contrib/completion/bash/docker-machine-prompt.bash
$ curl -O https://raw.githubusercontent.com/docker/machine/v0.15.0/contrib/completion/bash/docker-machine-wrapper.bash
$ curl -O https://raw.githubusercontent.com/docker/machine/v0.15.0/contrib/completion/bash/docker-machine.bash
$ vim ~/.bashrc
```
##### 添加 
```
PS1='[\u@\h \W$(__docker_machine_ps1)]\$ '
source /etc/bash_completion.d/docker-machine-prompt.bash
source /etc/bash_completion.d/docker-machine-wrapper.bash
source /etc/bash_completion.d/docker-machine.bash
```
```
$ source ~/.bashrc
```
