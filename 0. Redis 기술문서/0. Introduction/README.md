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