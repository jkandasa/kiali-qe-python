FROM openshift/jenkins-slave-base-centos7

RUN yum install -y epel-release

COPY requirements.txt $HOME

RUN ls $HOME

# Install python and all requirements
RUN yum -y install \
        sudo \
        python2 \
        python2-pip \
        git \
        wget \
    && yum clean all

RUN useradd -d ${HOME} -u 1001 -g 0 -G wheel -m -s /bin/bash default

# Allow the wheel group to use sudo without a password
RUN echo '%wheel ALL=(ALL) NOPASSWD: ALL' >> /etc/sudoers

RUN chown -R 0:0 $HOME && \
    pip install --upgrade pip setuptools urllib3 && \
    pip install --ignore-installed -r ${HOME}/requirements.txt

RUN chown -R 1001:0 $HOME && \
    chmod -R g+rw $HOME

USER 1001
