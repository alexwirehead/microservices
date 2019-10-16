FROM ubuntu:16.04
RUN apt-get update \
    && apt-get install -y ruby-full ruby-dev build-essential \
    && gem install bundler --no-ri --no-rdoc


ENV APP_HOME=/app \
    COMMENT_DATABASE_HOST=comment_db_host \
    COMMENT_DATABASE=comments
RUN mkdir $APP_HOME
WORKDIR $APP_HOME
ADD Gemfile* $APP_HOME/
RUN bundle install && bundle clean --force
ADD . $APP_HOME

CMD ["puma"]
