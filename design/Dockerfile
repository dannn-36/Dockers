FROM dorowu/ubuntu-desktop-lxde-vnc

# Instala GIMP e Inkscape
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 32EE5355A6BC6E42 || true
RUN apt-get update && \
    apt-get install -y gimp inkscape && \
    apt-get clean

# Expone puertos para VNC y acceso web VNC
EXPOSE 5901 6080

# El usuario podrá acceder al entorno gráfico LXDE y usar GIMP/Inkscape vía VNC en el navegador (puerto 6080)