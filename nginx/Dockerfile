FROM nginx:1.23.3

RUN apt-get update \
    && apt-get -y install \
    vim wget procps

RUN groupadd -r -g 82 www \
    && useradd --system -u 82 -g www www

COPY nginx.conf /etc/nginx/

EXPOSE 80 443