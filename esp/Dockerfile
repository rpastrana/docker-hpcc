FROM hpccsystems/hpcc-base:7-xenial

RUN apt-get update && apt-get install -y iputils-ping curl xterm
RUN groupadd hpcc && useradd -s /bin/bash -r -m -d /home/hpcc -g hpcc -c "hpcc Runtime User" hpcc

ENV VERSION 7.0.18
ENV FULL_VERSION 7.0.18-1
#ENV PLATFORM_DOWNLOAD_MD5  ef58e94dcc66a45cb0fc8202e68b50d9
ENV PLATFORM_PACKAGE hpccsystems-platform-community_${FULL_VERSION}xenial_amd64.deb

RUN set -x \
   &&  wget  "http://wpc.423a.rhocdn.net/00423A/releases/CE-Candidate-${VERSION}/bin/platform/${PLATFORM_PACKAGE}" \
   #&& echo "$PLATFORM_DOWNLOAD_MD5 ${PLATFORM_PACKAGE}" | md5sum -c - \
   && dpkg -i "${PLATFORM_PACKAGE}" \
   && rm -rf "${PLATFORM_PACKAGE}"

EXPOSE 8010

#RUN cp -r /home/hpcc/.ssh ~/

COPY docker-entrypoint.sh /
COPY base-esp.xml /
ENTRYPOINT ["/docker-entrypoint.sh"]

#CMD ["/usr/sbin/sshd", "-D"]
#WORKDIR "/var/lib/HPCCSystems/myesp"
#CMD ["/opt/HPCCSystems/bin/init_dali"]
#CMD ["/opt/HPCCSystems/bin/esp"]
