# Intro
Experimenting kind on ubuntu

## Run ubuntu ubuntu
docker run -dt --name ubuntu ubuntu:22.04
docker exec -it ubuntu /bin/bash

## Setup ubuntu
passwd
apt update
apt install sudo
apt install curl

## Create your favorite user
adduser raffaele
adduser raffaele sudo
su - raffaele

## export the container
docker export -o ubuntu_22-04.tar ubuntu

## import the container into wsl
wsl --import Ubuntu-22.04 ./ ubuntu_22-04.tar


## install Podman
sudo apt install podman
sudo chmod 4755 /usr/bin/newgidmap
sudo chmod 4755 /usr/bin/newuidmap
usermod --add-subuids 200000-201000 --add-subgids 200000-201000 raffaele
grep raffaele /etc/subuid /etc/subgid

## Install Kind
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.11.1/kind-linux-amd64
chmod +x ./kind
mv ./kind /usr/bin/kind

## Example
kind create cluster