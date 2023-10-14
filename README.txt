如何编译Nginx1.25.2 + OPENSSL 3.1.3 +GMSSL 3.0.2
开始配置环境:
	1.安装VS 2017社区版
		1.1 选中windows - VC++ 生成工具；
		1.2 右侧菜单选中以下内容
			Windows10 SK
			用于Cmake的生成工具
			用于x86 和 x64的VC++ ALT
			用于x86 和 x64的VC++ MFC
			用于C++/CLI
			标准库模块（实验性）
		1.3右下角选 全部下载后安装 确定Y ；等待安装完成即可；安装过程中怎么配置其他环境
		
	2.安装 ActivePerl_v5.28.1.0000.exe
		2.1 本程序可以自行下载；也可以到我的代码库/集成工具文件夹/进行下载；
		2.2 下载dmake，我的代码库/集成工具文件夹/进行下载，然后解压到Perl根目录
			主要因为ActivePerl没有自带dmake组件，编译环境需要用到dmake
		2.3 打开cmd.exe 运行 cpanm -g install cpanminus  和 cpanm console::win32
			如果遇到找不到 make 则运行 cpan o conf nmake 回车;输入commit回车;然后再次尝试
			
	3.安装 MSYS2/MSYS 本程序可以自行下载；也可以到我的代码库/集成工具文件夹/msys2.rar进行下载；
		3.1 本程序用于生成makefile文件，后续用得到，必须安装;
	
	4.下载cmake 本程序可以自行下载；也可以到我的代码库/集成工具文件夹/Cmake进行下载；
		
		4.1 下载nasm-2.07；本程序可以自行下载；也可以到我的代码库/集成工具文件夹/nasm-2.07进行下载；
	
	5.配置环境变量
		5.1 我的电脑-高级系统设置-环境变量-系统环境变量；
		
		5.2 找到Path 打开，增加C:\Users\28299\Desktop\nasm-2.07  和 C:\Users\28299\Desktop\cmake\bin
			这个路径自行设置按照实际情况修改进行配置;

	6.下载nginx所需的类库
		6.1 openssl-3.1.3.tar.gz 本程序可以自行下载；也可以到我的代码库/集成工具文件夹/nasm-2.07进行下载；
		
		6.2 pcre-8.45.zip 本程序可以自行下载；也可以到我的代码库/集成工具文件夹/nasm-2.07进行下载；
		
		6.3 zlib-1.2.0.1.tar.gz 本程序可以自行下载；也可以到我的代码库/集成工具文件夹/nasm-2.07进行下载；
		
		6.4 解压上述3个文件到nginx1.25.2源码目录下objs/lib/文件夹中，截止到2023年10月14日，这三个文件是版本最新的；
			没有目录就自行创建目录
	
	7.下载GMSSL 到这里 https://gitee.com/mirrors/GmSSL 下载，下载完成后解压到源码目录下objs/lib/文件夹中
	
	
:: 第一步打开MSYS2/MSYS；
::1.切换到源码目录
cd /c/users/28299/Desktop/nginx-release-1.25.2
::2.运行这串命令 在objs文件夹中生成makefile
auto/configure     --with-cc=cl     --with-debug     --prefix=     --conf-path=conf/nginx.conf     --pid-path=logs/nginx.pid     --http-log-path=logs/access.log     --error-log-path=logs/error.log     --sbin-path=nginx.exe     --http-client-body-temp-path=temp/client_body_temp     --http-proxy-temp-path=temp/proxy_temp     --http-fastcgi-temp-path=temp/fastcgi_temp     --http-scgi-temp-path=temp/scgi_temp     --http-uwsgi-temp-path=temp/uwsgi_temp     --with-cc-opt=-DFD_SETSIZE=1024     --with-pcre=objs/lib/pcre2-10.39     --with-zlib=objs/lib/zlib-1.2.11     --with-openssl=objs/lib/openssl-3.1.3     --with-openssl-opt=no-asm --with-http_v2_module --with-http_realip_module --with-http_addition_module --with-http_sub_module --with-http_dav_module --with-http_stub_status_module --with-http_flv_module --with-http_mp4_module --with-http_gunzip_module --with-http_gzip_static_module --with-http_auth_request_module --with-http_random_index_module --with-http_secure_link_module --with-http_slice_module --with-mail --with-stream --with-stream_realip_module --with-stream_ssl_preread_module --with-openssl=objs/lib/openssl-3.1.3 --with-openssl-opt='no-asm no-tests -D_WIN32_WINNT=0x0501' --with-http_ssl_module --with-mail_ssl_module --with-stream_ssl_module
::这串命令展开如下所示:
auto/configure \
    --with-cc=cl \
    --with-debug \
    --prefix= \
    --conf-path=conf/nginx.conf \
    --pid-path=logs/nginx.pid \
    --http-log-path=logs/access.log \
    --error-log-path=logs/error.log \
    --sbin-path=nginx.exe \
    --http-client-body-temp-path=temp/client_body_temp \
    --http-proxy-temp-path=temp/proxy_temp \
    --http-fastcgi-temp-path=temp/fastcgi_temp \
    --http-scgi-temp-path=temp/scgi_temp \
    --http-uwsgi-temp-path=temp/uwsgi_temp \
    --with-cc-opt=-DFD_SETSIZE=1024 \
    --with-pcre=objs/lib/pcre2-10.39 \
    --with-zlib=objs/lib/zlib-1.2.11 \
    --with-openssl=objs/lib/openssl-3.1.3 \
    --with-openssl-opt=no-asm \
    --with-gmssl=objs/lib/gmssl \
    --with-gmssl-opt=no-asm \
	--with-http_v2_module \
	--with-http_realip_module \
	--with-http_addition_module \
	--with-http_sub_module \
	--with-http_dav_module \
	--with-http_stub_status_module \
	--with-http_flv_module \
	--with-http_mp4_module \
	--with-http_gunzip_module \
	--with-http_gzip_static_module \
	--with-http_auth_request_module \
	--with-http_random_index_module \
	--with-http_secure_link_module \
	--with-http_slice_module \
	--with-mail --with-stream \
	--with-stream_realip_module \
	--with-stream_ssl_preread_module \
	--with-openssl=objs/lib/openssl-3.1.3 \
	--with-openssl-opt='no-asm no-tests -D_WIN32_WINNT=0x0501' \
	--with-http_ssl_module \
	--with-mail_ssl_module \
	--with-stream_ssl_module
	
	
	::第二部找到VS2017中 打开适用于 VS 2017 的 x64 本机工具命令提示.cmd；
	
	::1.切换到源码目录
	cd C:\Users\28299\Desktop\nginx-release-1.25.2
	::2开始构建
	
	nmake -f objs/makefile
	
	
	如果没有遇到错误将会编译成功：等待40分钟左右编译完成，objs文件夹下会生成nginx.exe
	
	
	本文参考文章 https://blog.csdn.net/zccoften/article/details/130700218
			   https://gitee.com/mirrors/GmSSL
			   https://www.gmssl.cn/gmssl/index.jsp
			   https://www.baidu.com/首页上方的的AI整合编写
																
																2023年10月14日 17：33