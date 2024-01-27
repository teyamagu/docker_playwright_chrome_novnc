FROM mcr.microsoft.com/playwright:jammy

WORKDIR /app

# Dockerビルド時にタイムゾーン選択を求められるときがあるので事前に選択する
RUN ln -sf /usr/share/zoneinfo/Asia/Tokyo /etc/localtime

# chrome install
RUN curl -sSL https://dl.google.com/linux/linux_signing_key.pub | apt-key add -
RUN sh -c 'echo "deb http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google-chrome.list'
RUN apt-get -y update
RUN apt-get install -y google-chrome-stable dbus

# japanese font setting and install
ENV LANGUAGE ja_JP.UTF-8
ENV LANG ja_JP.UTF-8
RUN apt-get install -y --no-install-recommends locales && \
    locale-gen ja_JP.UTF-8 && \
    apt-get install -y --no-install-recommends fonts-ipafont

# playwright install and vnc setting
RUN apt-get update && apt-get -y install x11vnc websockify novnc
RUN npm update -g npm
RUN npm init -y
RUN npm install playwright-core

COPY docker-init.sh /

CMD [ "/docker-init.sh" ]
