FROM dorowu/ubuntu-desktop-lxde-vnc

RUN rm -f /etc/apt/sources.list.d/google-chrome.list
RUN apt-get update && \
    apt-get install -y gimp inkscape && \
    apt-get clean

# Expone puertos para VNC y acceso web VNC
EXPOSE 5901 6080

# El entrypoint y el entorno de escritorio ya están configurados por la imagen base