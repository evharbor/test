#				�ο��ĵ�
## 1.master ip��10.XX.XX.87
	client ip:10.XX.XX.225-239


## 2.�ֱ�ͨ��master��client�������ܵ�½
###       	 ���岽�����£�
###        	1����masterִ�� ssh-keygen -t rsa ���������Կ�ļ�
###	2��masterִ��ssh-copy-id -i ~/.ssh/id_rsa.pub dss@10.XX.XX.225-239���ֱ�ִ�У�����Կ�ļ����䵽client��
###	3��ִ����Ч�鿴.ssh�ļ��Ƿ����µĹ�Կ����


## 3.�����ļ���ͬ��ϵͳ
###	1����master���ļ��Զ����ϴ���client��
###	2������client�����б�/updata��
###	3��ִ���Զ����ű���remmotecopy.sh�����˽ű�����  client IP�б�    �����ļ�Ŀ¼     client�洢Ŀ¼
####		eg��sh remotecopy.sh -f /updata/hosts /root/API_upload1.py /root/API_upload2.py
###	4���ű�ִ������Զ��رգ�ȷ��ͬ���ɹ�	


## 4.��������ִ��linuxϵͳ����ϵͳ
###	1��master����client����ִ��master��Ҫִ�е�������
###	2������client�����б�/updata��
###	3��ִ���Զ����ű���doCommand.sh���˽ű�����ΪҪִ�е�����Ҫ�á� ������ס
####		eg�� sh doCommand.sh 'python36 API_upload2.py >/dev/null 2>&1 &'
####		�����м�����Ҫ�������� /dev/null 2>&1 &,Ŀ�����ڽ����صĲ�������linux��ʱ�洢�Ŀռ��Դﵽ����ִ�������Ŀ�ģ�������ִ��ʱ�䣩



ע�������ļ��ű��ڱ�����ļ����¡�







