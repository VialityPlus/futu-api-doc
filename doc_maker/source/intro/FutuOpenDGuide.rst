=================
FutuOpenD使用说明
=================

 .. _set_handler: ../api/Quote_API.html#set-handler


基本介绍
----------

  FutuOpenD是futu-api的网关程序，运行于客户本机或服务器，负责中转协议请求到富途后台，并将处理后的数据返回给协议请求连接。
 
  FutuOpenD目前提供两种安装执行形式，用户可根据自身需求选择任一方式。
  
  1. 命令行形式：提供命令行执行程序，需自行进行部分配置，适合熟悉度高或无界面化需求的用户； 
  
  2. 可视化形式：提供界面化应用程序，操作便捷，尤其适合入门用户。 
  
----------------------------


下载安装
----------

命令行FutuOpenD
~~~~~~~~~~~~~~~~~~~~
  * 命令行FutuOpenD目前直接提供程序压缩包，解压后即可运行。 
  
  
  * 压缩包内除了各平台的执行程序，还有带有默认FutuOpenD配置文件（FutuOpenD.xml），程序打包数据（Appdata.dat）。
  
  
  * Appdata.dat是程序需要用到的一些数据量较大的信息，打包数据减少启动下载该数据用时，若不存在则程序无法正常启动。
  
  
  * FutuOpenD.xml 用于配置FutuOpenD程序启动参数，若不存在则程序无法正常启动，支持用户自定义文件路径， 详见 `启动命令行参数 <./FutuOpenDGuide.html#id10>`_

可视化FutuOpenD  
~~~~~~~~~~~~~~~~~~
  * 可视化OpenD提供程序安装包，可一键安装运行，
  
  * Windows安装在%appdata%目录下。
  
  * 下载方式同命令行FutuOpenD。

方式1：`富途官网下载 <https://www.futunn.com/download/index/>`_ 

.. image:: ../_static/futunn.com.png


方式2：QQ群文件下载

.. image:: ../_static/download-QQ.png

--------------

登录参数使用优先级
----------------
  1.命令行证书登录
  
  2.命令行帐号密码密文登录
  
  3.命令行帐号密码明文登录
  
  4.配置文件证书登录
  
  5.配置文件帐号密码密文登录
  
  6.配置文件帐号密码明文登录

----------------------------
  
FutuOpenD配置
--------------

命令行FutuOpenD
~~~~~~~~~~~~~~~~~~~~
  * 命令行FutuOpenD启动配置文件使用XML格式，如下图所示：

  .. image:: ../_static/FTOpenDConfig.png

  **配置项：**
  
  ========================   =============================================================================================================================================================   ================================================
  键值                       说明                                                                                                 是否可选配置项
  ========================   =============================================================================================================================================================   ================================================
  ip                         监听地址                                                                                                                                                        是，不设置则默认127.0.0.1    
  api_port                   API协议接收端口                                                                                                                                                 是，可以命令行指定
  push_proto_type            API协议支持PB以及Json格式，PB：0，Json：1，推送类协议通过该配置决定包体格式                                                                                     是，不设置则默认PB格式
  qot_push_frequency         API订阅数据推送频率控制，单位毫秒，目前不包括K线和分时                                                                                                          是，不设置则不限制频率
  rsa_private_key            API协议RSA加密私钥（PKCS#1）文件绝对路径                                                                                                                        是，不设置则协议不加密
  telnet_ip                  远程操作命令监听地址                                                                                                                                            是，不设置则默认127.0.0.1    
  telnet_port                远程操作命令监听端口                                                                                                                                            是，不设置则不启用远程命令
  login_account              登录帐号                                                                                                                                                        是，可以使用证书登录或命令行输入
  login_pwd                  登录密码明文                                                                                                                                                    是，可以使用密文、证书登录或命令行输入
  login_pwd_md5              登录密码密文（32位MD5加密16进制），密文明文都存在情况下，只使用密文                                                                                             是，可以使用明文、证书登录或命令行输入
  log_level                  日志级别，可填no(无日志)，debug(最详细)，info(次详细)，warning，error，fatal                                                                                    是，默认info级别
  simulate_trade             是否启用模拟交易，关闭模拟交易可节省少量资源使用，可填enable，disable                                                                                           是，默认启用
  websocket_ip               API协议监听地址，可选127.0.0.1（监听来自本地的连接）以及0.0.0.0（监听来自所有网卡的连接）                                                                       是，不设置则默认127.0.0.1 
  websocket_port             WebSocket服务监听端口                                                                                                                                           是，不设置则不启用该功能  
  websocket_private_key      WebSocket证书私钥文件路径，私钥不可设置密码，不配置则不启用SSL，需要和证书同时配置                                                                              是，不设置则不启用SSL
  websocket_cert             WebSocket证书文件路径，不配置则不启用SSL，需要和私钥同时配置                                                                                                    是，不设置则不启用SSL
  websocket_key_md5          密钥密文（32位MD5加密16进制），用于JS接口连接时用于判断是否可信连接                                                                                             是，不设置则不做验证
  price_reminder_push        是否接收到价提醒推送，0：不接收，1：接收（需在脚本中设置回调函数 set_handler_ )                                                                                 是，默认会推送
  auto_hold_quote_right      被踢后是否自动抢权限？0：否，1：是，开启该选项时，OpenD在行情权限被抢后，会自动抢回。如果10秒内再次被抢，则其他终端获得最高行情权限（OpenD不会再抢）            是，默认会自动抢权限
  ========================   =============================================================================================================================================================   ================================================

