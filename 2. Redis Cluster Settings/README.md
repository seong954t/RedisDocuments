# 2. Redis Cluster Settings

\* 별도의 언급이 없는 한 모든 작업은 /home/redis_4/redis-stable 경로에서 이루어진다.

**Redis Cluster Settings의 목표는 아래의 명령어가 실행되도록 하는 것이다.**

Redis Cluster를 시작하기 위해서 redis-trib.rb를 실행해야 한다.
아래의 명령어를 통해 실행해보자.

    $ src/redis-trib.rb

<br><img src="./img/img03.png" width="398px">

<br>
만약 Ruby가 없다면 위와 같은 Error Message가 나타날 것이다. 이것은 ruby가 설치되어있지 않아서 발생하는 문제이니 ruby를 설치해보자. 
