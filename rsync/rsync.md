����̨�������䱸������


1������
?wget https://download.samba.org/pub/rsync/src/rsync-3.1.2.tar.gz
?tar -zxvf rsync-3.1.2.tar.gz

2����װ
cd rsync-3.1.2
./configure --prefix=/usr/local/rsync
make
make install

3������rsyncd.conf
vim /usr/local/rsync/rsyncd.conf?


rsyncd.conf ���������£�


### ȫ�ֲ��� ###
port=8730 # ��Ĭ�϶˿���873���������8730�ˡ�
motd file=/usr/local/rsync/rsyncd.motd
log file=/usr/local/rsync/rsyncd.log
pid file=/var/run/rsyncd.pid


### ģ����� ###
[testmodule]
path=/root/test
use chroot=true
uid=0
gid=0
read only=false
exclude=/readme.txt /runtime

#auth users����û���������������ϵͳ�в����ڵ��û���
auth users=mazhenwei
secrets file = /usr/local/rsync/rsyncd.secrets

4������rsyncd.secrets

vim /usr/local/rsync/rsyncd.secrets

rsyncd.secrets�����ݵ��﷨Ϊ �û���:��¼����

����
mazhenwei:123

# rsyncd.secrets�ļ�Ȩ�ޱ�������Ϊ600
chmod 600 /usr/local/rsync/rsyncd.secrets


5������rsyncd.motd
vim /usr/local/rsync/rsyncd.motd


rsyncd.motd�����ݾ�����
welcome use rsync service !


6������rsync����
/usr/local/rsync/bin/rsync --daemon --config=/usr/local/rsync/rsyncd.conf


7������rsync����������

vi /etc/rc.local

��ĩβ����??/usr/local/rsync/bin/rsync --daemon --config=/usr/local/rsync/rsyncd.conf

����Ŀ¼/root/test/�µ����ݸ�b��

/usr/local/rsync/bin/rsync --port=8730 -av /root/test/ ?mazhenwei@10.0.87.2::testmodule --password-file=/root/mazhenwei.pass

��ȡb�����ݵ�����/root/test/Ŀ¼��

/usr/local/rsync/bin/rsync --port=8730 -av mazhenwei@10.0.87.21::testmodule ?/root/test/ ?--password-file=/root/mazhenwei.pass  ##�����pass�ļ�ҲҪchmod  600
