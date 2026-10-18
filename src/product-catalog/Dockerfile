FROM golang:1.27-alpine3.23 AS builder

WORKDIR /usr/src/app

COPY . .

RUN go mod download

RUN go build -o product-catalog . 

FROM alpine

WORKDIR /usr/src/app

COPY --from=builder /usr/src/app/product-catalog .

# the products are loaded from the product.json in product directory so copied the folder
COPY ./products ./products

ENV PRODUCT_CATALOG_PORT 8088

ENTRYPOINT ["./product-catalog"]
