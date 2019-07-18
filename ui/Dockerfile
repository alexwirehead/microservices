FROM ruby:2.5-alpine

ENV APP_HOME=/app \
    POST_SERVICE_HOST=post_host \
    POST_SERVICE_PORT=5000 \
    COMMENT_SERVICE_HOST=comment_host \
    COMMENT_SERVICE_PORT=9292

RUN apk update && \
    apk upgrade && \
    apk add ruby-dev build-base && \
    rm -rf /var/cache/apk/* && mkdir $APP_HOME

WORKDIR $APP_HOME
ADD Gemfile* $APP_HOME/
RUN bundle install && bundle clean
ADD . $APP_HOME
CMD ["puma"]