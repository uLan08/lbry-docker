FROM ubuntu:18.04

RUN groupadd --gid 1000 lbryio \
  && useradd --uid 1000 --gid lbryio --shell /bin/bash --create-home lbryio

RUN apt-get update && apt-get install -y curl unzip

ARG RELEASE
RUN VERSION=${RELEASE:-`curl --silent "https://api.github.com/repos/lbryio/lbrycrd/releases/latest" | grep '"tag_name"' | sed -E 's/.*"([^"]+)".*/\1/'`} \
  && $(cd /tmp && curl -SLO https://github.com/lbryio/lbrycrd/releases/download/${VERSION}/lbrycrd-linux.zip) \
  && mkdir -p /opt/lbrycrd \
  && unzip /tmp/lbrycrd-linux.zip -d /opt/lbrycrd \
  && ln -s /opt/lbrycrd/lbrycrd-cli /usr/local/bin/lbrycrd-cli \
  && ln -s /opt/lbrycrd/lbrycrd-tx /usr/local/bin/lbrycrd-tx \  
  && ln -s /opt/lbrycrd/lbrycrdd /usr/local/bin/lbrycrdd \
  && rm /tmp/lbrycrd-linux.zip
  
USER lbryio

CMD ["lbrycrdd", "-server"]
