# Use Fedora as the base image
FROM fedora:latest

# Update and install required dependencies
RUN dnf update -y && \
    dnf install -y \
    git vim make time awk date yes \
    util-linux findutils diffutils \
    gcc flex bison bc \ 
    ncurses-devel openssl-devel elfutils-libelf-devel \
    kernel-headers kernel-devel \
    perl perl-Data-Dumper patch tar gzip cpio \
    && dnf clean all

# Set the working directory
WORKDIR /kernbench

# Clone the Linux source code
RUN git clone --depth=1 https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git linux

RUN mv /kernbench/linux/tools/testing/selftests/devices/probe/boards/Dell\ Inc.,XPS\ 13\ 9findutils300.yaml /kernbench/linux/tools/testing/selftests/devices/probe/boards/Dell.yaml

# Clone the kernbench benchmark script
RUN git clone --depth=1 https://github.com/linux-test-project/ltp.git && \
    cp ltp/utils/benchmark/kernbench-0.42/kernbench linux/kernbench.sh

# Make the script executable
RUN chmod +x linux/kernbench.sh

# Default command: Run kernbench
CMD ["/bin/bash", "-c", "cd /kernbench/linux && ./kernbench.sh"]


# podman run -it --privileged -v /lib/modules:/lib/modules -v /usr/src/kernels:/usr/src/kernels kernbench:latest
# podman run -it --privileged -v /lib/modules:/lib/modules -v /usr/src/kernels:/usr/src/kernels kernbench:latest /bin/bash
