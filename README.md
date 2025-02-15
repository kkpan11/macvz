[![Go Report Card](https://goreportcard.com/badge/mac-vz/macvz)](https://goreportcard.com/report/github.com/mac-vz/macvz)
[![Codacy grade](https://img.shields.io/codacy/grade/40eae50295114eabba6b12b7372bed81?&logo=codacy)](https://www.codacy.com/gh/mac-vz/macvz/dashboard?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=mac-vz/macvz&amp;utm_campaign=Badge_Grade)
[![GitHub](https://img.shields.io/github/license/mac-vz/macvz?color=brightgreen)](https://github.com/mac-vz/macvz/blob/main/LICENSE)

# MACVZ

This project is inspired by and a rewrite of lima-vm.

The major difference is macvz uses macOS new [Virtualization API](https://developer.apple.com/documentation/virtualization?language=objc) instead of QEMU for spinning up VM's.

# Requirements
- Higher or equal to macOS monterey (12.2)
- Golang

# Getting Started
## Installation via Homebrew
- Run `brew install mac-vz/tap/macvz` to install macvz

## Installation via source
- Run `make all` to compile and build binary
- Run `make install` to install the binary to /usr/local

## Using macvz as a alternate for Docker Desktop
To start a Docker VM, run the following command
```
macvz start https://raw.githubusercontent.com/mac-vz/macvz/main/examples/docker.yaml
```

Execute the following command in macOS host to update docker.sock location
```
export DOCKER_HOST=unix://${HOME}/.macvz/docker/sock/docker.sock
```

That's it !! 


## Other macvz commands

To get shell access to a running VM,
```
macvz shell docker
```

To stop a running VM,
```
macvz stop docker
```

# Features
- Ability to start, stop and shell access
- Filesystem mounting using virtfs (See the performance report below)
- Automatic Port forwarding
- Custom DNS Resolution (like host.docker.internal)

# Planned
- Support for commands like list, delete, pause, resume
- Support for different linux distros

# Performance Summary

## Summary of filesystem performance with colima

The following table contains result summary of some different workloads tested against macvz and colima

### Summary for IOPS (Input Ouput Per Second)
| Workload            | Summary                            | macvz   | colima |
|---------------------|------------------------------------|---------|--------|
| Sequential Reads    | macvz handles 8x higher operations | 620K    | 77K    |
| Random Reads        | macvz handles 3x higher operations | 82K     | 25K    |
| Random Reads/Writes | macvz handles 3x higher operations | 37K/12K | 14K/4K |
| Sequential writes   | macvz performs almost equally      | 37K     | 38K    |
| Random writes       | macvz performs almost equally      | 22K     | 30K    |

### Summary for Bandwidth (Maximum amount of data transmitted)
| Workload            | Summary                       | macvz      | colima    |
|---------------------|-------------------------------|------------|-----------|
| Sequential Reads    | macvz handles 8x more data    | 2500MB     | 306MB     |
| Random Reads        | macvz handles 3x more data    | 320MB      | 98MB      |
| Random Reads/Writes | macvz handles 3x more data    | 140MB/50MB | 60MB/20MB |
| Sequential writes   | macvz performs almost equally | 145MB      | 150MB     |
| Random writes       | macvz performs almost equally | 90MB       | 110MB     |

Check out Wiki page [Why use virtualization framework](https://github.com/mac-vz/macvz/wiki/Why-use-macOS-virtualization-framework-%3F) for detailed information

# Project Status
⚠️ The project is still in early stage development and may introduce breaking changes.

# Supporters

[<img src="https://uploads-ssl.webflow.com/5ac3c046c82724970fc60918/5c019d917bba312af7553b49_MacStadium-developerlogo.png" style="max-height: 150px;width: 150px"/>](https://macstadium.com)
