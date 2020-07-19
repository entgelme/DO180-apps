FROM ubi7/ubi:7.7

MAINTAINER username <username@example.com>

ENV NEXUS_VERSION=2.14.3-02 \
    NEXUS_HOME=/opt/nexus

RUN yum install -y --setopt=tsflags=nodocs java-1.8.0-openjdk-devel && \
    yum clean all -y

RUN groupadd -r nexus -f -g 1001 && \
    useradd -u 1001 -r -g nexus -m -d /opt/nexus -s /sbin/nologin \
            -c "Nexus User" nexus && \
    chown -R nexus:nexus /opt/nexus && \
    chmod -R 755 /opt/nexus

USER nexus

ADD nexus-2.14.3-02-bundle.tar.gz /opt/nexus
ADD nexus-start.sh /opt/nexus/

RUN ln -s /opt/nexus/nexus-2.14.3-02 \
          /opt/nexus/nexus2

WORKDIR /opt/nexus

VOLUME ["/opt/nexus/sonatype-work"]

CMD ["sh", "nexus-start.sh"]

