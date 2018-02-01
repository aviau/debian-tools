output:
	mkdir output

.PHONY: build
build:
	docker pull debian:stretch
	docker build \
	--build-arg userid=$$(id -u) \
	--build-arg username=$$(id -u --name) \
	-t stretch-backports \
	.

# GPG: On the host, run `gpgconf --list-dirs | grep agent-socket` to find out
# where sockets are placed. Then run it in the container and mount the socket
# at the right place.
.PHONY: run
run: build output
	gpg-agent
	docker run -it \
		--rm \
		--privileged \
		-v $$(pwd)/output:/home/aviau/output \
		-v /run/user/$$( id -u)/gnupg/S.gpg-agent.ssh:/run/user/$$( id -u)/gnupg/S.gpg-agent.ssh \
		-v ~/.bash_history:/home/aviau/.bash_history \
		-v ~/.ssh/config:/home/aviau/.ssh/config:ro \
		-v ~/.ssh/known_hosts:/home/aviau/.ssh/known_hosts \
		-v ~/.gitconfig:/home/aviau/.gitconfig:ro \
		-v ~/.vimrc:/home/aviau/.vimrc:ro \
		-v ~/.vim:/home/aviau/.vim:ro \
		-v ~/.gbp.conf:/home/aviau/.gbp.conf:ro \
		-v ~/bin:/home/aviau/bin:ro \
		-v ~/.gnupg:/home/aviau/.gnupg \
		-v /run/user/$$( id -u)/gnupg/S.gpg-agent:/home/aviau/.gnupg/S.gpg-agent \
		-v ~/.bashrc:/home/aviau/.bashrc:ro \
		-v ~/.quiltrc-dpkg:/home/aviau/.quiltrc-dpkg:ro \
		-e SSH_AUTH_SOCK=/tmp/ssh_auth_sock \
		stretch-backports \
		bash
