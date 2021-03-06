---
layout: post
title:  "데이터 엔지니어 관련 영상 메모"
subtitle: "데이터 엔지니어 관련 영상 메모"
categories: data
tags: engineering
comments: true
---

Youtube에서 데이터 엔지니어로 검색해서 나온 몇 영상들을 보고 정리한 글입니다. 추후 영어 비디오도 정리할 예정입니다 (지속적으로 업데이트)

## 데이터 지능 팟캐스트. E11 데이터 엔지니어링편
---

- 넷플릭스 배재현님, 쿠팡 글로벌 최현식님(2018년 3월)
- [데이터 지능 팟캐스트](http://data-intelligence.io/?p=142)
- 넷플릭스 배재현님
	- 서치 백엔드 경력으로 시작해서 이렇게
	- 넷플릭스, 우버, 넷플릭스
	- 넷플릭스에서 실시간 파이프라인 (카프카)
	- 우버에선 시장데이터 분석 및 최적화
	- 카프카
		- 메세지 큐
		- 링크드인
		- 고전적 데이터 파이프라인은 지점 A에서 B로 보내면 B가 다른 쪽으로 보내고, 그리고 저장하는 방식
		- 카프카는 브로커 컨슈머 프로듀서. 브로커가 저장하고 프로듀서가 보내고 컨슈머가 받고. 브로커가 디스크에 저장하니 메세지 큐라고 생각
		- 카프카가 생기고 개런티드 딜리버리란 말을 쉽게 사용하게 됨
		- 컨슈머가 데이터를 가져가는 과정에서 락이 없음
		- 자바, 씨쁠쁠에선 락을 걸지만 카프카는 토픽. 내부에 파티션이 존재해서 락이 없어도 됨
		- 실시간 처리한 이유는 드루이드 프로젝트 파일럿. 드루이드에서 카프카를 사용하고 있어서 사용  
- 쿠팡 최현식님
	- 그루터에서 컨트리뷰터 (타조?), 쿠팡 미국지사
		- 타조 : 기능적으론 Hive와 동일
	- ETL 데이터 파이프라인 설계, 구현, 유지보수, 머신러닝 파이프라인 일부   
	- 하이브 시퀄, 스팤sql, sql 최적화 airflow 관리, r 서버 관리 등
	- S3에서 Hive로, Hive에서 오로라로 동기화
	- 오로라 : 데이터 웨어하우스  
	- 보통 관계형 DB/OLTP : 히스토리가 아닌 현재 값만 저장
	- Operation DB : 트랜잭션에 최적화. 분석을 하면 서비스에 영향을 줄 수 있어서 분석엔 적합하지 않음
	- Change data capture : mysql의 데이터를 dump떠서 hive로 load
	- db의 오버헤드가 크고 실시간이나 잦은 주기로 덤프를 뜨면 db에 오버헤드가 생김
- 김진영님이 생각한 데이터 엔지니어링 : 로우하게 하둡 관리, 파이프라인 관리, 메트릭 관리 등으로 나눌 수 있다고 생각

### 데이터 과학자들과 어떻게 일을 하는지?
- 데이터 사이언스 : 문제 정의 - 데이터 검증 - 실험
- 데이터 엔지니어링 : 데이터를 질의 가능하게 처리. 데이터 과학자가 할 수 있을정도로 만들고, 데이터 엔지니어링이 그 밑단 데이터 준비
- 엔지니어링과 사이언스 사이에 구분이 애매함. 데이터 사이언스에서 시작한 엔지니어링은 지속 가능하기 쉽지 않음
- 서로의 언어를 이해할 수 있어야 함
- 쿠팡은 workflow가 백여개가 있는데 job이 오래 걸리거나 문제가 생기는 경우 데이터 사이언티스트가 최적화를 해달라고 요청. 이럴 때 시퀄, 스팤시스템 최적화 등을 진행
- 타조 시스템을 통해 분산 시스템을 이해하고 있기에 가능함
- 비즈니스 로직부터 이해하면 필요없는 구문이나 조인을 찾을 수 있음

### 데이터 엔지니어링의 역사
- 데이터를 질의 가능하게 만든다는 관점으로 보면, 랭킹 시스템/검색 시스템도 데이터 엔지니어링이라 볼 수 있음
- 맵리듀스 논문. 프로토콜 버퍼. 직렬화/역직렬화 논문을 읽어보길
- 하둡, 하둡을 쉽게 사용하기 위한 하이브, 하둡 2.0 생기고 스케쥴러 yarn이 별도로 나옴
- 지금은 batch 일을 하다보니 하둡 자체는 잡 스케쥴러 yarn과 자체 데이터센터인 hdfs 외에는 크게 커다란 비중을 차지하고 있진 않은 듯
- 하둡의 IO는 디스크에서 발생하고 스파크는 메모리! 스파크가 강세
- denormalization, schemaless한 데이터를 다루고, nosql

### 데이터 엔지니어의 스킬셋
- Q) 스킬셋이 최근에 바뀐 것 같은데 어떤가요?
- A) 클라우드 서비스가 점점 나와서 데이터 엔지니어들이 했던 일들이 점점 대체되고 있는 듯  
	- 하둡 : 프러덕션 / 분석 2가지로 사용됨. 프러덕션에는 여전히 중요함. 추천 엔진이나 검색 로직은 최적화가 필요해서 여전히 엔지니어링이 많이 필요함. 반면 분석은 점점 엔지니어링 스킬이 없어도 점점 가능. 인프라가 고도화되며 분석을 위한 도구를 만들던 데이터 엔지니어는 아리송 그러나 데이터 엔지니어는 계속 수요가 있음  
	- 비즈니스 어플리케이션을 만들 수 있는 사람이 되야 함 모든 것이 자동화되는 것은 먼 미래의 일이기에 수요가 있지만, 커리어의 그로스가 있을 분야인가 걱정함. 너무 빠르게 변화중(이건 딥러닝도 동일)  
	- 분석을 위한 데이터 엔지니어링은 어느정도 성숙기
	- (내 생각 : 딥러닝/머신러닝을 위한 데이터 엔지니어링은 아직 성장기인듯! 분산 딥러닝 같은 것과 Serving)
	- 데이터 분석은 90%정도는 SQL로도 커버 가능하다고 생각. 그래서 이 직군의 성장에 대한 고민을 하는듯  
