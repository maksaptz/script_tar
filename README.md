#!/bin/bash

#имена старых архивов
#ls /root/back -lt | tail -n +4 | awk '{ print $9 }'

#если бэкап завершен успешно
if tail -n 1 /var/log/rsnapshot.log | grep "completed successfully" &> /dev/null
then    #создаем новый архив
        mkdir /root/olo/$(date '+%Y-%m-%d')
        cd /root/test
        find ./ -maxdepth 1 -type d -exec tar -czf /root/olo/$(date '+%Y-%m-%d')/'{}'.tar.gz '{}' \;
        #then tar -czf /root/back/"$(date '+%Y-%m-%d').tar.gz" -C /root/test data
        #удаляем старые архивы
#       cd /root/olo
#       rm $(ls /root/back -lt | tail -n +4 | awk '{ print $9 }') &> /dev/null
fi
