Docker Coompose file to bring up a 3 node rabbitmq cluster on a single server using 
docker-compose up -d OR
docker stack deploy -c docker-compose.yml rabbitmq

Please ensure the below file permissions for the stack / compose to work properly.

-rw-------    1 root     root          1512 Nov 18 14:16 docker-compose.yml
-rwxr-xr-x    1 root     root           191 Nov 18 13:21 cluster-entrypoint.sh
drwxr-xr-x    8 root     root           166 Nov 18 14:17 .git
-r--------    1 root     root            19 Nov 18 14:15 .erlang.cookie
-rw-------    1 root     root           169 Nov 18 14:15 .env

Once done, your rabbitmq management console can be browsed using the url : http://hostname:25672

NOTE: Should the "depend_on" condition is not met and all three nodes start at the same time, the secondary members have issues joining the cluster,
Ensure the primary is up and Issue the command: 
docker service scale rab3_rabbitmq2=0 rab3_rabbitmq3=0 
and after a few seconds, 
docker service scale rab3_rabbitmq2=1 rab3_rabbitmq3=1

Enjoy!
