FROM alpine:latest
RUN apk update && \
    apk upgrade && \
    apk add bash ruby ruby-io-console curl-dev ruby-dev build-base \
    && gem install bundler:1.14.6 --no-ri --no-rdoc

ENV APP_HOME /app
RUN mkdir $APP_HOME
WORKDIR $APP_HOME
ADD Gemfile* $APP_HOME/
RUN bundle install
ADD . $APP_HOME

ENV COMMENT_DATABASE_HOST comment_db_host
ENV COMMENT_DATABASE comments

CMD ["puma"]