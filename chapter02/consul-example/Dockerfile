FROM alpine:latest
LABEL maintainer="Russ McKendrick <russ@mckendrick.io>"
LABEL description="An image with the latest version on Consul."

ENV CONSUL_VERSION 1.2.2
ENV CONSUL_SHA256 7fa3b287b22b58283b8bd5479291161af2badbc945709eb5412840d91b912060

RUN  apk add --update ca-certificates wget && \
     wget -O consul.zip https://releases.hashicorp.com/consul/${CONSUL_VERSION}/consul_${CONSUL_VERSION}_linux_amd64.zip && \
     echo "$CONSUL_SHA256 *consul.zip" | sha256sum -c - && \
     unzip consul.zip && \
     mv consul /bin/ && \
     rm -rf consul.zip && \
     rm -rf /tmp/* /var/cache/apk/*

EXPOSE 8300 8301 8301/udp 8302 8302/udp 8400 8500 8600 8600/udp

VOLUME [ "/data" ]

ENTRYPOINT [ "/bin/consul" ]
CMD [ "agent", "-data-dir", "/data", "-server", "-bootstrap-expect", "1", "-client=0.0.0.0"]