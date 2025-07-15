FROM almalinux:9
RUN dnf install nginx -y 
RUN rm -rf /usr/share/nginx/html/index.html
ADD https://raw.githubusercontent.com/Lakshmiredddy/Terraform/refs/heads/main/notes.md   /usr/share/nginx/html/index.html
RUN chmod +r  /usr/share/nginx/html/index.html
CMD ["nginx", "-g" , "daemon off;"]




