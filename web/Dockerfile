FROM dorowu/ubuntu-desktop-lxde-vnc

RUN rm -f /etc/apt/sources.list.d/google-chrome.list
RUN apt-get update && \
    apt-get install -y apache2 php php-mysql wget unzip && \
    apt-get clean

# Instala Eclipse PDT
RUN wget -O /tmp/eclipse.tar.gz "https://www.eclipse.org/downloads/download.php?file=/technology/epp/downloads/release/2024-03/R/eclipse-php-2024-03-R-linux-gtk-x86_64.tar.gz&r=1" && \
    tar -xzf /tmp/eclipse.tar.gz -C /opt && \
    rm /tmp/eclipse.tar.gz && \
    ln -s /opt/eclipse/eclipse /usr/local/bin/eclipse

# Configura Apache para servir desde /workspace
RUN rm -rf /var/www/html && ln -s /workspace /var/www/html

# Expone puertos: 80 (web), 5901 (VNC), 6080 (web VNC)
EXPOSE 80 5901 6080

# Crea el directorio de trabajo para el código
RUN mkdir -p /workspace
WORKDIR /workspace

# El entrypoint y el entorno de escritorio ya están configurados por la imagen base

RUN apt-get update && apt-get install -y phpmyadmin && apt-get clean