output:
	mkdir output

.PHONY: build
build:
	docker pull debian:unstable
	docker build \
	--build-arg userid=$$(id -u) \
	--build-arg username=$$(id -u --name) \
	-t debian-tools-unstable \
	.

.PHONY: run
run: build output
	docker run -it \
		--rm \
		-v $$(pwd)/output:/home/aviau/output \
		-v /run/user/$$( id -u)/gnupg/S.gpg-agent.ssh:/run/user/$$( id -u)/gnupg/S.gpg-agent.ssh \
		-v ~/.bash_history:/home/aviau/.bash_history \
		-v ~/.ssh/config:/home/aviau/.ssh/config:ro \
		-v ~/.ssh/known_hosts:/home/aviau/.ssh/known_hosts \
		-v ~/.gitconfig:/home/aviau/.gitconfig:ro \
		-v ~/.vimrc:/home/aviau/.vimrc:ro \
		-v ~/.vim:/home/aviau/.vim:ro \
		-v ~/.gbp.conf:/home/aviau/.gbp.conf:ro \
		-v ~/.gnupg:/home/aviau/.gnupg \
		-v ~/.bashrc:/home/aviau/.bashrc:ro \
		-v ~/.quiltrc-dpkg:/home/aviau/.quiltrc-dpkg:ro \
		-e SSH_AUTH_SOCK=/tmp/ssh_auth_sock \
		debian-tools-unstable \
		bash