- 진영님 Q) IOT같은 곳에서 데이터 처리가 더 중요하고, 요즘은 센서에서 음성 데이터를 모집할테니 이것도 발전이 필요하지 않을까요?
- A) 리얼타임은 아직 발전이 많이되진 않음. 로우 레이턴시와 하이 아이피에스는 항상 이슈! AB Test를 위해 셋업하고 그걸 보기 위해 이것저것 만듬. 사이언티스트도 ETL을 점점 관리하는듯
	- 자체 데이터센터 구축한 사례 : 데이터 엔지니어링을 작게 시작하면 벤더에 주문하는 방식. 장비 셋팅까지 너무 오래걸리고 안정화까지 오래 걸림. 배포나 어플리케이션들 다 직접 개발. 페이스북 급 아니면 클라우드가 정답일듯
- 클라우드가 보안 관련이 취약적이다? 그렇지 않음 하드에 있다고 보안이 되는건 아님. 차라리 클라우드가 일관적으로 커버 가능하고 복구하는 기능이 존재. 전통적인 기업에서 걱정하는데, 딱히?   
- 진영님 Q) 어떤 종류의 데이터는 클라우드에 올라가면 안된다 이런거 있지 않나?
- A) 개인 정보는 안됨! 법무팀과 이야기해서 처리했음

### 데이터 엔지니어로서 보람 및 단점
- 엔지니어링 문제를 해결하는 과정. 즐거움은 어려운 문제를 해결했을 때 느끼는 자기만족과 남들이 인정할 때(구현한 시스템이 비즈니스에 임팩트) 행복
- 데이터 과학자들이 제가 구축한 시스템을 사용하며 기분이 좋아지지만 몸은 힘들어지는 과정. 제 이름을 몰라도 시스템의 이름을 알면 기분이 좋아짐
- 어려운 문제를 해결해야 되는 중압감과 시스템 장애를 대처하는 책임감은 힘들고 고통받았음. 시스템이 유명해질수록 시스템의 한계도 빨리 오는 편. 오픈소스에 의존하는데 오픈소스 내부까지 이해하지 않으면 디버깅하기 힘듬. 소스코드를 읽어보고 커뮤니티에서 커버하지 못하면 자신이 패치하거나 해결해야 함
- 단순히 오픈소스를 조합해 파이프라인을 만드는 것은 누구나 할 수 있음. 진짜 어려운 문제를 해결하는 것부터 본인의 역량이 중요  

