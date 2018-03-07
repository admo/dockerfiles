FROM ubuntu:17.10

RUN true \
	&& apt update \
	&& apt upgrade --assume-yes \
	&& apt install --assume-yes \
		# development
		build-essential \
		cmake \
		git \
		git-lfs \
		subversion \
		vim \
		# X application support
		libfreetype6 \
		libxext6 \
		libxi6 \
		libxrender1 \
		libxtst6 \
		# Docker in Docker support
		lxc \
		iptables \
		# Miscellaneous
		apt-transport-https \
		apt-utils \
		bash-completion \
		bsdtar \
		ca-certificates \
		language-pack-en \
		man-db \
		openssh-server \
		python-minimal \
		sudo \
		tmux \
		xauth \
	&& apt clean \
	&& rm -rf /var/lib/apt/lists/*

RUN true \
	&& sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd \
	&& mkdir /var/run/sshd \
	&& echo "AddressFamily inet" >> /etc/ssh/sshd_config \
	&& echo LC_ALL=en_US.UTF-8 >> /etc/environment \
	&& echo LANG=en_US.UTF-8 >> /etc/environment

RUN true \
	&& mkdir /opt/clion \
	&& wget --no-verbose --output-document=- https://download.jetbrains.com/cpp/CLion-2017.3.1.tar.gz | tar --strip-components=1 --extract --gzip --file - --directory=/opt/clion

# Install Docker from Docker Inc. repositories.
RUN wget --no-verbose --output-document=- https://get.docker.com/ | sh

RUN true \
	&& wget --no-verbose --output-document=/usr/local/bin/repo https://storage.googleapis.com/git-repo-downloads/repo \
	&& chmod a+x /usr/local/bin/repo \
	&& wget --no-verbose --output-document=- https://github.com/ninja-build/ninja/releases/download/v1.8.2/ninja-linux.zip | bsdtar --extract --file - --directory=/usr/local/bin \
	&& chmod a+x /usr/local/bin/ninja

RUN true \
	&& useradd --create-home --shell /bin/bash localuser \
	&& usermod --append --groups sudo,docker localuser \
	&& echo 'localuser:localuser' | chpasswd

VOLUME /var/lib/docker

CMD ["/usr/sbin/sshd", "-D"]