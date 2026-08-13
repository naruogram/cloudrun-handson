FROM --platform=$BUILDPLATFORM golang:1.26 AS build

ARG TARGETOS
ARG TARGETARCH

WORKDIR /go/src/app
COPY . .

RUN go mod download && go mod verify

RUN CGO_ENABLED=0 GOOS=$TARGETOS GOARCH=$TARGETARCH go build -o /go/bin/app

FROM --platform=$TARGETPLATFORM gcr.io/distroless/static-debian12

COPY --from=build /go/bin/app /
CMD ["/app"]