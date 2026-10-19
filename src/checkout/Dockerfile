FROM golang:1.27-alpine3.23 AS builder

WORKDIR /usr/src/app

COPY . .

RUN go mod download

RUN go build -o ./checkout .

FROM alpine

WORKDIR /usr/src/app

COPY --from=builder /usr/src/app/checkout .

ENV CHECKOUT_PORT=8089

ENTRYPOINT ["./checkout"]
