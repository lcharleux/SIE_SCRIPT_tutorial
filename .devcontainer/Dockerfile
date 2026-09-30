FROM mcr.microsoft.com/devcontainers/python:1-3.12-bookworm

ARG HUGO_VERSION=0.150.0
ARG DART_SASS_VERSION=1.92.1
ARG TARGETARCH

ENV PATH="/opt/venv/bin:/usr/local/hugo:/usr/local/dart-sass:${PATH}" \
    PIP_DISABLE_PIP_VERSION_CHECK=1 \
    PIP_NO_CACHE_DIR=1

COPY requirements-dev.txt /tmp/requirements-dev.txt

RUN set -eux; \
    case "${TARGETARCH}" in \
      amd64) deb_arch=amd64; sass_arch=x64 ;; \
      arm64) deb_arch=arm64; sass_arch=arm64 ;; \
      *) echo "Unsupported architecture: ${TARGETARCH}" >&2; exit 1 ;; \
    esac; \
    curl -fsSL -o /tmp/hugo.tar.gz "https://github.com/gohugoio/hugo/releases/download/v${HUGO_VERSION}/hugo_extended_${HUGO_VERSION}_linux-${deb_arch}.tar.gz"; \
    mkdir -p /usr/local/hugo; \
    tar -C /usr/local/hugo -xzf /tmp/hugo.tar.gz; \
    curl -fsSL -o /tmp/dart-sass.tar.gz "https://github.com/sass/dart-sass/releases/download/${DART_SASS_VERSION}/dart-sass-${DART_SASS_VERSION}-linux-${sass_arch}.tar.gz"; \
    tar -C /usr/local -xzf /tmp/dart-sass.tar.gz; \
    python -m venv /opt/venv; \
    /opt/venv/bin/pip install --upgrade pip; \
    /opt/venv/bin/pip install -r /tmp/requirements-dev.txt; \
    rm -f /tmp/hugo.tar.gz /tmp/dart-sass.tar.gz /tmp/requirements-dev.txt
