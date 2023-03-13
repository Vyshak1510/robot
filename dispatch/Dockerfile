FROM golang:1.17

WORKDIR /go/src/app

COPY *.go .
COPY --from=fzf53242.live.dynatrace.com/linux/oneagent-codemodules:go / /
ENV LD_PRELOAD /opt/dynatrace/oneagent/agent/lib64/liboneagentproc.so

RUN go mod init dispatch && go get
RUN go install

CMD dispatch
