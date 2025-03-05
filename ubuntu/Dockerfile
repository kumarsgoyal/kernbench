# Use Ubuntu as the base image
FROM ubuntu:latest

# Update and install required dependencies
RUN apt update -y && \
    apt install -y \
    git vim make time \
    coreutils findutils diffutils \
    gcc flex bison bc \
    libncurses-dev libssl-dev libelf-dev \
    linux-headers-generic \
    perl perl-modules patch tar gzip cpio \
    && apt clean

# Set the working directory
WORKDIR /kernbench

# Clone the Linux source code
RUN git clone --depth=1 https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git linux

# Fix YAML file issue (if it exists)
RUN mv /kernbench/linux/tools/testing/selftests/devices/probe/boards/Dell\ Inc.,XPS\ 13\ 9300.yaml /kernbench/linux/tools/testing/selftests/devices/probe/boards/Dell.yaml

# Clone the kernbench benchmark script
RUN git clone --depth=1 https://github.com/linux-test-project/ltp.git && \
    cp ltp/utils/benchmark/kernbench-0.42/kernbench linux/kernbench.sh

# Make the script executable
RUN chmod +x linux/kernbench.sh

# Default command: Run kernbench
CMD ["/bin/bash", "-c", "cd /kernbench/linux && ./kernbench.sh"]

