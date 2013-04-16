1、区分大小写
2、变量要声明
3、函数可以用函数名.arguments.length来获得参数数量
4、支持try catch
5、基于对象而不是面向对象
6、var d = new Date(99,10,1)99年10月1日，getTime()获得毫秒数
7、parseInt，parseFloat，toString，escape，unescape
8、eval()执行语句
9、模拟对象
function student(name){
	this.name = name
	this.getName = getName;
}

function getName(){
	return this.name
}

var s = new student("palo")
util.puts(s.getName());
10、给基础对象添加属性，所有new出来的都有，并且修改new出来的对象不会影响别的new出来的对象
student.prototype.foodgroup = "carbohydrates"

11、with (Math) {  
x = cos(3 * PI) + sin(LN10); 	
  y = tan(14 * E);	
}

12、navigator
appCodeName;IE,Mozilla
language
platform
plugin

screen
availHeight
availWidth
colorDepth
height
width

windows
name
satus
self
top
parent
open
fullscreen

location
href
port
host
protocol
pathname

history
current
length
next
previous

back()
forward()
go()
document