
### Dev Tools
> Web Site
* Markdown Web Editor : https://stackedit.io/app



개발
	우분투 명령어 
		https://delirussum.tistory.com/76

	텔레그래프(telegraf)
		튜토리얼 : https://techexpert.tips/ko/influxdb-ko/ubuntu-linux%EC%97%90-telegraf-%EC%84%A4%EC%B9%98/
		
	오픈 JDK 설치
		http://programmingskills.net/archives/702
	
	엘라스틱서치(elasticsearch)
		https://webisfree.com/2018-11-24/elasticsearch-%EC%97%98%EB%9D%BC%EC%8A%A4%ED%8B%B1%EC%84%9C%EC%B9%98-ubuntu-%ED%99%98%EA%B2%BD-%EC%84%A4%EC%B9%98%EB%B0%A9%EB%B2%95
		
		다운로드 페이지 : https://www.elastic.co/kr/downloads/elasticsearch
		다운로드 
			wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.4.2-amd64.deb
		설치
			dpkg -i elasticsearch-7.4.2-amd64.deb
			
		시작 
			service elasticsearch start
		
		localhost:9200
		
	키바나 설치
		https://blo-gu.tistory.com/12
		
		다운로드 페이지 : https://www.elastic.co/kr/downloads/kibana
		다운로드 
			wget https://artifacts.elastic.co/downloads/kibana/kibana-7.4.2-amd64.deb
		설치 
			dpkg -i kibana-7.4.2-amd64.deb
		
		시작 
			service kibana start
		
		localhost:5601
	
	텔레그래프 설정 변경
		vi /etc/telegraf/telegraf.conf
		기존 파일명 변경 : mv 원본파일명 변경파일명
		
		실행
		## telegraf -config /etc/telegraf/telegraf.conf
		
		systemctl start telegraf.service
		systemctl stop telegraf.service
		systemctl restart telegraf.service
		
		
	그라파나(grafana) 설치
		다운로드 및 : https://grafana.com/grafana/download
		
		wget https://dl.grafana.com/oss/release/grafana_6.4.4_amd64.deb
		sudo dpkg -i grafana_6.4.4_amd64.deb
		
		# systemctl start grafana-server
		# systemctl status grafana-server
		
		ID, PW : admin/admin
		
elastic search 외부에서 접속해 보려고 하자 접속이 안됨.

방화벽을 열어도 되지 않아 elasticsearch 에서 외부접속을 막는것으로 판단

find / -name elasticsearch.yml 에 정보를 수정하라는 글을 봄
	https://override1592.tistory.com/24
수정하고 재시작을 해야 하는데 재시작이 되지 않음

	이런글도 봄  https://okayjava.tistory.com/30

이런 오류가 남
Job for elasticsearch.service failed because the control process exited with error code.
See "systemctl status elasticsearch.service" and "journalctl -xe" for details.

상태 체크
service elasticsearch status

해결방법!!
https://discuss.elastic.co/t/problems-with-access-to-elasticsearch-form-outside-machine/172450/2



내 방화벽 포트 열어주기 
219.251.113.39

ufw allow from 219.251.113.39 to any port 9200 proto tcp
ufw allow from 219.251.113.39 to any port 5601 proto tcp
ufw allow from 219.251.113.39 to any port 3000 proto tcp



# find [경로] -name [파일명] 명령어를 사용한다.



입력한 경로를 포함해서 하위 경로에 있는 모든 파일을 검색해 조건에 맞는 파일이나 디렉토리를 찾아준다.



최상위 디렉토리 아래에 있는 모든 경로에서 'test' 라는 이름을 가진 파일이나 디렉토리를 검색해보자.



# find / -name test
