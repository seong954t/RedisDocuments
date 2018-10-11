## 1. 명령어

redis를 실행한다.

    $ ./redis-server
    $ ./redis-cli

기본 명령어들은 [RedisGate](http://redisgate.kr/redis/introduction/redis_intro.php)사이트에서 학습할 수 있다.

우선 String, List, Sets, Sorted Sets, Hashes 5가지의 데이터 타입으로이루어져있다.

각 데이터 타입에 대한 특징들에 따라 주로 사용될 것 이라고 생각되는 명령어들을 우선으로 학습하는 것이 좋을 것 같다.

1. Common Keys

    데이터 타입에 관계없이 모든 Key에 적용되는 명령을 우선 학습하였다.

    - Key 확인 및 조회 : EXISTS, KEYS, SCAN, SORT

    - Key 이름 변경 : RENAME, RENAMENX

    - Key 자동 소멸 관련 : EXPIRE, EXPIREAT, PEXPIRE, TTL, PTTL, PERSIST

    - 정보 확인 : TYPE, OBJECT

    - 샘플링 : RANDOMKEY

    - DATA 이동 : MOVE, DUMP, RESTORE, MIGRATE

    RANDOMKEY, DUMP, RESTORE는 초반에 많이 사용하지 않을 것 같았다. 나중에 자세히 다뤄봐야겠다.
