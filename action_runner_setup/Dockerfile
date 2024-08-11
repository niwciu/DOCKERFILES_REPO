FROM ubuntu:latest

RUN echo 'deb http://security.ubuntu.com/ubuntu focal-security main' >> /etc/apt/sources.list.d/focal-security.list

RUN apt-get update && apt upgrade -y && apt-get install -y --no-install-recommends \
    ca-certificates \
    sudo \
    curl \
    wget \
    libdigest-sha-perl \
    libssl1.1

WORKDIR /home/actions-runner

RUN curl -o actions-runner-linux-x64-2.319.0.tar.gz -L https://github.com/actions/runner/releases/download/v2.319.0/actions-runner-linux-x64-2.319.0.tar.gz
# RUN apt update && apt install libdigest-sha-perl -y

RUN tar xzf ./actions-runner-linux-x64-2.319.0.tar.gz

# add user with no password - action runner required no root accout to run
RUN useradd actions-runner && \
    echo 'actions-runner ALL=(ALL) NOPASSWD: ALL' >> /etc/sudoers
USER actions-runner 

# add missing dependencies 
RUN sudo ./bin/installdependencies.sh



# RUN /bin/installdependencies.sh
# 



# #############################33333
#./config.sh --url https://github.com/niwciu/PUSHBUTTON_SWITCH_LIB --token ANWL2FXTTKV65DR7TNELADDGW5WTW