FROM alpine:3.20 as dist

RUN arch=$(uname -m) && \
    if [ "$arch" = "x86_64" ]; then \
        export DIST_ARCH=linux-arm64; \
    elif [ "$arch" = "aarch64" ]; then \
        export DIST_ARCH=linux-arm64; \
    else \
        echo "Unsupported architecture: $arch" && \
        exit 1; \
    fi

ADD dist/*$IMAGE_ARCH.tar.gz /dist

FROM alpine:3.20

RUN apk add --no-cache ca-certificates

COPY --from=dist /dist/ /app/

RUN ln -s /app/pulsarctl /usr/local/bin/pulsarctl

CMD ["/app/pulsarctl"]