可视化FutuOpenD  
~~~~~~~~~~~~~~~~~~ 
  * 可视化FutuOpenD配置以界面化表单形式展现，代替命令行版本的XML配置文件方式。
    
  .. image:: ../_static/UIConfig.png
  
  **配置项说明如下表所示：**
  
  ====================   =================================================================================================================
  配置项                 说明                                                                               
  ====================   =================================================================================================================
  监听地址               API协议监听地址，可选127.0.0.1（监听来自本地的连接）以及0.0.0.0（监听来自所有网卡的连接），或填本机某个网卡地址
  监听端口               API协议监听端口
  日志级别               FutuOpenD日志级别
  API推送频率            API订阅数据推送频率控制，单位毫秒，目前不包括K线和分时
  Telnet地址             远程操作命令监听地址
  Telnet端口             远程操作命令监听端口
  加密私钥路径           API协议RSA加密私钥（PKCS#1）文件绝对路径
  WebSocket监听地址      API协议监听地址，可选127.0.0.1（监听来自本地的连接）以及0.0.0.0（监听来自所有网卡的连接）
  WebSocket端口          WebSocket服务监听端口
  WebSocket证书          WebSocket证书文件路径，不配置则不启用SSL，需要和私钥同时配置
  WebSocket私钥          WebSocket证书私钥文件路径，私钥不可设置密码，不配置则不启用SSL，需要和证书同时配置
  WebSocket鉴权密钥      密钥密文（32位MD5加密16进制），用于JS接口连接时用于判断是否可信连接
  ====================   =================================================================================================================
  
.. note::    
  * 可视化FutuOpenD通过启动命令行OpenD来提供服务， 且通过Websocket与命令行OpenD交互，所以必定启动Websocket功能。
  
  * 当API监听地址不是本地，使用交易接口需配置私钥。
  
  * 当WebSocket监听地址不是本地，需配置SSL才可以启动，且证书私钥生成不可设置密码。
  
  * 密文是明文经过32位MD5加密后用16进制表示的数据，搜索在线MD5加密（注意，通过第三方网站计算可能有记录撞库的风险）或下载MD5计算工具可计算得到。
  
  32位MD5密文如下图红框区域（e10adc3949ba59abbe56e057f20f883e）：
  
  .. image:: ../_static/MD5.png

  * FutuOpenD默认读取同目录下的FutuOpenD.xml。在MacOS上，由于系统保护机制，FutuOpenD.app在运行时会被分配一个随机路径，导致无法找到原本的路径。此时有以下方法：

  1. 执行tar包下的fixrun.sh
  2. 用命令行参数-cfg_file指定配置文件路径，见下面说明


