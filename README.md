# rails-pq
Dockerfile for rails 5.1.3 with alpine environment and postgresql headers

## Usage example:

```Dockerfile
FROM seendex/rails-pq

LABEL maintainer="a.maslov@seendex.ru"

ENV RAILS_ENV production
ENV RACK_ENV production
ENV RAILS_LOG_TO_STDOUT 1

RUN mkdir -p /app
WORKDIR /app

COPY Gemfile Gemfile.lock ./
RUN bundle install --jobs 20 --retry 5

COPY . ./
RUN bundle exec rake assets:precompile --trace

CMD bundle exec puma -C config/puma.rb
```
