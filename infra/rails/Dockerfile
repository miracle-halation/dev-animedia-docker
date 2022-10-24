FROM ruby:3.0.2
ENV RAILS_ENV=production

## Railsの準備
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - \
    && echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list \
    && apt-get update -qq \
    && apt-get install -y nodejs yarn nginx vim\
		&& mkdir backend

WORKDIR /backend
COPY Gemfile Gemfile
COPY Gemfile.lock Gemfile.lock

RUN bundle install

COPY . /backend

## nginxの準備
RUN groupadd nginx
RUN useradd -g nginx nginx
COPY nginx.conf /etc/nginx/nginx.conf

## 起動準備
COPY deployentrypoint.sh /usr/bin/
RUN chmod +x /usr/bin/deployentrypoint.sh

ENTRYPOINT ["deployentrypoint.sh"]
EXPOSE 80
