FROM ubuntu:16.04

RUN true \
	&& apt update \
	&& apt upgrade --assume-yes \
	&& apt install --assume-yes \
		ca-certificates \
		curl \
		gawk \
		wget \
		git-core \
		diffstat \
		unzip \
		texinfo \
		gcc-multilib \
     		build-essential \
		chrpath \
		socat \
		python-minimal \
		libpython2.7-stdlib \
		cpio \
		openssh-client \
		sudo \
#	&& apt autoremove --asume-yes  \
	&& rm --recursive --force /var/lib/apt/lists/*

RUN true \
	&& useradd --create-home --shell /bin/bash localuser \
	&& usermod --append --groups sudo localuser \
	&& echo 'localuser:localuser' | chpasswd

RUN true \
	&& echo export DL_DIR="/workspace/yocto-packages" >> /etc/profile.d/eb-environment.sh \
	&& echo export CACHE="/workspace/.cache_rcar-3" >> /etc/profile.d/eb-environment.sh \
	&& echo export SSTATE_MIRROR_DIR="/mnt/b10107/ICAS1_linux_build_ci/cache_rcar-3/sstate-cache" >> /etc/profile.d/eb-environment.sh \
	&& chmod +x /etc/profile.d/eb-environment.sh

WORKDIR /workspace/.repo/manifests
USER localuser
#ENTRYPOINT -l
CMD ["/bin/bash", "--login"]
