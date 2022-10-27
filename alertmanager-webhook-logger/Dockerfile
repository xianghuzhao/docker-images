FROM golang:1.18 as builder

ARG VERSION=1.0

WORKDIR /app

RUN git clone --depth=1 --branch $VERSION https://github.com/tomtom-international/alertmanager-webhook-logger.git /app && \
    CGO_ENABLED=0 GOOS=linux GOARCH=amd64 GOPROXY=https://goproxy.cn go build -installsuffix 'static' . 

#RUN echo 'nobody:x:65534:65534:nobody:/:' > /etc/passwd && \
#    echo 'nobody:x:65534:' > /etc/group


FROM alpine

COPY --from=builder /app/alertmanager-webhook-logger /app/alertmanager-webhook-logger
#COPY --from=builder /etc/passwd /etc/passwd
#COPY --from=builder /etc/group /etc/group

# Perform any further action as an unprivileged user.
USER nobody:nobody

ENTRYPOINT ["/app/alertmanager-webhook-logger"]
