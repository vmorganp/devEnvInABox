# See here for image contents: https://github.com/microsoft/vscode-dev-containers/tree/v0.194.3/containers/ubuntu/.devcontainer/base.Dockerfile

# [Choice] Ubuntu version: hirsute, bionic, focal
ARG VARIANT="focal"
FROM mcr.microsoft.com/vscode/devcontainers/base:0-${VARIANT}

# [Optional] Uncomment this section to install additional OS packages.
# RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
#     && apt-get -y install --no-install-recommends <insert stuff you want> 

# RUN sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)" "" --unattended

# Terraform and Packer
ENV TERRAFORM_VERSION="0.15.1"
ENV PACKER_VERSION="1.7.2"

RUN wget "https://releases.hashicorp.com/terraform/${TERRAFORM_VERSION}/terraform_${TERRAFORM_VERSION}_linux_amd64.zip" -O /tmp/terraform.zip && unzip /tmp/terraform.zip -d /usr/bin && rm /tmp/terraform.zip
RUN wget "https://releases.hashicorp.com/packer/${PACKER_VERSION}/packer_${PACKER_VERSION}_linux_amd64.zip" -O /tmp/packer.zip && unzip /tmp/packer.zip -d /usr/bin && rm /tmp/packer.zip

# Awscli v2
RUN curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "/tmp/awscliv2.zip"
RUN unzip /tmp/awscliv2.zip -d /tmp/ \
  && ./tmp/aws/install \
  && rm -rf /tmp/awscliv2.zip /tmp/aws

# Install tfenv and configure env.
# user vscode
# RUN git clone https://github.com/tfutils/tfenv.git /tmp/tfenv \ 
#   && ln -s ~/.tfenv/bin/* /usr/local/bin
# "postCreateCommand": "mkdir ~/.tfenv && sudo mv /tmp/tfenv/* ~/.tfenv && sudo ln -s ~/.tfenv/bin/* /usr/local/bin"



USER vscode
RUN git clone https://github.com/tfutils/tfenv.git /home/vscode/.tfenv \ 
  && sudo ln -s /home/vscode/.tfenv/bin/* /usr/local/bin

RUN wget https://raw.githubusercontent.com/rupa/z/master/z.sh -O /home/vscode/z.sh
COPY .zshrc /home/vscode/

USER root
RUN apt-get update && apt-get upgrade -y