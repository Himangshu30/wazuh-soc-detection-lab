FROM ubuntu:22.04
ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y \
    auditd audispd-plugins curl gnupg2 lsb-release \
    sudo openssh-server net-tools iproute2 nano \
    && apt-get clean

RUN useradd -m -s /bin/bash labuser && \
    echo "labuser:LabPass123!" | chpasswd

RUN mkdir /var/run/sshd

CMD service ssh start && service auditd start && tail -f /dev/null
