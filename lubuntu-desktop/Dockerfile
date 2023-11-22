FROM --platform=linux/amd64 arm64v8/ubuntu:20.04

RUN apt update && DEBIAN_FRONTEND=noninteractive apt install -y lubuntu-desktop

RUN apt-get update && apt-get install -y wget gnupg
RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add -
RUN echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" > /etc/apt/sources.list.d/google-chrome.list
RUN apt install firefox

RUN rm /run/reboot-required*

RUN useradd -m kmnviz -p $(openssl passwd testing)
RUN usermod -aG sudo kmnviz

RUN apt install -y xrdp
RUN adduser xrdp ssl-cert

RUN sed -i '3 a echo "\
export GNOME_SHELL_SESSION_MODE=lubuntu\\n\
export XDG_SESSION_TYPE=x11\\n\
export XDG_CURRENT_DESKTOP=LXQt\\n\
export XDG_CONFIG_DIRS=/etc/xdg/xdg-Lubuntu:/etc/xdg\\n\
" > ~/.xsessionrc' /etc/xrdp/startwm.sh

EXPOSE 3389

CMD service xrdp start ; bash 