# 4. Start (Multy Machine) Redis Cluster <sub>reference by [Cluster Redis-trib.rb of RedisGate](http://redisgate.kr/redis/cluster/redis-trib.php)</sub>

\* 3개의 CentOS(Machine)와 redis 설정을 한 이후 진행하면 된다.

\* [3. Start (Single Machine) Redis Cluster](https://github.com/seong954t/RedisStudy/tree/master/3.%20Start%20(Single%20Machine)%20Redis%20Cluster)에서 한 절차와 동일하게 각 Machine(컴퓨터)에서 7000 / 7001 폴더 생성 후 redis.conf를 설정해준다.

**(Multy Machine) Redis Cluster의 목표는 3개의 독립적인 Machine을 Cluster하여 Cluster의 데이터 저장이 어떻게 되는지 테스트하는 것이다.**