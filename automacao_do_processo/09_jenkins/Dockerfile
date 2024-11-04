FROM jenkins/jenkins:2.452.2-jdk17

USER root

# Atualizar pacotes e instalar dependências
RUN apt-get update && \
    apt-get install -y \
    lsb-release \
    python3.11-venv \
    python3-pip \
    wget \
    xdg-utils \
    libxkbcommon-x11-0 \
    libxdamage1 \
    libvulkan1 \
    libpangocairo-1.0-0 \
    libnss3-dev \
    libasound2 \
    libatk1.0-0 \
    libglib2.0-dev \
    fonts-liberation \
    libatspi2.0-0 \
    libatk-bridge2.0-0 \
    libcups2 \
    libgtk-3-dev \
    libgtk-4-1 && \
    echo "deb http://deb.debian.org/debian bookworm-backports main contrib non-free" >> /etc/apt/sources.list && \
    apt-get update && \
    wget http://archive.ubuntu.com/ubuntu/pool/main/libu/libu2f-host/libu2f-udev_1.1.4-1_all.deb && \
    dpkg -i libu2f-udev_1.1.4-1_all.deb && \
    wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb && \
    dpkg -i google-chrome-stable_current_amd64.deb && \
    rm libu2f-udev_1.1.4-1_all.deb google-chrome-stable_current_amd64.deb && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

# Copiar conteúdo de _data para /var/jenkins_home no container
COPY _data/ /var/jenkins_home/

# Ajustar permissões no diretório do Jenkins
RUN chown -R jenkins:jenkins /var/jenkins_home && \
    chmod -R 775 /var/jenkins_home

# Certifique-se de que o diretório do projeto está acessível
RUN mkdir -p /var/jenkins_home/workspace/demo-pipeline && \
    chown -R jenkins:jenkins /var/jenkins_home/workspace/demo-pipeline

# Voltar para o usuário Jenkins
USER jenkins
