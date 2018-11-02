## 3. Redis Cluster Data Sharding

- Redis에서 Data Sharding을 통해 Cluster Node를 추가하고, 제거를 쉽게 할 수 있다.

- Redis Cluster는 일관된 hashing을 사용하지 않는다. 그러나 그것은 모든 key가 hash slot이라고 불리는 sharding의 다른 형태이다.

- Redis Cluster에는 16384 개의 hash slot이 있고, 주어진 key의 hash slot을 계산하기 위해 CRC16 mod 16384의 값을 가져온다.

    이러한 slot을 통해 cluster에 node를 쉽게 추가하고, 제거할 수 있다.

 

- 각각 hash slot을 가지고 있는 cluster 된 node A, B, C가 있고, 새로운 node D 가 추가된다고 가정하자.

    이 때 새로운 node D를 추가하기 위해 A, B, C의 hash slot을 D에게 일부 할당해주어야 한다. 이와 마찬가지로 node D를 삭제하기 위해서는 node D의 slot을 A, B, C에게 되돌려 준 후 node D가 비어있다면, 삭제할 수 있다.