# Kernel Benchmarking with Kernbench

This repository provides Dockerfiles for running Kernbench inside a containerized environment. It supports both Fedora and Ubuntu distributions.

## What is Kernbench?
Kernbench is a CPU-intensive benchmark for measuring Linux kernel compilation performance under different load conditions.

## Supported Distributions
- **Fedora** (Latest)
- **Ubuntu** (Latest LTS)


## Getting Started

### Prerequisites
- Podman or Docker installed on your system.
- Kernel sources must be available on the host machine `/usr/src/kernels/`.


## Setup & Usage

### 1. Clone the Repository

git clone [kernbench](https://github.com/kumarsgoyal/kernbench.git)


### 2. Building the Podman or Docker Image

#### Fedora
```cd fedora```

```podman build -t kernbench-fedora . ```

OR 

``` docker build -t kernbench-fedora .```

#### Ubuntu
```cd ubuntu```

```podman build -t kernbench-ubuntu . ```

OR 

``` docker build -t kernbench-ubuntu .```


### 3. Running the Podman or Docker Image
#### Fedora

```podman run -it --privileged -v /lib/modules:/lib modules -v /usr/src:/usr/src kernbench-fedora:latest ``` 

OR

``` podman run -it --privileged -v /lib/modules:/lib/modules -v /usr/src:/usr/src kernbench-fedora:latest /bin/bash ```

#### Ubuntu

```podman run -it --privileged -v /lib/modules:/lib modules -v /usr/src:/usr/src kernbench-ubuntu:latest ``` 

OR

``` podman run -it --privileged -v /lib/modules:/lib/modules -v /usr/src:/usr/src kernbench-ubuntu:latest /bin/bash ```


### Expected Output
The benchmark will output performance metrics like:

- Elapsed Time
- CPU Utilization
- Context Switches
- System & User Time


## Contributions
Feel free to submit issues or pull requests if you encounter any problems or want to improve the setup.

## License
This project is licensed under the MIT License.
