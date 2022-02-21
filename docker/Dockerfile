FROM golang:1.16-alpine as builder
WORKDIR /app/
COPY go.mod go.sum ./
RUN go mod download
COPY . .
RUN apk add --no-cache build-base pkgconfig vips-dev
RUN go build -v

FROM alpine:3.14
EXPOSE 8080
RUN apk add --no-cache ca-certificates curl vips && update-ca-certificates
COPY --from=builder /app/imgproxy /usr/local/bin/imgproxy

CMD ["imgproxy"]
