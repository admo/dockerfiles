FROM ubuntu:latest

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
		make \
		unzip \
	&& curl --silent --fail --show-error --location https://github.com/luarocks/luarocks/archive/2.4.3.tar.gz -o luarocks-2.4.3.tar.gz \
	&& tar xzf luarocks-2.4.3.tar.gz \
	&& cd luarocks-2.4.3 \
	&& ./configure \
	&& make install \
	&& cd - \
	&& rm -rf luarocks-2.4.3.tar.gz luarocks-2.4.3/ \
	&& update-alternatives --install "/usr/bin/lua" "lua-interpreter" "/usr/bin/lua5.3" 100 \
	&& update-alternatives --set lua-interpreter /usr/bin/lua5.3 \
        && apt --assume-yes autoremove \
	&& rm -rf /var/lib/apt/lists/*

RUN true \
	&& apt update \
	&& apt install --assume-yes --no-install-recommends \
		libexpat1-dev \
		ruby \
		ruby-dev \
	&& luarocks install luaexpat \
	&& luarocks install luafilesystem \
	&& luarocks install luajson \
	&& luarocks install luassert \
	&& gem install --no-ri --no-rdoc cucumber -v 1.3.20 \
	&& luarocks build --tree=/usr/local https://raw.github.com/admo/cucumber-lua/lua53/cucumber-lua-0.0-2.rockspec \
	&& apt --assume-yes --autoremove purge \
		libexpat1-dev \
		ruby-dev \
	&& apt --assume-yes clean \
	&& rm -rf /var/lib/apt/lists/*

RUN true \
	&& apt update \
	&& apt install --assume-yes --no-install-recommends \
		python3-minimal \
		python3-virtualenv \
	&& python3 -m virtualenv --python=python3 --no-wheel /workspace/.venv \
	&& . /workspace/.venv/bin/activate \
	&& pip install \
		behave \
		dicttoxml \
		flake8 \
		pyhamcrest \
	&& deactivate \
	&& apt --assume-yes --autoremove purge \
		python3-virtualenv \
	&& apt --assume-yes clean \
	&& rm -rf /var/lib/apt/lists/*

RUN true \
	&& echo LC_ALL=en_US.UTF-8 >> /etc/environment \
	&& echo LANG=en_US.UTF-8 >> /etc/environment

