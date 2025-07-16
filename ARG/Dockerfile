ARG version
FROM almalinux:${version:-9}
ENV COURSE="devops"\
        DURATION="120hrs"
        
ARG tranier="siva"
# this is for args can be passed to the conatiner
ENV tranier=$tranier 
RUN echo "Hi course is {{ $COURSE }}, Tranier is {{ $TRAINER }}, duration is {{ $DURATION }}"
CMD ["sleep","1000"]