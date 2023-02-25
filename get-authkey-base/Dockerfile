# Produces a container to be stored in
# https://github.com/tailscale/github-action/pkgs/container/get-authkey
FROM golang:1.20.1-bullseye as builder
WORKDIR /app
RUN git clone https://github.com/tailscale/tailscale.git && \
    cd tailscale && go get -d ./... && \
    ./tool/go build ./cmd/get-authkey

FROM debian:bullseye-slim
LABEL org.opencontainers.image.source="https://github.com/tailscale/github-action-get-authkey-base"
RUN apt update && apt install -y ca-certificates
COPY --from=builder /app/tailscale/get-authkey /get-authkey
