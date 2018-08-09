FROM zabbix/zabbix-appliance:centos-3.4.12

RUN find /etc/yum.repos.d/*.repo -type f | xargs -i mv {} {}.bak

COPY ["conf/Centos-7.repo", "/etc/yum.repos.d/"]
COPY ["fonts/msyh.ttf", "/usr/share/fonts/dejavu"]

RUN rm -rf /etc/localtime && ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
    rm -f /usr/share/zabbix/fonts/graphfont.ttf && \
    ln -s /usr/share/fonts/dejavu/msyh.ttf /usr/share/zabbix/fonts/graphfont.ttf && \
    yum --quiet makecache && \
    yum -y install kde-l10n-Chinese glibc-common && \
    localedef -c -f UTF-8 -i zh_CN zh_CN.utf8 && \
    export LC_ALL=zh_CN.utf8 && \
    yum -y clean all && \
    rm -rf /var/cache/yum/ 

EXPOSE 80/TCP 443/TCP 10051/TCP 3306/TCP

VOLUME ["/usr/lib/zabbix","/var/lib/zabbix","/etc/zabbix","/etc/ssl/nginx"]