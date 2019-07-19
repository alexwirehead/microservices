FROM ubuntu:16.04

RUN apt-get update && \
    apt-get install -y mongodb-server ruby-full ruby-dev build-essential git && \
    gem install bundler && \
    git clone https://github.com/alexwirehead/reddit.git
COPY mongod.conf /etc/mongod.conf
COPY db_config /app/db_config
COPY start.sh /start.sh

RUN cd /reddit && bundle install && \
    mkdir -p /data/db && \
    chmod 0777 /start.sh
CMD ["/start.sh"]