FROM ruby:2.6.3
RUN apt-get update -qq && \
    apt-get install -y build-essential \ 
                       libpq-dev \        
                       nodejs           

RUN mkdir /app
WORKDIR /app
ENV RAILS_ENV production
COPY Gemfile /app/Gemfile
COPY Gemfile.lock /app/Gemfile.lock

RUN gem install bundler
RUN bundle install
ADD . /app
EXPOSE 3000

CMD ["/bin/sh", "-c", "bundle exec rails db:create && bundle exec unicorn -p 3000 -c /app/config/unicorn.rb -E production"]
