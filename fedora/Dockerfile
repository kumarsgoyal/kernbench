# Use Fedora as the base image
FROM fedora:latest

# Update and install required dependencies
RUN dnf update -y && \
    dnf install -y \
    git vim make time awk date yes \
    gcc bc flex bison \
    ncurses-devel elfutils-libelf-devel \
    openssl-devel perl python3 dwarves \
    && dnf clean all
    
# Set the working directory
WORKDIR /kernbench

# Clone the Linux source code
RUN git clone --depth=1 https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git linux

# Clone the kernbench benchmark script
RUN git clone --depth=1 https://github.com/kumarsgoyal/ltp.git && \
    cp ltp/utils/benchmark/kernbench-0.42/kernbench linux/kernbench.sh

# Make the script executable
RUN chmod +x linux/kernbench.sh

# Default command: Run kernbench
CMD ["/bin/bash", "-c", "cd /kernbench/linux && ./kernbench.sh"]
