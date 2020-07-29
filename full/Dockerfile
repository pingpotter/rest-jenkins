# Build the Go Binary.
FROM golang:1.14.6 as builder

WORKDIR /service
COPY . .

RUN go test -v ./...

# Set the environment variables for the go command:
# * CGO_ENABLED=0 to build a statically-linked executable
ENV CGO_ENABLED=0 GOOS=linux
#BUILD APP
RUN go build -mod=vendor -a -o api main.go

# Run the Go Binary in Alpine.
FROM alpine:3.12
ARG BUILD_DATE
RUN apk --no-cache add ca-certificates

COPY --from=builder /service/api /app/api

WORKDIR /app
CMD ["/app/api"]

ENV PORT 8080

LABEL org.opencontainers.image.created="${BUILD_DATE}" \
    org.opencontainers.image.authors="Jiraphon Sa." \