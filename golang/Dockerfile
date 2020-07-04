FROM golang:1.14 AS build
RUN apt-get update && apt-get install unzip
WORKDIR /go/src/github.com/marjamis/<project>/
COPY go.* ./
RUN go mod download
COPY *.go ./
COPY ./cmd/ ./cmd/
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o entrypoint .

FROM alpine:3.10.3
LABEL maintainer=marjamis
RUN apk --no-cache add ca-certificates
# USER nobody
WORKDIR /app/
COPY --from=build /go/src/github.com/marjamis/<project>/entrypoint .
ENTRYPOINT ["./entrypoint"]
