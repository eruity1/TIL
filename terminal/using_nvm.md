# Using NVM
Node Version Manager (NVM) is a tool for managing Node versions on your device.
Instead of using npm to install and uninstall Node versions for different project, you can use NVM to help you effectively manage your node versions for each project.
NVM allows you to install different versions of Node and to switch between these versions depending on the project you are working on.

## Check Your Node Versions
```bash
nvm ls
```
Example output:
```bash
       v16.20.2
       v18.20.8
->      v24.1.0
         system
default -> node (-> v24.1.0)
```
`->` will show your current active version
`default ->` shows which version is used by default

## Install a Node Version
```bash
nvm install vX.Y.Z
```

## Switch to a Different Installed Version
```bash
nvm use 16.20.2
```

## Set Default Version
```bash
nvm alias default 16.20.2
```

## Create a Custom Alias
```bash
nvm alias fav-node 18.20.8
nvm use fav-node
``` 
