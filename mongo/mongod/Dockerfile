FROM treasureboat/centos6
RUN echo '[mongodb-org]' > /etc/yum.repos.d/mongodb.repo
RUN echo 'name=MongoDB 3.2 Repository' >> /etc/yum.repos.d/mongodb.repo
RUN echo 'baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.2/x86_64/' >> /etc/yum.repos.d/mongodb.repo
RUN echo 'gpgcheck=1' >> /etc/yum.repos.d/mongodb.repo
RUN echo 'enabled=1' >> /etc/yum.repos.d/mongodb.repo
RUN echo 'gpgkey=https://www.mongodb.org/static/pgp/server-3.2.asc' >> /etc/yum.repos.d/mongodb.repo

# Install MongoDB
RUN yum install -y mongodb-org-server

# Create the MongoDB data directory
RUN mkdir -p /data/db

EXPOSE 27017
ENTRYPOINT ["usr/bin/mongod"]

