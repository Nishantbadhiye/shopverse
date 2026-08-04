FROM golang:1.24-alpine AS builder

WORKDIR /app

COPY go.mod go.sum ./

RUN go mod download

COPY . .

RUN CGO_ENABLED=0 GOOS=linux go build -o shopverse-api ./cmd/main.go

FROM gcr.io/distroless/static-debian12

COPY --from=builder /app/shopverse-api /shopverse-api

EXPOSE 9091

USER nonroot:nonroot

ENTRYPOINT ["/shopverse-api"]