启动命令行参数
---------------

  命令行部分参数与配置文件相同，同样参数若存在于命令行与配置文件，使用命令行参数。
  
  .. image:: ../_static/login-command.png
  
  传参格式：-key=value
  
  例如FutuOpenD.exe -login_account=100000 -login_pwd=123456 -lang=en

  
  **参数项：**
  
  ========================   =====================================================================================================================================================   ================================================
  键值                       说明                                                                                                                                                    是否可选配置项
  ========================   =====================================================================================================================================================   ================================================
  login_account              登录帐号                                                                                                                                                是，可以使用证书登录或配置文件配置项
  login_pwd                  登录密码明文                                                                                                                                            是，可以使用证书登录或配置文件配置项
  login_pwd_md5              登录密码密文（32位MD5加密16进制），密文明文都存在情况下，只使用密文                                                                                     是，可以使用密文、证书登录或配置文件配置项
  login_by_remember          记住密码登录，需要搭配帐号使用，当该参数存在，忽略密码参数                                                                                              是，可以使用帐号密码登录或命令行输入
  remember                   记住密码，当该参数不设置时，已记住密码的帐号继续记住，需要取消记住密码，需要明确传入-remember=0                                                         是，不设置保留当前帐号的记住密码状态
  login_region               优先连接点区域，但不一定能连接上该区域连接点(gz/sh/hk)                                                                                                  是，不设置则自动选择
  cfg_file                   FutuOpenD配置文件绝对路径                                                                                                                               是，不设置则使用程序所在目录下的FutuOpenD.xml
  console                    是否显示控制台，后台运行：0，控制台运行：1                                                                                                              是，不设置则默认控制台运行
  lang                       FutuOpenD语言，en：英文，chs：简体中文                                                                                                                  是，不设置则默认简体中文
  api_ip                     API服务监听地址                                                                                                                                         是，不设置则默认127.0.0.1   
  api_port                   API协议接收端口                                                                                                                                         是，不设置则使用配置文件配置项
  help                       输出启动命令行参数然后退出程序                                                                                                                          是，不设置则正常启动FutuOpenD
  log_level                  日志级别，可填no(无日志)，debug(最详细)，info(次详细)，warning，error，fatal                                                                            是，默认info级别
  no_monitor                 是否启动守护进程，启动：0，不启动：1                                                                                                                    是，默认带守护进程启动
  simulate_trade             是否启用模拟交易，关闭模拟交易可节省少量资源使用，可填enable，disable                                                                                   是，默认启用
  websocket_ip               WebSocket服务监听地址，可选127.0.0.1（监听来自本地的连接）以及0.0.0.0（监听来自所有网卡的连接）                                                         是，不设置则默认127.0.0.1    
  websocket_port             WebSocket服务监听端口                                                                                                                                   是，不设置则不启用该功能
  websocket_private_key      WebSocket证书私钥文件路径，不配置则不启用SSL，需要和证书同时配置                                                                                        是，不设置则不启用SSL
  websocket_cert             WebSocket证书文件路径，不配置则不启用SSL，需要和私钥同时配置                                                                                            是，不设置则不启用SSL
  websocket_key_md5          密钥密文（32位MD5加密16进制），用于JS接口连接时用于判断是否可信连接                                                                                     是，不设置则不做验证
  price_reminder_push        是否接收到价提醒推送，0：不接收，1：接收（需在脚本中设置回调函数 set_handler_ )                                                                         是，默认会推送
  auto_hold_quote_right      被踢后是否自动抢权限？0：否，1：是，开启该选项时，OpenD在行情权限被抢后，会自动抢回。如果10秒内再次被抢，则其他终端获得最高行情权限（OpenD不会再抢）    是，默认会自动抢权限
  ========================   =====================================================================================================================================================   ================================================

--------------

运维命令
--------------
  
  通过命令行或者Telent发送命令可以对FutuOpenD做运维操作。
  
  命令格式：**cmd -param_key1=param_value1 -param_key2=param_value2**
  
----------------------------  
  
help - 命令帮助
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

  help -cmd=exit

  查看指定命令详细信息，不指定参数则输出命令列表

  **Paramters cmd:** str，命令
  
