FROM golang:1.12 as builder

ARG SSH_KEY

#RUN echo "$SSH_KEY"

# Authorize SSH Host
RUN mkdir -p /root/.ssh && \
    chmod 0700 /root/.ssh && \
    ssh-keyscan github.com > /root/.ssh/known_hosts

# go2xunit allows us to turn Go test results into xunit (aka JUnit) output
# We must run this before we configure git to replace all https urls with ssh urls.
RUN go get github.com/tebeka/go2xunit

# We need this key so that we can read our private IMQS git repos from github
RUN echo "$SSH_KEY" > /root/.ssh/id_rsa && \
    chmod 600 /root/.ssh/id_rsa

RUN git config --global url."git@github.com:".insteadOf "https://github.com/"

WORKDIR /test

# Cache dependencies
COPY go.mod go.sum ./
RUN go mod download

# Copy code in
COPY . .