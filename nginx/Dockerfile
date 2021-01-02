FROM nginx:1.19.0-alpine

ARG prometheus_hostname
ARG prometheus_ip
ARG prometheus_port

ARG grafana_hostname
ARG grafana_ip
ARG grafana_port

ENV PROMETHEUS_HOSTNAME=$prometheus_hostname
ENV PROMETHEUS_IP=$prometheus_ip
ENV PROMETHEUS_PORT=$prometheus_port

ENV GRAFANA_HOSTNAME=$grafana_hostname
ENV GRAFANA_IP=$grafana_ip
ENV GRAFANA_PORT=$grafana_port

COPY ./certs/fullchain.pem /etc/ssl/fullchain.pem
COPY ./certs/privkey.pem /etc/ssl/privkey.pem

RUN chmod 600 /etc/ssl/*.pem
RUN chown root:root /etc/ssl/*.pem

COPY ./nginx/nginx.conf /tmp/docker.nginx
RUN envsubst '$GRAFANA_HOSTNAME $GRAFANA_IP $GRAFANA_PORT $PROMETHEUS_HOSTNAME $PROMETHEUS_IP $PROMETHEUS_PORT' < /tmp/docker.nginx > /etc/nginx/nginx.conf

CMD [ "nginx", "-g", "daemon off;" ]s
