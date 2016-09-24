# pureftpd-mysql-auth-config
pureftpd 通过mysql认证


# 编译

	wget  http://download.pureftpd.org/pub/pure-ftpd/releases/pure-ftpd-1.0.37.tar.bz2

	./configure --prefix=/usr/local/pureftpd CFLAGS=-O2 \
	--with-mysql \
	--with-altlog \
	--with-cookie \
	--with-diraliases \
	--with-ftpwho \
	--with-paranoidmsg \
	--with-peruserlimits \
	--with-quotas \
	--with-ratios \
	--with-sysquotas \
	--with-throttling \
	--with-virtualchroot \
	--with-virtualhosts \
	--with-welcomemsg  --without-sendfile

#创建用户

	mkdir -p /var/ftp
	userdel ftp
	groupdel ftp
	usermod -u 2000 -g ftp -s /sbin/nologin -d /var/ftp ftp  
	usermod -u 2000 -g ftp -s /sbin/nologin -d /var/ftp ftp  





# sql 

	CREATE DATABASE pureftpd;
	grant all on pureftpd.* to pureftpd@'%' identified by 'pureftpd';
	FLUSH PRIVILEGES;
	use pureftpd;
	CREATE TABLE `users` (
	  `User` char(32) NOT NULL DEFAULT '',
	  `Password` char(32) CHARACTER SET utf8 COLLATE utf8_bin NOT NULL DEFAULT '',
	  `Dir` varchar(128) NOT NULL DEFAULT '',
	  `Status` enum('0','1') NOT NULL DEFAULT '1',
	  PRIMARY KEY (`User`),
	  UNIQUE KEY `User` (`User`)
	) ENGINE=MyISAM DEFAULT CHARSET=utf8;
	
	
	
#启动pureftpd

/usr/local/pureftpd/sbin/pure-config.pl /usr/local/pureftpd/etc/pureftpd.conf  &