.. note::

    * 运维代码在Telnet窗口或命令控制台输入
    .. image:: ../_static/req-verify.png

  
exit - 退出程序
~~~~~~~~~~~~~~~~

  exit 

  退出FutuOpenD程序


req_phone_verify_code - 请求手机验证码
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

  req_phone_verify_code 

  请求手机验证码，当启用设备锁并初次在该设备登录，要求做安全验证。
  
input_phone_verify_code - 输入手机验证码
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

  input_phone_verify_code -code=123456

  输入手机验证码，并继续登录流程。

  **Parameters: code** - str，手机验证码
 
req_pic_verify_code - 请求图形验证码
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

  req_pic_verify_code 

  请求图形验证码，当多次输入错登录密码时，需要输入图形验证码。
  
input_pic_verify_code - 输入图形验证码
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

  input_pic_verify_code -code=1234

  输入图形验证码，并继续登录流程。

  **Paramters: code** - str，图形验证码
  
relogin - 重登录
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

  relogin -login_pwd=123456

  当登录密码修改或中途打开设备锁等情况，要求用户重新登录时，可以使用该命令。只能重登当前帐号，不支持切换帐号。
  密码参数主要用于登录密码修改的情况，不指定密码则使用启动时登录密码。

  **Paramters: login_pwd** - str，登录密码明文
  
  **Paramters: login_pwd_md5** - str，登录密码密文（32位MD5加密16进制）
  
ping - 检测与连接点之间的时延
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

  ping 

  检测与连接点之前的时延
  
show_delay_report - 展示延迟统计报告
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

  show_delay_report -detail_report_path=D:/detail.txt -push_count_type=sr2cs 

  展示延迟统计报告，包括推送延迟，请求延迟以及下单延迟。每日北京时间6:00清理数据。 
  
  **Paramters: detail_report_path** - str，文件输出路径（MAC系统仅支持绝对路径，不支持相对路径），可选参数，若不指定则输出到控制台
  
  **Paramters: push_count_type** -  str，推送延迟的类型(sr2ss，ss2cr，cr2cs，ss2cs，sr2cs)，默认sr2cs，sr指服务器接收时间(目前只有港股支持该时间)，ss指服务器发出时间，cr指OpenD接收时间，cs指OpenD发出时间

close_api_conn - 关闭API连接
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

  close_api_conn  -conn_id=123456

  关闭某条API连接，若不指定则关闭所有
  
  **Paramters: conn_id** - uint64，API连接ID

show_sub_info - 展示订阅状态
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

  show_sub_info -conn_id=123456 -sub_info_path=D:/detail.txt

  展示某条连接的订阅状态，若不指定则展示所有
  
  **Paramters: conn_id** - uint64，API连接ID
  
  **Paramters: sub_info_path** - str，文件输出路径（MAC系统仅支持绝对路径，不支持相对路径），可选参数，若不指定则输出到控制台
  
request_highest_quote_right - 请求最高行情权限
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

  request_highest_quote_right 

  当高级行情权限被其他设备（如：桌面端/手机端）占用时，可使用该命令重新请求最高行情权限（届时，其他处于登录状态的设备将无法使用高级行情）。
  
  
---------------------------- 

WebSocket相关
--------------

证书使用
~~~~~~~~~~~~~~
   
  为保证安全，当websocket监听来自非本地请求时，需要启用SSL并配置连接密钥。
   
  SSL通过在配置证书以及对应的私钥来启用，命令行FutuOpenD可通过XML或命令行参数设置文件路径。
  
  界面FutuOpenD点击【更多选项】可以看到对应设置项。
  
  .. image:: ../_static/MoreConfig.png
  
  .. note::
     
   * 如果证书是自签的，则需要在调用JS接口所在机器上安装该证书，或者设置不验证证书。
   
