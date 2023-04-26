# Cap & Eventual Consistency

# CAP 이론 이란?

Consistency ( 일관성 ) 
Availability ( 가용성 ) 
Partition Tolerance ( 분할 허용성 )

Cap 이론은 “ 적절한 응답 시간 내 세 가지 속성을 모두 만족시키는 분산 시스템을 구성할 수 없다”는 이론

분할이 생겼을 떄 일관성과 가용성 중 하나를 희생해야 한다는 것을 의미

# Eventual Consistency 란?

항목이 새롭게 업데이트 되지 않는다는 전제하에 항목의 모든 읽기 작업이 최종적으로는 마지막으로
업데이트 된 값을 반환한다는 것을 이론적으로 보장
