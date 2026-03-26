FROM golang:1.23.4-alpine AS builder
WORKDIR /app
COPY . .
RUN go build -o emailservice

FROM alpine:latest
WORKDIR /app
COPY --from=builder /app/emailservice .

EXPOSE 8080
CMD ["./emailservice"]