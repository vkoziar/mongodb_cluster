FROM dev24/mongodb:latest

# Install MongoDB
RUN yum install -y mongodb-org-mongos

EXPOSE 27017
ENTRYPOINT ["/usr/bin/mongos"]
