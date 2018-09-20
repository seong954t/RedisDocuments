# 3. Start (Single Machine) Redis Cluster

\* 이전과 동일하게 /home/redis_4/redis-stable 경로에서 작업한다.

\* 7000 / 7001 / 7002 port에 대해 Cluster를 진행한다.

**(Single Machine) Redis Cluster의 목표는 7000 / 7001 / 7002 port의 server를 하나의 컴퓨터에서 Cluster하는 것이다.**

## 3.1 7000 / 7001 / 7002 폴더 생성

아래 명령어를 통해 3개의 폴더를 생성해주자.


    $ mkdir 7000 7001 7002

## 3.2 redis.conf 파일 수정 및 복사


폴더를 생성했다면,  /home/redis_4/redis-stable 에 있는 redis.conf파일을 해당 폴더로 복사한다.

이 때, redis.conf 파일의 내용을 아래와 같이 수정한다.

\* 아래 명령어를 통해 vim으로 수정 가능하다.

    $ vi redis.conf

 vim 에디터에서 아래 명령어를 통해 텍스트 검색을 하면 된다.

    $ esc + :/[검색 내용]

 수정 내용들을 찾아 아래와 같이 변경하자.

    port [포트번호]                     ->         ex) port 7000

    cluster-enabled yes                    

    cluster-config-file nodes.conf     

    cluster-node-timeout 3000         

    appendonly yes                          

    dir [conf 파일 디렉토리]            ->         ex) dir /home/redis_4/redis-stable/7000

 

수정 후 아래와 같이 redis.conf파일을 저장하자.

    $ esc + :wq

 