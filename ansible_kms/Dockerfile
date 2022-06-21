FROM ubuntu:20.04 as ansible_kms

ARG TZ Europe/Moscow
ENV TZ $TZ

WORKDIR /root
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
RUN apt update && apt install -y software-properties-common cron && add-apt-repository --yes --update ppa:ansible/ansible && apt install -y ansible && \
apt install -y python-dev libkrb5-dev krb5-user && \
mv /etc/krb5.conf  /etc/krb5.conf.back 

COPY krb5.conf /etc/krb5.conf

ARG SHEDULE  "0 */1 * * *"
ENV SHEDULE $SHEDULE
RUN  echo "${SHEDULE} chmod +x /root/run.sh && /bin/bash /root/run.sh" >> /mycron | crontab -u root /mycron  
RUN  crontab -l

VOLUME [ "/var/log", "/root" ]

#CMD [ "cat",  "/etc/krb5.conf", "&& tail -f /dev/null" ]
CMD ["cron","-f"]



