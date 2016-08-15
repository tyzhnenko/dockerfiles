FROM centos:7

ENV shellcheckVersion 0.4.3
ENV shellcheckTag v$shellcheckVersion

RUN yum -y install epel-release && \
    yum -y update && \
    yum install --setopt=tsflags=nodocs \
      --nogpgcheck \
      --assumeyes \
      --quiet \
      cabal-install tar && \
    yum clean all && \
    rm -rf /var/cache/yum

RUN cabal update && \
    cabal install cabal-install && \
    cabal install cabal

RUN cabal update \
    && curl -Lso /tmp/shellcheck-$shellcheckTag.tar.gz https://github.com/koalaman/shellcheck/archive/$shellcheckTag.tar.gz \
    && tar zxf /tmp/shellcheck-$shellcheckTag.tar.gz -C /tmp/ \
    && rm /tmp/shellcheck-$shellcheckTag.tar.gz \
    && cabal install /tmp/shellcheck-$shellcheckVersion

RUN ln -s ~/.cabal/bin/shellcheck /usr/local/bin/
