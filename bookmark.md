
### Dev Tools
> Web Site
* Markdown Web Editor : https://stackedit.io/app



����
	����� ��ɾ� 
		https://delirussum.tistory.com/76

	�ڷ��׷���(telegraf)
		Ʃ�丮�� : https://techexpert.tips/ko/influxdb-ko/ubuntu-linux%EC%97%90-telegraf-%EC%84%A4%EC%B9%98/
		
	���� JDK ��ġ
		http://programmingskills.net/archives/702
	
	����ƽ��ġ(elasticsearch)
		https://webisfree.com/2018-11-24/elasticsearch-%EC%97%98%EB%9D%BC%EC%8A%A4%ED%8B%B1%EC%84%9C%EC%B9%98-ubuntu-%ED%99%98%EA%B2%BD-%EC%84%A4%EC%B9%98%EB%B0%A9%EB%B2%95
		
		�ٿ�ε� ������ : https://www.elastic.co/kr/downloads/elasticsearch
		�ٿ�ε� 
			wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.4.2-amd64.deb
		��ġ
			dpkg -i elasticsearch-7.4.2-amd64.deb
			
		���� 
			service elasticsearch start
		
		localhost:9200
		
	Ű�ٳ� ��ġ
		https://blo-gu.tistory.com/12
		
		�ٿ�ε� ������ : https://www.elastic.co/kr/downloads/kibana
		�ٿ�ε� 
			wget https://artifacts.elastic.co/downloads/kibana/kibana-7.4.2-amd64.deb
		��ġ 
			dpkg -i kibana-7.4.2-amd64.deb
		
		���� 
			service kibana start
		
		localhost:5601
	
	�ڷ��׷��� ���� ����
		vi /etc/telegraf/telegraf.conf
		���� ���ϸ� ���� : mv �������ϸ� �������ϸ�
		
		����
		## telegraf -config /etc/telegraf/telegraf.conf
		
		systemctl start telegraf.service
		systemctl stop telegraf.service
		systemctl restart telegraf.service
		
		
	�׶��ĳ�(grafana) ��ġ
		�ٿ�ε� �� : https://grafana.com/grafana/download
		
		wget https://dl.grafana.com/oss/release/grafana_6.4.4_amd64.deb
		sudo dpkg -i grafana_6.4.4_amd64.deb
		
		# systemctl start grafana-server
		# systemctl status grafana-server
		
		ID, PW : admin/admin
		
elastic search �ܺο��� ������ ������ ���� ������ �ȵ�.

��ȭ���� ��� ���� �ʾ� elasticsearch ���� �ܺ������� ���°����� �Ǵ�

find / -name elasticsearch.yml �� ������ �����϶�� ���� ��
	https://override1592.tistory.com/24
�����ϰ� ������� �ؾ� �ϴµ� ������� ���� ����

	�̷��۵� ��  https://okayjava.tistory.com/30

�̷� ������ ��
Job for elasticsearch.service failed because the control process exited with error code.
See "systemctl status elasticsearch.service" and "journalctl -xe" for details.

���� üũ
service elasticsearch status

�ذ���!!
https://discuss.elastic.co/t/problems-with-access-to-elasticsearch-form-outside-machine/172450/2



�� ��ȭ�� ��Ʈ �����ֱ� 
219.251.113.39

ufw allow from 219.251.113.39 to any port 9200 proto tcp
ufw allow from 219.251.113.39 to any port 5601 proto tcp
ufw allow from 219.251.113.39 to any port 3000 proto tcp



# find [���] -name [���ϸ�] ��ɾ ����Ѵ�.



�Է��� ��θ� �����ؼ� ���� ��ο� �ִ� ��� ������ �˻��� ���ǿ� �´� �����̳� ���丮�� ã���ش�.



�ֻ��� ���丮 �Ʒ��� �ִ� ��� ��ο��� 'test' ��� �̸��� ���� �����̳� ���丮�� �˻��غ���.



# find / -name test
