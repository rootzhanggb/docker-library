#FROM gcr.io/google_containers/ubuntu-slim:0.6
FROM ubuntu:14.04
MAINTAINER zgb <312768277@qq.com>
# Ensure there are enough file descriptors for running Fluentd.
RUN ulimit -n 65536

# Disable prompts from apt.
ENV DEBIAN_FRONTEND noninteractive

# Copy the Fluentd configuration file.
COPY td-agent.conf /etc/td-agent/td-agent.conf

COPY build.sh /tmp/build.sh
RUN chmod a+x /tmp/build.sh && cp /tmp/build.sh /mnt
RUN /mnt/build.sh
# set cst +8:00
ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

ENV LD_PRELOAD /opt/td-agent/embedded/lib/libjemalloc.so

# Run the Fluentd service.
ENTRYPOINT ["td-agent"]
