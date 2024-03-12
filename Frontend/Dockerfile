# Use the official NGINX image as base
FROM nginx:alpine

# Copy static files to NGINX server
COPY index.html /usr/share/nginx/html/
COPY style.css /usr/share/nginx/html/

# Expose port 80
EXPOSE 80
