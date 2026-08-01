FROM golang:1.24-alpine AS builder

WORKDIR /app

COPY go.mod go.sum ./

RUN go mod download

COPY . .

RUN ls -l

RUN ls -l go.mod go.sum
RUN grep "github.com/gofiber/fiber/v2" go.sum
RUN grep "golang.org/x/crypto" go.sum



RUN CGO_ENABLED=0 GOOS=linux go build -o shopverse-api ./cmd/main.go

FROM gcr.io/distroless/static-debian12

COPY --from=builder /app/shopverse-api /shopverse-api

EXPOSE 8080

USER nonroot:nonroot

ENTRYPOINT ["/shopverse-api"]

