# Docker-chrome

[![Build Status](https://travis-ci.org/JinWuZhao/docker-chrome.svg?branch=master)](https://travis-ci.org/JinWuZhao/docker-chrome) ![GitHub release](https://img.shields.io/github/tag/JinWuZhao/docker-chrome.svg)

Chrome browser in docker container.  

Improves Chinese font display of the chrome image in https://github.com/jessfraz/dockerfiles.git.  


## Dependences
- Linux Operation System with X-Org or Wayland.
- docker
- [x11docker](https://github.com/mviereck/x11docker.git)
- xpra (optional)
- Xvfb (optional dependence of xpra)
- nxagent (optional)
- pulseaudio (provide audio, optional)

## Usages
- Launch Chrome as seamless applications:
```
x11docker --lang=zh_CN.UTF-8 --nxagent --pulseaudio --clipboard -- jinwuzhao/chrome --no-sandbox
```

- Launch Chrome in xpra environment:
```
x11docker --lang=zh_CN.UTF-8 --xpra --pulseaudio --clipboard -- jinwuzhao/chrome --no-sandbox
```

## Trouble Shooting
- Error: Only console users are allowed to run the X server
If the execution fails with this error message in the log file you need to make the following changes:  
Create the file /etc/X11/Xwrapper.config with the content  
```
/etc/X11/Xwrapper.config
allowed_users=anybody
```

- The browser often crashes.
Generally because of the default resource limits of docker.  
I recommend to launch Chrome likes this:  
```
x11docker --lang=zh_CN.UTF-8 --nxagent --pulseaudio --clipboard -- --cpus=2 --memory=1g --shm-size=1g -- jinwuzhao/chrome --no-sandbox
```
