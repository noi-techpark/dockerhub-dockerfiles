FROM python:3.6

ENV SCANCODE_RELEASE=3.2.3
ENV SPDX_TOOLS_RELEASE=2.2.4
RUN apt-get update && apt-get install -y bzip2 xz-utils zlib1g libxml2-dev libxslt1-dev openjdk-11-jdk-headless

RUN pip install wheel gitpython fossology==0.2.0 spdx-tools==0.6.1 anybadge flanker
RUN wget -P /usr/local/lib https://github.com/spdx/tools/releases/download/v${SPDX_TOOLS_RELEASE}/spdx-tools-${SPDX_TOOLS_RELEASE}-jar-with-dependencies.jar

RUN wget https://github.com/nexB/scancode-toolkit/releases/download/v${SCANCODE_RELEASE}/scancode-toolkit-${SCANCODE_RELEASE}.tar.bz2
RUN mkdir scancode-toolkit && tar xjvf scancode-toolkit-*.tar.bz2 -C scancode-toolkit --strip-components=1

RUN python -c "from flanker.addresslib import address" >/dev/null 2>&1
WORKDIR scancode-toolkit
ENV PATH=$HOME/scancode-toolkit:$PATH
RUN scancode --reindex-licenses
