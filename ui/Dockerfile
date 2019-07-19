FROM ubuntu:16.04
RUN apt-get update \
    && apt-get install -y ruby-full ruby-dev build-essential \
    && gem install bundler --no-ri --no-rdoc

ENV APP_HOME /app
RUN mkdir $APP_HOME
WORKDIR $APP_HOME
ADD Gemfile* $APP_HOME/
RUN bundle install && bundle clean
ADD . $APP_HOME
ENV POST_SERVICE_HOST post_host
ENV POST_SERVICE_PORT 5000
ENV COMMENT_SERVICE_HOST comment_host
ENV COMMENT_SERVICE_PORT 9292
CMD ["puma"]
