说明：
本工程是在原步兵工程上增删改出来的英雄工程
增：增加大量电机控制程序
删：自瞄、扭腰、拨盘等
改：控制方式

关于电机ID分配，有修改，请看《英雄车控制系统设计_v0.4》

命名说明：
PM ：PUSH MOTOR,即推弹电机
AM ：ARM MOTOR,	即机械臂电机，AM1L代表关节1左侧电机，AM1R代表关节1右侧电机，以此类推

底盘、云台、推弹电机的控制由Can1ControlTask完成
新增Can2ControlTask (在文件tasks_arm中),专门用于控制机械臂电机

操作方式：
发射：键鼠模式下同步兵，遥控器模式下从最高打到中间便会启动摩擦轮并开枪,发射已封装到函数shootOneGolf()中，调用一次推弹电机转一圈
运动：同步兵
取弹：遥控器控制模式下，左侧拨杆打到最低，取弹，打到最高，收回机械臂；键鼠模式下，由两个按键控制，控制函数是getGolf()和armReset()
	  取弹机械臂电机位置控制由setAMAngle(MotorId id, float angle)完成

新增的所有电机都是位置控制，默认减速比19，转子一圈编码数8192，控制方式是将其展开成直线，此时要仔细处理编码器上溢、下溢的问题（3000是随便给的）
每次上电启动后，机械臂电机、推弹电机都会将电机此时的角度设置为0°

待调参数：
	云台零点位置
	鼠标灵敏度
	所有的PID
	机械臂电机零点位置
	Pitch轴软件限位
	。。。
	太多了，不写了
	
	
