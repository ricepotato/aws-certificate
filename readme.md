# AWS Certificate

### Aurora 복제본이 포함된 Amazon Aurora

- 관계형 데이터베이스
- 마이크로초 대기시간을 일관되게 유지할 수 없음.
- ElasticCache 를 사용하는 경우에도 마이크로초 대시간을 일관되게 유지할 수 없음
- Amazon Aurora : https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/CHAP_AuroraOverview.html
- Amazon ElastiCache for Memcached란 무엇인가요? : https://docs.aws.amazon.com/AmazonElastiCache/latest/mem-ug/WhatIs.html

### DyanamoDB Accelerator (DAX) 가 포함된 Amazon DynamoDB

- 키 값 레코드를 지원하는 NoSQL database
- DAX 는 마이크로초 단위로 응답시간을 제공함
- Amazon DynamoDB : https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Introduction.html
- DynamoDB Accelerator 를 통한 인 메모리 가속화 : https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/DAX.html
