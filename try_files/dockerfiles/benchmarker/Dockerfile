FROM alpine:3

RUN apk add --no-cache --virtual deps curl && \
    curl -LO https://storage.googleapis.com/hey-release/hey_linux_amd64 && \
    mv hey_linux_amd64 /usr/local/bin/hey && \
    chmod +x /usr/local/bin/hey && \
    apk del deps

ENTRYPOINT ["/usr/local/bin/hey"]
CMD ["--help"]
