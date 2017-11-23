FROM ubuntu:latest as fetcher
RUN \
	useradd --create-home user \
	&& apt update \
	&& apt upgrade --assume-yes \
	&& apt install --assume-yes \
		curl \
		gcc \
		git \
		make \
		software-properties-common \
	&& add-apt-repository --yes ppa:ubuntu-toolchain-r/test \
	&& curl -sL https://deb.nodesource.com/setup_8.x | bash - \
	&& apt install --assume-yes --no-install-recommends \
		nodejs
USER user
WORKDIR /home/user
RUN \
	git clone https://github.com/mattgodbolt/compiler-explorer.git \
	&& cd compiler-explorer \
	&& make prereqs

FROM ubuntu:latest
COPY --from=fetcher /home/user/compiler-explorer /home/user/compiler-explorer
COPY --from=fetcher /etc/apt /etc/apt
RUN \
	sed -i 's/https/http/' /etc/apt/sources.list.d/nodesource.list \
	&& apt update \
	&& apt install --assume-yes --no-install-recommends \
		git \
		g++-4.4 \
		g++-4.6 \
		g++-5 \
		g++-6 \
		g++-7 \
		make \
		nodejs \
	&& apt clean \
	&& rm -rf /var/lib/apt/lists/*
RUN \
	useradd --create-home user
ENV EXTRA_ARGS="--host 0.0.0.0"
EXPOSE 10240
USER user
WORKDIR /home/user/compiler-explorer
CMD ["make"]