FROM golang:1.22.2-alpine3.19 AS builder
ARG GIT_TAG
WORKDIR /app
COPY . .
RUN apk update && apk add --no-cache make bash git
ENV GIT_TAG=${GIT_TAG}
ENV GO111MODULE=on
ENV CGO_ENABLED=0
RUN make build

FROM alpine:3.19
WORKDIR /app
RUN apk update && apk add --no-cache bash
COPY --from=builder /app/bin/k3d-tools .
ENTRYPOINT [ "/app/k3d-tools"]