### 데이터 엔지니어링을 시작하려는 분들에게 조언
- 굉장히 매력적인 분야. 수업에서 배운 내용을 그대로 쓸 수 있음(컴퓨터 사이언스 지식)
- 아무리 툴이 고도화되고 데이터 사이언스와 데이터 엔지니어가 점점 구분이 흐려지고 있지만, 본질은 변하지 않음. 분산 시스템과 데이터 구조, 알고리즘 공부를 많이 하길!  
- 스파크, 배치 스트리밍 등을 다룰 수 있는 것도 기본기가 있었기 때문에 가능하다고 생각
- 제네럴리스트는 점점 가치를 잃고있는 것 같으니 본질에 집중하며 자신의 관심사에 대해 깊게 공부하는 것을 추천
- 데이터베이스! (쿼리 프로세스 체크는 하이브 이해할 때 좋음) 데이터 웨어하우스 챕터를 잘 이해하면 데이터레이크 이해할 때 도움이 될 것
- 자신이 잘 다루는 오픈소스! 잘 정리된 자료가 거의 없으니 직접 사용해보고 소스를 까보는 것을 추천
- 학생들에게 실습을 추천한다면 방법은?
	- 데이터 과학은 캐글이 있는데 데이터 엔지니어링은?
	- 실습은 보통 오픈소스 홈페이지가서 튜토리얼 따라하는 정도뿐이고  사실 공부하기 쉽지 않음. 데이터 엔지니어링의 실력은 scalability과 트러블슈팅을 어떻게 하는지가 중요한데 대용량 환경을 경험해봐야 함
	- AWS를 사용해서 서버 구축정도는 경험해볼 순 있지만 의미있는 데이터를 경험하긴 힘듬 ㅠㅠㅠ 사실 여전히 어떻게 할지는 어려움  
- 데이터 엔지니어 주니어를 거의 뽑지 않음. 어플리케이션과 연결되있으면 순수 데이터 엔지니어보단 프러덕 개발에 가깝게 신입을 뽑긴하지만 고전적 데이터 엔지니어는 주니어를 잘 뽑지 않음


## [실리콘밸리의 한국인 2018] 세상에 임팩트를 주는 엔지니어
---

- 김형진 우버 데이터 엔지니어(2018년 4월)
- [영상](https://www.youtube.com/watch?v=NscFye0yM5Q)
- 엔지니어가 원하는 것은 무엇인가? 돈? 워라밸? 복지? 
- 세상을 바꾸는 임팩트를 주는 엔지니어가 되고 싶다라는 엔지니어가 꽤 있음
- Hacker News : 주말동안 못 만드는 이유는 효율성과 확장성!
- 우버의 마켓플레이스 팀
	- 드라이버 포지셔닝
	- 다이나믹 프라이싱
	- 플랫폼, 데이터
	- 매칭 
		- Uber X
		- 합석
		- 40억회 매칭
- 매칭팀의 효율성 프로젝트(Uber X)
	- 예약 매칭(Forward Dispatch)
		- 현재 여정이 곧 끝날 예정이라면, 다음 승객을 미리 연결
	- 여정 교환(Trip Swap)
		- 더 나은 운전자/승객 매칭이 가능해지면 교환을 통해 모두 win-win
	- 지속적 최적화(Continuous Optimization)
		- 지역의 상황 변화에 따라 계속적으로 매칭을 최적화
	- 프로젝트가 가져온 임팩트
		- 여정 교환을 통한 시간 절약 : 1주일당 10년 이상
		- 예약 매칭을 통한 시간 절약 : 1주일간 40년 이상
- 우버 익스프레스 풀
	- 추가적으로 기다리기
	- 지정돠니 장소로 걸어가기
	- 더 저렴한 가격
- 2017년 5월 기준 총 50억회의 여정 달성
- 2017년 한 해 동안 총 40억회 여정 달성
- 만약 우버에서 일어나는 모든 여정의 예상 도착시간을 1분씩 절감한다면?
	- 매년 76명의 삶에 해당하는 시간을 절약!  
- 효율성 X 확장성 = 임팩트!





## 구글 엔지니어가 들려주는 디자인, 클라우드, 빅데이터 이야기
---

- 구글 클라우드 엔지니어, 홍기락(2017년 9월)
- [영상](https://www.youtube.com/watch?v=P3AP32fg5X8)
- 앞부분만 들었음. 뒷부분은 디자이너가 개발하고 싶다면? 부분은 메모하지 않음
- 조지아텍 컴퓨터 사이언스 박사
- 빅데이터 관련 툴을 만드는 중!

## 클라우드가 인기있는 이유
- 기술적으론 예전부터 다 존재하던 것
- 데이터가 많아지며 컴퓨터 100대, 1000대를 직접 운영하기 어려워서 선호
- 데이터가 왜 많아졌나?
	- 데이터가 점점 쌓임. 병원 같은 곳도 데이터를 쌓는 중
	- 데이터가 쌓여서 우리가 못할 것이라고 했던 것들을 할 수 있게됨
	- 맵리듀스

## 분산시스템
- 분산 시스템이 좋아서 기락님은 시작
- 구글이 시작한 것은 이유가 있음
	- 맵리듀스 논문을 공개
	- 하둡이 생겨 비즈니스(그러나 구글이 하진 않음)
	- 구글도 이제 이런 것을 구현해 비즈니스를 하자!
- 클라우드 예시
	- 가상으로 머신 제공
	- 크롬북. 네트워크만 되면 모든 것이 될 수 있도록 설정(다른 불필요한 프로그램 없이)  
	- 고객 데이터를 클라우드에 올려서 분석(하이레벨 API 제공)
	- 구글 드라이브, 구글 포토
	























