ARG GO_VER=1.18
ARG GO_ARCH=bullseye
ARG OPERATOR_VER=1.19.1

FROM golang:${GO_VER}-${GO_ARCH}

# https://blog.scottchayaa.com/post/2018/11/04/docker-arg-env-variable/#arg
# ARG need to be declared again after FROM

ARG OPERATOR_VER
ARG GO_VER
ARG GO_ARCH


RUN if [ "${GO_ARCH}" == "alpine" ]; then apk add git curl bash alpine-sdk; fi


# Install operator-sdk 
RUN export ARCH=$(case $(uname -m) in x86_64) echo -n amd64 ;; aarch64) echo -n arm64 ;; *) echo -n $(uname -m) ;; esac) && \
    export OS=$(uname | awk '{print tolower($0)}') && \
    export OPERATOR_SDK_DL_URL=https://github.com/operator-framework/operator-sdk/releases/download/v${OPERATOR_VER} && \
    curl -LO ${OPERATOR_SDK_DL_URL}/operator-sdk_${OS}_${ARCH} && \
    chmod +x operator-sdk_${OS}_${ARCH} &&  mv operator-sdk_${OS}_${ARCH} /usr/local/bin/operator-sdk

# Install Golang extension package tools
RUN go install github.com/ramya-rao-a/go-outline@latest         && \
    go install github.com/cweill/gotests/gotests@latest         && \
    go install github.com/fatih/gomodifytags@latest             && \
    go install github.com/josharian/impl@latest                 && \
    go install github.com/haya14busa/goplay/cmd/goplay@latest   && \
    go install github.com/go-delve/delve/cmd/dlv@latest         && \
    go install honnef.co/go/tools/cmd/staticcheck@latest        && \
    go install golang.org/x/tools/gopls@latest



