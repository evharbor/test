#				�ο��ĵ�


## 1.��������
	master ip��10.XX.XX.87
	client ip:10.XX.XX.225-239



## 2.�ֱ�ͨ��master��client�������ܵ�½
### ���岽�����£�
       	1����masterִ�� ssh-keygen -t rsa ���������Կ�ļ�
	2��masterִ��ssh-copy-id -i ~/.ssh/id_rsa.pub dss@10.XX.XX.225-239���ֱ�ִ�У�����Կ�ļ����䵽client��
	3��ִ����Ч�鿴.ssh�ļ��Ƿ����µĹ�Կ����



## 3.�����ļ���ͬ��ϵͳ
	1����master���ļ��Զ����ϴ���client��
	2������client�����б�/updata��
	3��ִ���Զ����ű���remmotecopy.sh�����˽ű�����  client IP�б�    �����ļ�Ŀ¼     client�洢Ŀ¼
		eg��sh remotecopy.sh -f /updata/hosts /root/API_upload1.py /root/API_upload2.py
	4���ű�ִ������Զ��رգ�ȷ��ͬ���ɹ�	
```
#!/bin/bash
while getopts f: OPT;
do
	case $OPT in
		f|+f)
			files="$OPTARG $files"
			;;
		*)
			echo "usage: `basename $0` [-f hostfile] <from> <to>"
			exit 2
	esac
done
shift `expr $OPTIND - 1`
 
if [ "" = "$files" ];
then
	echo "usage: `basename $0` [-f hostfile] <from> <to>"
	exit
fi
 
for file in $files
do
	if [ ! -f "$file" ];
	then
		echo "no hostlist file:$file"
		exit
fi
hosts="$hosts `cat $file`"
done
 
for host in $hosts;
do
	echo "do $host"
	scp $1 root@$host:$2
done
```


## 4.��������ִ��linuxϵͳ����ϵͳ
	1��master����client����ִ��master��Ҫִ�е�������
	2������client�����б�/updata��
	3��ִ���Զ����ű���doCommand.sh���˽ű�����ΪҪִ�е�����Ҫ�á� ������ס
		eg�� sh doCommand.sh 'python36 API_upload2.py >/dev/null 2>&1 &'
		�����м�����Ҫ�������� /dev/null 2>&1 &,Ŀ�����ڽ����صĲ�������linux��ʱ�洢�Ŀռ��Դﵽ����ִ�������Ŀ�ģ�������ִ��ʱ�䣩
```
#!/bin/sh

doCommand()
{
    hosts=`sed -n '/^[^#]/p' hostlist`
    for host in $hosts
        do
            echo ""
            echo HOST $host
            ssh $host "$@"
        done
    return 0
}

    if [ $# -lt 1 ]
    then
            echo "$0 cmd"
            exit
    fi
    doCommand "$@"
    echo "return from doCommand"

```


ע�������ļ��ű��ڱ�����ļ����¡�







