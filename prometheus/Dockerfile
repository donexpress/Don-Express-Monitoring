FROM alpine:3.10.2

RUN apk add gettext

ARG dc0_nginx_logs_port
ARG stg_nginx_logs_port
ARG prod_nginx_logs_port
ARG dc0_cluster_ip
ARG stg_cluster_ip
ARG prod_cluster_ip

ENV DC0_NGINX_LOGS_PORT=$dc0_nginx_logs_port
ENV STG_NGINX_LOGS_PORT=$stg_nginx_logs_port
ENV PROD_NGINX_LOGS_PORT=$prod_nginx_logs_port
ENV DC0_CLUSTER_IP=$dc0_cluster_ip
ENV STG_CLUSTER_IP=$stg_cluster_ip
ENV PROD_CLUSTER_IP=$prod_cluster_ip

COPY ./prometheus/prometheus.yml /tmp/prometheus-base.yml
RUN envsubst '$DC0_NGINX_LOGS_PORT $STG_NGINX_LOGS_PORT  $PROD_NGINX_LOGS_PORT  $DC0_CLUSTER_IP $STG_CLUSTER_IP $PROD_CLUSTER_IP' < /tmp/prometheus-base.yml > /tmp/prometheus.yml

FROM prom/prometheus:v2.17.1

COPY --from=0 /tmp/prometheus.yml /etc/prometheus/prometheus.yml
