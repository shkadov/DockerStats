# DockerStats
Script for gathering Docker containers names and stats
#!/bin/bash

# Gathering docker containers stats for zabbix
#
# by den.shkadov@namecheap.com
delim='-------------------------------'
stats=0
#while [ 1 ]; do
declare -a name=( $(docker ps --format "table {{.ID}}\t{{.Names}}" | sed 1d |awk '{print $2}') )
for contName in ${name[@]}
do
        stats=`docker stats $contName --no-stream | awk '{print $2,$8}'|sed 1d| sed 's/%//g'`
echo "$contName" "$stats"
#echo "$delim"
done
#sleep 5
#done
