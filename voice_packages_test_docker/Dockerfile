FROM ubuntu:artful

RUN true \
	&& apt update \
	&& apt install --assume-yes --no-install-recommends \
		ca-certificates \
		curl \
		gcc \
		git \
		language-pack-en \
		liblua5.3-dev \
		lua5.3 \
		luarocks \
		make \
		unzip \
	&& update-alternatives --install "/usr/bin/lua" "lua-interpreter" "/usr/bin/lua5.3" 100 \
	&& update-alternatives --set lua-interpreter /usr/bin/lua5.3 \
    && apt --assume-yes autoremove \
	&& rm -rf /var/lib/apt/lists/*

RUN true \
	&& apt update \
	&& apt install --assume-yes --no-install-recommends \
		ruby \
		cucumber \
		lua-expat \
		lua-filesystem \
		lua-json \
		lua-luassert \
		lua-socket \
		lua-socket-dev \
	&& luarocks build --tree=/usr https://raw.github.com/admo/cucumber-lua/lua53/cucumber-lua-0.0-2.rockspec \
	&& apt --assume-yes --autoremove purge \
		libexpat1-dev \
		lua-socket-dev \
	&& apt --assume-yes clean \
	&& rm -rf /var/lib/apt/lists/*

RUN true \
	&& apt update \
	&& apt install --assume-yes --no-install-recommends \
		python3-minimal \
		python3-behave \
		python3-dicttoxml \
		python3-flake8 \
		python3-hamcrest \
	&& apt --assume-yes --autoremove purge \
		python3-virtualenv \
	&& apt --assume-yes clean \
	&& rm -rf /var/lib/apt/lists/*

RUN true \
	&& echo export LC_ALL=en_US.UTF-8 >> /etc/environment \
	&& echo export LANG=en_US.UTF-8 >> /etc/environment

RUN true \
	&& useradd --create-home --shell /bin/bash localuser \
	&& usermod --append --groups sudo localuser \
	&& echo 'localuser:localuser' | chpasswd

USER localuser
CMD ["/bin/bash"]

