FROM ubuntu:22.04


# Update the package list, install sudo, create a non-root user, and grant password-less sudo permissions
RUN apt-get update && apt upgrade -y && apt-get install -y --no-install-recommends \
    ca-certificates \
    wget \
    cmake \
    ninja-build \
    libglib2.0-0 -y 
    # && rm -rf /var/lib/apt/lists/*

# Set the working directory
WORKDIR /home/temp

# # Copy files into the container and set the appropriate permissions
COPY src/st-stm32cubeclt_1.16.0_21983_20240628_1741_amd64.deb_bundle.sh ./

# install STM32CubeCLT
RUN LICENSE_ALREADY_ACCEPTED=1 ./st-stm32cubeclt_1.16.0_21983_20240628_1741_amd64.deb_bundle.sh

ENV PATH="$PATH:/opt/st/stm32cubeclt_1.16.0/GNU-tools-for-STM32/bin" 
ENV PATH="$PATH:/opt/st/stm32cubeclt_1.16.0/STM32CubeProgrammer/bin"
ENV PATH="$PATH:/opt/st/stm32cubeclt_1.16.0/STMicroelectronics_CMSIS_SVD"
ENV PATH="$PATH:/opt/st/stm32cubeclt_1.16.0/STM32target-mcu"
ENV PATH="$PATH:/opt/st/stm32cubeclt_1.16.0/STLink-gdb-server/bin"
RUN cd .. && rm -rf temp

# #install Actions Runner
WORKDIR /home/actions-runner/app
# Download the latest runner package
RUN wget -qO actions-runner-linux-x64-2.319.0.tar.gz -L https://github.com/actions/runner/releases/download/v2.319.0/actions-runner-linux-x64-2.319.0.tar.gz
RUN apt update && apt install libdigest-sha-perl -y
# Optional: Validate the hash
CMD echo "52b8f9c5abb1a47cc506185a1a20ecea19daf0d94bbf4ddde7e617e7be109b14  actions-runner-linux-x64-2.319.0.tar.gz" | shasum -a 256 -c
# Extract the installer
RUN tar xzf ./actions-runner-linux-x64-2.319.0.tar.gz

RUN useradd actions-runner && \
    echo 'actions-runner ALL=(ALL) NOPASSWD: ALL' >> /etc/sudoers
USER actions-runner   
# RUN ./config.sh --url https://github.com/niwciu/PUSHBUTTON_SWITCH_LIB --token ANWL2FRVILIRV4RBQN6325DGW2XY2




# Set the non-root user as the default user
# USER actions-runner

# #
# # cleanup
# #

# # uninstall wget
# # RUN DEBIAN_FRONTEND='noninteractive' sudo apt-get remove wget -y
# # delete src files
# RUN sudo rm -r /home/actions-runner/app/src/*
# RUN sudo rm -r /home/actions-runner/app/src
# RUN sudo rm -r /home/actions-runner/app/actions-runner-linux-x64-2.309.0.tar.gz

# RUN rm -rf /var/lib/apt/lists/*

# -----------------------------------------------------
#
# ./config.sh --url https://github.com/niwciu/IMPLIKO_TYP_D --token ANWL2FQHGMDNUGKQKUOVAPDFCPMHU
# ./run.sh

# ./config.sh remove --token ANWL2FQHGMDNUGKQKUOVAPDFCPMHU ./config.sh remove --token ANWL2FQHGMDNUGKQKUOVAPDFCPMHU


