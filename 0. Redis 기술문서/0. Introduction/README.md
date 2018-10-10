## 0. 소개

Redis라는 Cache Server에 대해 알아보자.

1. __Redis__ 란?

    __Re__ mote __Di__ ctionary __S__ ystem으로 Key/Value Store라고 한다.
    원격 사전 시스템? 이라고 보면 될지 모르겠다. 사전처럼 데이터를 넣어놓고, 원격에서 요청하여 정보를 얻어가는 형태인가보다.

    NoSQL DBMS로 분류되기도 하고, Memcached와 같은 In Memory 솔루션으로 분류되기도 한다고 한다.
    성능은 Memcached에 버금가면서 다양한 데이터 구조체를 지원하여 Message Queue, Shared memory, Remote Dictionary용도로 사용될 수 있다고 한다.

2. __Key/Value Store__

    Redis의 기존인 Key/Value Store는 특정 __Key__ 에 __Value__ 를 저장하는 구조로 되어있고, __PUT/GET Operation을 지원__ 한다고 한다.

    key   | value
    ----- | ------
    key_1 | value_1
    key_2 | value_2
    key_3 | value_3
    key_4 | value_4

    모든 데이터는 메모리에 저장되고, 이로 인해 매우 빠른 __read/write__ 속도를 보장한다. 그래서 전체 저장 가능 __데이터 용량은 물리적인 메모리 크기를 넘을 수 없다.__

    Server restart와 같은 상황에서 __데이터 저장을 보장하기 위해 Disk persistence store__ 로 사용한다.

3. __다양한 데이터 타입__

    단순 Key/Value Store 이라면 Memcached를 사용하면 되지만, Redis를 사용하는 가장 큰 이유 중 하나는 __Object가 아닌 자료구조를 갖는다__ 는 것이다.
    크게 __String, Set, Sorted Set, Hashes, List__ 로 5가지의 데이터 구조를 갖는다.

    \* Redis에서 하나의 키당 총 2^32개의 데이타를 이론적으로 저장할 수 있으나, 최적의 성능을 낼 수 있는 것은 일반적으로 1,000~5,000개 사이로 알려져 있다.

4. __Persistence__

    기본적으로 memcached의 경우 Memory에만 데이터를 저장하여 서버 restart 시 데이터 유실이 있지만, Redis는 disk에 데이터를 저장 하기 때문에 restart 시 데이터를 다시 읽어 Loading하기 때문에 데이터 유실이 되지 않는다.

    Redis 데이터 저장 방법

    1. Snapshotting (RDB) 방식

        순간적으로 __메모리 내용 전체를 DISK에 옮긴다.__

        SAVE와 BGSAVE 두가지 방식이 존재한다.

        1. SAVE방식은 Blocking 방식으로 순간적으로 Redis의 모든 동작을 정지시킨 후, 그 때의 snapshot을 disk에 저장한다.

        2. BGSAVE방식은 Non-Blocking방식으로 별도의 process를 통해 명령어 수행 당시 메모리 snapshot을 disk에 저장한다.(저장 순간 Redis는 정상동작 한다.)

        - 장점 : snapshot을 그대로 뜨기 때문에, 서버 restart시 snapshot만 load하면 되어 restart 시간이 빠르다.
        
        - 단점 : snapshot 추출 시간이 오래 걸리고, snapshot 추출 후 서버가 down되면 이후 데이터가 유실된다.(백업 시점의 데이터만 유지!)

    2. Append on File (AOF) 방식

        Redis의 모든 write/update연산 자체를 모두 __Log 파일에 기록__ 한다.

        서버 restart 시 write/update operation이 순차적으로 재실행되며 데이터를 복구한다. operation이 발생할때 마다 매번 기록하여 RDB와는 다르게 특정 시점이 아닌 현재 시점까지의 Log를 기록할 수 있다.(Non-Blocking Call) 

        - 장점 : Log file에 대해서 append만 하여 Log write 속도가 빠르고, 언제 서버가 down되어도 데이터 유실이 없다.

        - 단점 : 모든 write/update operation에 대해 Log를 남기기 때문에 RDB에 비해 과대하게 크다. 복구시 저장된 write/update operation을 다시 replay하여 restart 속도가 느리다.
    
    __RDB와 AOF를 혼용__ 해서 사용하는 것이 바람직하다. 주기적으로 snapshot으로 백업을 하고, 다음 snapshot까지의 저장을 AOF로 수행한다.

    이렇게 수행할 경우 __서버 restart 시 백업된 snapshot을 reload__ 하고, 소량의 __AOF Log들만 replay__ 하기 때문에 __restart 시간을 절약__ 하면서 __데이터 유실을 방지__ 할 수 있다.

