FROM mariadb:11.6.2
ENV TZ UTC
ENV LC_ALL en_US.UTF-8

RUN apt update \
    && apt install -y language-pack-en pigz unzip pv nano \
    && rm -rf /var/lib/apt/lists/*
