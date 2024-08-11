#############################################################################################################
# This docker image require to download, unzip STM32Cube_CLT and place the .sh script in src folder
#
# To build container:
#       docker build -t USER_NAME/CONTAINER_NAME:VERSION_NUMB -t USER_NAME/CONTAINER_NAME:latest .
#   example:
#       docker build -t niwciu/stm32cube_clt_container:1.0.0 -t niwciu/stm32cube_clt_container:latest .
# To push the container:
#       docker push USER_NAME/CONTAINER_NAME:VERSION_NUMB  
#       docker push USER_NAME/CONTAINER_NAME:latest
#   example:
#       docker push niwciu/stm32cube_clt_container:latest
#       docker push niwciu/stm32cube_clt_container:1.0.0
#
############################################################################################################

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

ARG VERSION=1.16.0
ARG BUILD=21983_20240628_1741
# # Copy files into the container and set the appropriate permissions
COPY src/st-stm32cubeclt_${VERSION}_${BUILD}_amd64.deb_bundle.sh ./

# install STM32CubeCLT
RUN LICENSE_ALREADY_ACCEPTED=1 ./st-stm32cubeclt_1.16.0_21983_20240628_1741_amd64.deb_bundle.sh

ENV PATH="$PATH:/opt/st/stm32cubeclt_1.16.0/GNU-tools-for-STM32/bin" 
ENV PATH="$PATH:/opt/st/stm32cubeclt_1.16.0/STM32CubeProgrammer/bin"
ENV PATH="$PATH:/opt/st/stm32cubeclt_1.16.0/STMicroelectronics_CMSIS_SVD"
ENV PATH="$PATH:/opt/st/stm32cubeclt_1.16.0/STM32target-mcu"
ENV PATH="$PATH:/opt/st/stm32cubeclt_1.16.0/STLink-gdb-server/bin"
RUN cd .. && rm -rf temp

RUN rm -rf /var/lib/apt/lists/*