生成自签证书
~~~~~~~~~~~~~~
  
  自签证书生成详细资料不便在此文档展开，请自行查阅。

  在此提供较简单可用的生成步骤：
  
  1. 安装openssl
  
  2. 修改openssl.cnf，在alt_names节点下加上FutuOpenD所在机器IP地址或域名;如 IP.2 = xxx.xxx.xxx.xxx, DNS.2 = www.xxx.com
  
  3. 生成私钥以及证书（PEM）。
  
  证书生成参数参考如下：
    ```
    openssl req -x509 -newkey rsa:2048 -out futu.cer -outform PEM -keyout futu.key -days 10000 -verbose -config openssl.cnf -nodes -sha256 -subj "/CN=Futu CA" -reqexts v3_req -extensions v3_req
    ```

  附上本地自签证书以及生成证书的配置文件供测试： `openssl.cnf <../_static/file/openssl.cnf>`_  |  `futu.cer <../_static/file/cer>`_  | `futu.key <../_static/file/key>`_  
  
  .. note::

    * openssl.cnf需要放到系统路径下，或在生成参数中指定绝对路径。
    * 注意生成私钥需要指定不设置密码（-nodes）。
    
---------------------------- 

补充说明
--------------
 
日志级别
~~~~~~~~~~~~~~
  默认info级别，在系统开发阶段建议不要关闭日志或者将日志修改到info以上（warning，error，fatal），避免出现问题无法确认以及定位问题。
  
  
问卷评估及协议确认
~~~~~~~~~~~~~~~~~~~~~
  需要进行相关问卷评估及协议确认，才可以使用FutuOpenD，请先 `前往完成 <https://www.futunn.com/about/api-disclaimer/>`_ 。

----------------------------
  
RSA私钥文件
~~~~~~~~~~~~~~
  
 参考文件格式：
  
 .. code-block:: bash

    -----BEGIN RSA PRIVATE KEY-----
    MIICXAIBAAKBgQCx3W78hx5dQxg47hGMEj02JAJYP+HdKGWD8QilzeK4eL6QJ9QP
    +uVYGA5Jp0Ed2AaV+zQrT/BCe6z5j/Qd5B0eY2cFlgk+/hbAt7A4wcSAbby8nONw
    0fZTglU78FhLUih84Int5HO0Fr3WLUDvpE+TgS3l/2u5ym6H6fvsdrdNCwIDAQAB
    AoGAHep/s2vKmKcjWNf6DZQ3xXZzCoLcK4WS5YlSCglCHAL7EmYQjguGLbYGGS9P
    jYR7Pxi8YpiUcao5otQqnCh1GRFouU397D3h+bf/bQXINZcv3sxKFrXm9MNVaBJD
    W4BcC3HGfnlaIVTKU+qGkeA1BydP5AQyxsGOq00IUeGK4uECQQD/5xHLDwhwYFyc
    MK4xMnlrvne8TSlPBciWfrxQ7V/X0eP/HQ20VkVxc0tFD91aLrCap6OYcNV9jwJN
    wTQLt5wbAkEAse7C75LKW0+cMcROvAR3qLV2LbGjLW+cH6WmEP9CEGxi0aJg4Gs3
    oSRYfaC/RLI87sSb0DC5+mTswXduLGpB0QJAJk0ec6cHW1KA6fu7Rq/ITqEOaMef
    xC0YbbYAV5h/vNy0ZE2j7HbxI97eyDJsrf/I/QzURo+01HsgHCUrtglAOwJBAKiW
    cA7sh1zS5kxlErCkjvfDz1BmIhT3zfZSTjGGmYLUHyE/eAjKra+5rzqA5xjgxEj6
    8iLlOCFeJND+Jt5gYzECQH+HtFilF1SxGS4AHrJomHaMhk/IazjtUnLuFM/DuZ/h
    sxTqXpBBCtTqcAotMlx4ZJQYL3f2PmI2Q/o0NUMt40w=
    -----END RSA PRIVATE KEY-----
    
 .. note::

  * RSA 密钥的填充方式为 PKCS1， 位数1024
  * 密钥文件可通过第三方web平台自动生成， 请在baidu或google上搜索"RSA 在线生成"
  * 将私钥保存成文件，并在将文件路径配置在FutuOpenD.xml的rsa_private_key配置项
  * 公钥可通过私钥计算得到，但生成私钥时不要设置密码
  * 该密钥需要在OpenD配置文件中指定，且API接口也需要调用相关接口设置密钥信息
  
---------------


    
    
    
