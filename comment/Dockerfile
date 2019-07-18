FROM ruby:2.5-alpine
RUN apk update && \
    apk upgrade && \
    apk add ruby-dev build-base && \
    rm -rf /var/cache/apk/*

ENV APP_HOME /app
RUN mkdir $APP_HOME
WORKDIR $APP_HOME
ADD Gemfile* $APP_HOME/
RUN bundle install && bundle clean
ADD . $APP_HOME

ENV COMMENT_DATABASE_HOST comment_db_host
ENV COMMENT_DATABASE comments

CMD ["puma"]