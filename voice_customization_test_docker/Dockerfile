FROM ubuntu:xenial

RUN true \
	&& apt update --quiet \
	&& apt install --quiet --assume-yes --no-install-recommends \
		gcc \
		git \
		make \
		language-pack-en \
		lua5.1 \
		lua-filesystem \
		lua-xmlrpc \
		lua-sec \
		lua-expat \
		libarchive-extract-perl \
		libarchive-zip-perl \
		libc6-dev \
		libmodern-perl-perl \
		liblua5.1-0 \
		liblua5.1-0-dev \
		libxml-hash-lx-perl \
		libxml-libxml-perl \
		libxml-writer-perl \
		pkg-config \
		python3 \
		python3-hamcrest \
		python3-pip \
		python3-setuptools \
		python3-wheel \
		ruby \
		zip \
	&& pip3 install behave dicttoxml \
	&& cpan Path::Abstract JSON::Parse Lua::API \
	&& apt --quiet --assume-yes purge \
		gcc \
		libc6-dev \
		liblua5.1-0-dev \
		pkg-config \
		python3-pip \
		python3-setuptools \
		python3-wheel \
		make \
	&& apt --quiet --assume-yes autoremove \
	&& apt --quiet --assume-yes clean \
	&& rm --force --recursive /var/lib/apt/lists/* \
	&& rm --force --recursive /root/.cpan \
	&& ln --symbolic /usr/bin/python3 /usr/bin/python \
	&& echo "\nexport LANG=en_US.UTF-8\nexport TOOLS_REPOS_PATH=/workspace/voice_tools\n" >> /etc/profile

WORKDIR /workspace/sparta/mib3t/voice-customization
ENTRYPOINT ["/bin/sh", "-l", "-c"]
