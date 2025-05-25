FROM dorowu/ubuntu-desktop-lxde-vnc

RUN rm -f /etc/apt/sources.list.d/google-chrome.list
RUN apt-get update && \
    apt-get install -y openjdk-17-jdk wget unzip git qemu-kvm libvirt-daemon-system libvirt-clients bridge-utils libgl1-mesa-glx && \
    apt-get clean

# Instala Android Studio
RUN wget -O /tmp/android-studio.tar.gz https://redirector.gvt1.com/edgedl/android/studio/ide-zips/2022.3.1.21/android-studio-2022.3.1.21-linux.tar.gz && \
    tar -xzf /tmp/android-studio.tar.gz -C /opt && \
    rm /tmp/android-studio.tar.gz && \
    ln -s /opt/android-studio/bin/studio.sh /usr/local/bin/android-studio

# Instala Android SDK Command Line Tools
ENV ANDROID_SDK_ROOT /opt/android-sdk
RUN mkdir -p $ANDROID_SDK_ROOT/cmdline-tools && \
    wget -O /tmp/commandlinetools.zip "https://dl.google.com/android/repository/commandlinetools-linux-11076708_latest.zip" && \
    unzip /tmp/commandlinetools.zip -d $ANDROID_SDK_ROOT/cmdline-tools && \
    mv $ANDROID_SDK_ROOT/cmdline-tools/cmdline-tools $ANDROID_SDK_ROOT/cmdline-tools/latest && \
    rm /tmp/commandlinetools.zip

# Añade herramientas CLI al PATH
ENV PATH $PATH:$ANDROID_SDK_ROOT/cmdline-tools/latest/bin:$ANDROID_SDK_ROOT/platform-tools

# Instala plataformas y emulador
RUN yes | sdkmanager --licenses && \
    sdkmanager "platform-tools" "platforms;android-34" "emulator" "system-images;android-34;google_apis;x86_64"

# Crea un AVD (emulador)
RUN echo "no" | avdmanager create avd -n test_avd -k "system-images;android-34;google_apis;x86_64" --device "pixel"

# Expone puertos: 5901 (VNC), 6080 (web VNC), 5554/5555 (emulador), 5037 (ADB)
EXPOSE 5901 6080 5554 5555 5037

# El entrypoint y el entorno de escritorio ya están configurados por la imagen base