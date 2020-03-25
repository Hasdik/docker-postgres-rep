# docker-postgres-rep
# settings docker Swarm
1) Из master машины необходимо выполнить docker swarm init --advertise-addr IP_MASTER:2377 (указываем IP master машины)
2) Далее получим команду типа 'docker swarm join-token manager ...', это необходимо выполнить из slave машины, чтобы присоединить worker к кластеру.
# settings replication
1) Из master машины необходимо выполнить docker build -t vektor-postgres-master . для создания образа
2) Из slave машины необходимо выполнить docker build -t vektor-postgres-slave . для создания образа
3) Из master машины переходим в каталог с docker-swarm.yml и выполняем docker stack deploy -c docker-swarm.yml pg_replication
4) Из машины master выполняем ./restore для восстановаления существующей БД
5) Из webapp можно обращаться по host: IP_MASTER