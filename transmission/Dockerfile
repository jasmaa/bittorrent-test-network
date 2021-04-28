FROM ubuntu:latest

WORKDIR /usr/src/app

RUN apt-get update
RUN apt-get install transmission-cli iputils-ping -y

COPY . .