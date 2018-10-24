# Updated as of Oct 23, 2018
FROM httpd:latest

#Author of the Docker File
LABEL "Maintainer"="Cusey"

# Copy the following directory
COPY hello-world-html/ /usr/local/apache2/htdocs/hello-world-html

# Copy httpd.conf with changes to the root directory
COPY httpd.conf /usr/local/apache2/conf