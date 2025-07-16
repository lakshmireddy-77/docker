FROM almalinux:9
RUN mkdir /tmp/workdir-demo
RUN cd /tmp/workdir-demo
RUN pwd
RUN echo "I am in working directory " > hello.txt
# to keep the container busy
CMD ["sleep", "1000"]