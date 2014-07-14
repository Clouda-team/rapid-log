#rapidJS-log

通用的log工具.可以将log输出至stdout,stderr，目标文件或网络中的日志服务器中.

##Configure
	var conf = {
	    /**
	     * 日志级别, 由细到粗为
	     * 
	     * DEV:10 -> INFO:20 -> WARN:30 -> ERR:40 -> CRASH:50
	     * 
	     * default : INFO;
	     */
	    level : 'DEV',
	    /**
	     * 时间格式
	     * 
	     * TIMESTAMP ,ISO , GMT , UTC , LOCAL
	     */
	    formatDate : "LOCAL",
	    /**
	     * 一般性日志输出位置,
	     * default: 输出至stdout, 如果启动node时，配置了stdout，建议这里保持default.
	     * pathStr: 输出至目标文件
	     * "tcp://xxxxxxxxx" : 输出至目标tcp服务器,    暂未实现
	     * "http://xxxxxxxxx" : 输出至目标http服务器,  暂未实现
	     */
	    outputInfo : "default",
	    /**
	     * 错误性日志输出位置,
	     * default: 输出至stderr ， 如果启动node时，配置了stderr，建议这里保持default.
	     * pathStr: 输出至目标文件
	     * "tcp://xxxxxxxxx" : 输出至目标tcp服务器,    暂未实现
	     * "http://xxxxxxxxx" : 输出至目标http服务器,  暂未实现
	     */
	    outputErr : "default",
	    /**
	     * 自定义输出方法
	     * 
	     * lable : levelNubmer
	     * 
	     * levelNubmer > 0 , 日志级别.大于30将被输出至outputErr, 小于上面配置的level不被输出.
	     * lable 用户自定义的lable不转换大小写直接成生同名的日志方法.lable不能与默认的五个方
	     * 法同名(dev,info,warn,err,crash)，否则将被覆盖
	     */
	    customLevel:{
	        lab1:25,
	        lab2:55
	    },
	    
	    //  ------------- 以下配置暂未实现 ----------------- 
	    /**
	     * 文件分割
	     * false 不分割，
	     * 'LAUNCH' 每次启动 ,
	     * {number} 每number分钟分隔一个
	     */
	    splitLogBy : false, // 
	    
	    /**
	     * 是否将日志启动至另一个进程中.
	     */
	    fork : false,
	    
	    /**
	     * 启动为日志server  当启用为server时，fork配置不起作用..
	     * default : false,
	     * 
	     * {
	     *      port : number,
	     *      type : 'http' || 'tcp',
	     *      // 一个简单的验证字符串..防止服务被滥用
	     *      simpleToken : "XXXXX"     
	     * }
	     */
	    service: false
	}

##Demo
	var log = require("rapid-log")(conf);	//直接使用上面的configure

	// just use it. like the console.log;

	log.info("come and use rapid-log..");
	log.dev("this is devlog");
	log.warn("this is warn");
	log.err("this is errlog, msg : %s , code : %d ","message",100);
	log.crash("this is crashlog, msg : %s , code : %d ","message",100);
	
	// 自定义的日志方法
	log.lab1("lab1,lab1,lab1");
	log.lab2("lab1,lab1,lab1");