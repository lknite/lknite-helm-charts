A wireguard container built for centos-8-stream which takes advantage of the scripts from the linuxserver docker-wireguard project.

Source: https://github.com/lknite/docker-wireguard-centos-8-stream

LinuxServer docker-wireguard project: https://github.com/linuxserver/docker-wireguard

Note:
- Whichever node this ends up on, it must have sysctl 'net.ipv4.ip_forward=1', or it will not work
- Initial startup may take quite awhile, 4 minutes +, if the wireguard module is being recompiled. Be sure to use a volume for the modules folder to avoid having to recompile.

Sample installation script:
```
$ cat update-install
#!/bin/bash

NAME=wireguard
NS=$NAME
REPO=https://lknite.github.io/lknite-helm-charts
REPO_ALIAS=lknite
CHART=wireguard-centos-8-stream

# prep
helm repo add $REPO_ALIAS $REPO
helm repo update
touch values.yaml

# install/upgrade
helm upgrade \
        --install \
        --namespace $NS \
        --create-namespace \
        -f ./values.yaml \
        $NAME $REPO_ALIAS/$CHART
```
Troubleshooting:
- re-read the notes above and you should be good to go
