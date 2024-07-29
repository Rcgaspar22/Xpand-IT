FROM centos:7

# Defina a versão do Tomcat que queremos baixar
ENV TOMCAT_VERSION=9.0.91

# Adicionar repositórios YUM corretos
RUN sed -i 's|^mirrorlist=|#mirrorlist=|g' /etc/yum.repos.d/CentOS-*.repo && \
    sed -i 's|^#baseurl=http://mirror.centos.org|baseurl=http://vault.centos.org|g' /etc/yum.repos.d/CentOS-*.repo

# Atualize os pacotes e instale wget, Java e tar
RUN yum clean all && \
    yum update -y && \
    yum install -y wget java-1.8.0-openjdk tar && \
    yum clean all

# Baixe e extraia o Tomcat
RUN wget https://downloads.apache.org/tomcat/tomcat-9/v${TOMCAT_VERSION}/bin/apache-tomcat-${TOMCAT_VERSION}.tar.gz && \
    tar xzvf apache-tomcat-${TOMCAT_VERSION}.tar.gz -C /opt && \
    mv /opt/apache-tomcat-${TOMCAT_VERSION} /opt/tomcat && \
    rm apache-tomcat-${TOMCAT_VERSION}.tar.gz

# Exponha a porta 8080 para acessar o Tomcat
EXPOSE 8080

# Inicie o Tomcat
CMD ["/opt/tomcat/bin/catalina.sh", "run"]
