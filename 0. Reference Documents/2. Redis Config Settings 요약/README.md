## 2. Redis Config Settings 요약<sub>reference by [RedisGate Cluster Start](http://redisgate.kr/redis/cluster/cluster_start.php)<sub/>

**3. Start (Single Machine) Redis Cluster 의 Config Setting내용을 간단하게 요약한 문서이다.**

현재 설정한 cluster를 실행하기 위해 redis.conf 파일에서 변경한 내용들에 대해서 작성하였다.

    port [변경 포트 번호]
    cluster-enabled yes
    cluster-config-file nodes.conf
    cluster-node-timeout 3000
    appendonly yes
    dir [redis.conf 경로]

\* 추가<sub>자세한 내용은 [Moss' tistory](http://moss.tistory.com/entry/Redis-%EC%84%9C%EB%B2%84-%EC%84%A4%EC%A0%95-%EC%A0%95%EB%A6%AC) 참고</sub>

    maxclients [client 수] : 한번에 연결될 수 있는 최대 client 수 설정 Redis process의 file descriptor의 숫자만큼 연결 가능. "0"은 제한 없음을 의미

    maxmemory [bytes] : memory limit 시 설정 된 maxmemory-policy에 따라 기존 key가 제거된다.

    maxmemory-policy [policy] : maxmemory에 도달했을 때 삭제 정책을 설정한다. (policys : volatile-lru, allkeys-lru, volatile-random, allkeys-random, volatile-ttl, noeviction)

이를 여러개의 port에 대해 설정할 경우

    1. port 번호 폴더 생성
    2. 생성된 port 번호 폴더에 redis.conf 파일 복사
    3. 위의 설정 정보로 내용 수정
    4. port 번호 폴더의 redis.conf로 redis-server 실행

의 절차를 통해 진행하면 된다.