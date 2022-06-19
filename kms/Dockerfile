FROM alpine:latest as builder
WORKDIR /root
COPY ./source/* /root/
RUN ls -all /root/
RUN apk add --no-cache git make build-base && \    
    git clone --branch master --single-branch https://github.com/Wind4/vlmcsd.git && \
    cd vlmcsd/ && \
    make


FROM alpine:latest as kms
WORKDIR /root/
COPY --from=builder /root/vlmcsd/bin/vlmcsd /usr/bin/vlmcsd
EXPOSE 1688/tcp
CMD [ "/usr/bin/vlmcsd", "-D", "-d" ]

