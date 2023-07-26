# build container stage 1
#use specific version tag, don't use latest tag.
FROM ubuntu:20.04 
ARG DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -y golang-go=2:1.13~1ubuntu2
COPY app.go .
RUN pwd
RUN CGO_ENABLED=0 go build app.go

# app container stage 2
FROM alpine:3.12.0
#belwo line will male file system read only
RUN chmod a-w /etc
#don't run image as root,use specific user.
RUN addgroup -S appgroup && adduser -S appuser -G appgroup -h /home/appuser
#belwo line will remove shell access
RUN rm -rf /bin/*
COPY --from=0 /app /home/appuser/
USER appuser
CMD ["/home/appuser/app"]
