#  ���ݿ�

## ��������
���ݿ��Ǳ�ģʽ������أ���־���洢��ͱ�ռ������Ч�ش������ݿ�����ļ��ϡ�

![](http://www.yiibai.com/uploads/allimg/141215/091I54530-0.png)

## ��������

### �г���ǰʵ�����õ����ݿ�Ŀ¼�б�

�﷨:

	db2 list db directory 


### �������ݿ�

�﷨:

	db2 create db <db_name>
 
ʾ����

	db2 create db newdb

�����

	DB20000I  CREATE DATABASE ����ɹ���ɡ�
	
���Բ鿴����ǰ���ݿ��Ŀ¼

```
D:\Program Files\IBM\SQLLIB\BIN>db2 list db directory

 ϵͳ���ݿ�Ŀ¼

 Ŀ¼�е���Ŀ�� = 1

���ݿ� 1 ��Ŀ��

 ���ݿ����                      = NEWDB
 ���ݿ�����                               = NEWDB
 �������ݿ�Ŀ¼                  = D:
 ���ݿⷢ�а漶��                = 10.00
 ע��                            =
 Ŀ¼��Ŀ����                    = ���
 Ŀ¼���ݿ������                  = 0
 ���÷�����������                =
 ���÷������˿ں�                =
```

### ɾ�����ݿ�

�﷨��

	db2 drop db <db_name>
	
### �������ݿ�

���������������б�Ҫ�ķ���Ϊ�ض������ݿ⣬���������ݿ��ǿ��õ�Ӧ�ó���

�﷨:

	db2 activate db <db_name> 
	
ʾ��: 

	db2 activate db newdb  
	
### ͣ�����ݿ�

ʹ�ô��������ֹͣ���ݿ����

�﷨:

	db2 deactivate db <db_name>
	
ʾ��: 

	db2 deactivate db newdb
	
### ���ӵ����ݿ�

����һ�����ݿ⣬����Ͷ��ʹ�ú���Ҫ���ӻ��������ݿ⡣

�﷨:

	db2 connect to <database name> 
	
ʾ��: 

	db2 connect to newdb 

�����

```
D:\Program Files\IBM\SQLLIB\BIN>db2 connect to newdb

   ���ݿ�������Ϣ

 ���ݿ������         = DB2/NT64 10.5.5
 SQL ��Ȩ��ʶ         = ADMIN
 �������ݿ����       = NEWDB
```

## ���û���������Զ�����ӵ����ݿ�

�﷨��

	db2 connect to <db_name> user <userid> using <password>   

ʾ����

	db2 connect to newdb user db2admin using 123abc   

�����

```
D:\Program Files\IBM\SQLLIB\BIN>db2 connect to newdb user db2admin using 123abc


   ���ݿ�������Ϣ

 ���ݿ������         = DB2/NT64 10.5.5
 SQL ��Ȩ��ʶ         = DB2ADMIN
 �������ݿ����       = NEWDB
```

## ��֤���ݿ��Ȩ��

�﷨��

```
db2 "select substr(authority,1,25) as authority, d_user, d_group, d_public, role_user, role_group, role_public,d_role from table( sysproc.auth_list_authorities_for_authid ('public','g'))as t order by authority"  
```
   