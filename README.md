# KOCWBigdata
KOCW 숭실대학교 박영택 교수의 빅데이터분산컴퓨팅을 들으면서 쓴 강의노트
Apach Hadoop 이란?
	• 빅데이터를 저장, 처리, 분석할 수 있는 소프트웨어 프레임워크
	• Distributed : 수십만대의 컴퓨터에 자료 분산 저장 및 처리
	• Scalable : 용량이 증대되는 대로 컴퓨터 추가
	• Fault-tolerant : 하나이상의 컴퓨터가 고장나는 경우에도 시스템이 정상작동
	• Open Source : 공개 SW
	• 오픈소스 프로젝트이며, 약 10개 회사의 60명의 Committer
	• 수 백명의 Contributor들이 개발 중이고, Bug 수정 등의 작업을 수행
	• 다양하고 많은 프로젝트, 애플리케이션, 도구에서 사용됨
	• 다양 에코 시스템 : 여러회사에서 사용을 할때 여러가지 엑세서리가 추가 되는 것을 의미함
		○ SQL을 다시 공부할 필요가 있음(HIVE 에코 시스템 활용)
	• 기존에는 Single 머신이었더면, 분산 머신을 쓸꺼임
The Motivation For Hadoop
	• 기존의 Large-Scale 컴퓨팅 시스템의 문제점을 해결 하기 위한 방안
	• 구글과 같이 대용량 데이터 처리를 처리하는 응용분야 출현
		○ 분산 컴퓨팅 이용(대형 컴퓨터를 쓰기엔 돈이;;;)
분산 처리 시스템
	• 해결 방법 : 더 많은 컴퓨터 사용
	• 진화
		○ 하나의 작업에 여러 대의 머신을 사용
		○ MPI(Message Passing Interface)를 이용하여 컴퓨터간에 메시지 수발신-> 프로그램 구조 복잡
		○ Partial failures : 수많은 컴퓨터를 사용하는 경우에 일부의 컴퓨터가 고장이 나는 경우 -> 성능저하가 유발됨
			§ 구글의 해결방안 : 복사본 3개를 분산 저장한다.
		○ 데이터 리커버리
			§ 시스템의 컴포넌트가 Fail 하더라도 시스템을 통해 작업은 지속적으로 수행 되어야함.
			§ Fail로 인해 어떠한 데이터 손실도 발생하면 안됨
			§ 시스템의 컴포넌트가 복구 되면 Rejoin이 가능 해야함
		○ Consistency
			§ 작업이 수행되는 동안 컴포넌트의 Fail은 결과에 영향을 주면 안됨
		○ Scalability
			§ 데이터 양이 증가하면, 각 작업의 성능이 감소함
			§ 시스템의 리소스가 증가 하면, 비례적으로 로드 Capacity가 증가
Hadoop의 역사
	• 하둡은 90년에서 20년 사이의 구글의 연구로 부터 시작
		○ GFS와 MapReduce를 강구해냄(비공개)
	• 기존 분산 컴퓨팅의 문제점을 해결할수 잇는 새로운 접근법
	• Core Concept : 초기 데이터를 시스템에 분산하여 저장
		○ 애플리케이션을 High-Level 코드로 작성
			§ 개발자에게 네트워크 프로그래밍, 의존성, Low-Level 지식이 요구 되지 않음
		○ 각 노드들은 가급적 통신에 대한 코드 작성이 필요 없음
		○ 데이터는 여러 노드에 미리 분산되어 저장
Hadoop : Very High Level Overview
	• 시스템이 데이터를 로드할 때 블럭으로 나누어짐
	• Map tasks(MapReduce 시스템의 첫 번째 파트)는 싱글 블록 단위로 작업 처리
	• 마스터 프로그램은 분산되어 저장된 데이터의 블럭에 대한 Map Task 작업을 각 노드에 할당
Fault Tolerance
	• Node가 Fail 한경우 Master Node는 Fail을 감지하고 작업을 다른 Node에 할당
	• Task 재 시작 하는 것은 다른 부분에 대한 작업을 수행중인 다른 Node와의 통신을 필요로 하지 않음.
	• Fail된 Node를 재시작하는 경우, 자동적으로 시스템에 연결 되어 새로운 task를 할당함.
	• 특정 Node의 성능이 매우 낮은 것으로 감지되면, Master Node는 같은 task를 다른 Node에 할당
		○ Sepeculative Execution


실습
	• Hue : 하둡의 에코 시스템으로서, 데이터 분석을 제공하는 웹 인터페이스
	
