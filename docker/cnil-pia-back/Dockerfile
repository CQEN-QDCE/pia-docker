FROM ruby:2.6.5

ENV DEBIAN_FRONTEND noninteractive
ENV PIA_VERSION 2.2.0
ENV RAILS_ENV production
ENV RAILS_SERVE_STATIC_FILES=true

RUN apt-get update \
 && apt-get install --no-install-recommends -y \
    git \
    postgresql-client \
    postgresql \
    postgresql-contrib \
 && apt-get clean


RUN git clone --branch master https://github.com/CQEN-QDCE/pia-back.git --depth 1 /var/www/

COPY docker/cnil-pia-back/database.yml /var/www/config/database.yml
COPY docker/cnil-pia-back/application.yml /var/www/config/application.yml

WORKDIR /var/www/

RUN gem install bundler
RUN bundle update nokogiri mimemagic
RUN bundle install

COPY docker/cnil-pia-back/entrypoint /entrypoint
RUN chmod +x /entrypoint
ENTRYPOINT ["/entrypoint"]

CMD ["bin/rails", "server"]
