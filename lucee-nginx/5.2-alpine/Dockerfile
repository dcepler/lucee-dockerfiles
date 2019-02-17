FROM dcepler/lucee52-alpine:latest

MAINTAINER David Epler <dcepler@dcepler.net>

# Install nginx and supervisord
RUN set -x && \
        apk add \
                nginx \
		supervisor

# Copy default nginx config files
COPY nginx.conf /etc/nginx/
COPY default.conf /etc/nginx/conf.d/

# Copy supervisord.conf
COPY supervisord.conf /etc/supervisor/conf.d/

# Provide test page
RUN mkdir -p /var/www
COPY index.cfm /var/www/
ONBUILD RUN rm -rf /var/www/*

# Expose HTTP and HTTPS ports
EXPOSE 80 443

# Engage
CMD ["supervisord", "-c", "/etc/supervisor/supervisord.conf"]
