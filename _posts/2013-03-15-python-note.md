dump
dir
vars
isinstance
type
issubclass
callable
getattr
__bases__
eval
eval("_ _import_ _('os').getcwd()",{__builtins__})
compile
exec
execfile

os.listdir
os.getcwd 
os.chdir
makedirs
removedirs

mkdir 和 rmdir 函数只能处理单个目录级
stat文件属性st_size,st_mtime,st_ctime
time.ctime(st_mtime)
chmod

os.name

import os
if os.name == "nt":
	command ="dir" 
else:
	command = "ls -l"
os.system(command)

program = "python"
arguments = ["hello.py"]
os.execvp(program, (program,) + tuple(arguments))

os.path.split(filename)
os.path.splitext(filename)
os.path.basename(filename)
os.path.dirname(filename)
os.path.join(os.path.dirname(filename),os.path.basename(filename))
os.path.exists(filename)
os.path.isfile(filename)
os.path.isdir(filename)
os.path.ismount(filename)
os.path.islink(filename)

os.environ["USER"] = "user"
print os.path.expandvars("/home/$USER/config")
print os.path.expandvars("$USER/folders")

//遍历
def callback(arg, directory, files):
for file in files:
print os.path.join(directory, file), repr(arg)
os.path.walk(".", callback, "secret message")

int("4545")

m=re.match(pattern,str)
m=re.search(pattern,str)
re.sub(pattern,substr,str)//替换子串
print m.group(0,1,2,3)

text = "a line of text\\012another line of text\\012etc..."
def octal(match):
# replace octal code with corresponding ASCII character
# 使用对应 ASCII 字符替换八进制代码
return chr(string.atoi(match.group(1), 8))
octal_pattern = re.compile(r"\\(\d\d\d)")
print text
print octal_pattern.sub(octal, text)


import operator
reduce(operator.add,[1,2,3,4,5])
operator.getitem(sequence, 2)
operator.indexOf(sequence, 2)

operator.sequenceIncludes(sequence, 3)

copy(object) => object 创建给定对象的 "浅/浅层(shallow)" 拷贝(copy).
这里 "浅/浅层(shallow)" 的意思是复制对象本身, 但当对象是一个容器
(container) 时, 它的成员仍然指向原来的成员对象.

copy.copy()
copy.deepcopy()

sys.argv[0]脚本执行参数
sys.path
sys.builtin_module_names内建模块
sys.modules.keys()已导入模块
sys.getrefcount(0)获得引用计数

sys.platform == "win32":"mac"

def profiler(frame, event, arg):
print event, frame.f_code.co_name, frame.f_lineno, "->", arg
sys.setprofile(profiler)
sys.setprofile(None)
sys.settrace(tracer)
sys.exit(1)抛异常退出

def exitfunc():
	print "world"
sys.exitfunc = exitfunc，退出异常的处理函数

注册多个异常退出函数
atexit.register(exit)
atexit.register(exit, 1)
atexit.register(exit, "hello", "world")

time.time()当前时间数字
time.localtime()字典
print time.gmtime(time.time())[:6]
print time.asctime(now)
print time.strftime("%y/%m/%d %H:%M", now)转字符串

print strptime("31 Nov 00", "%d %b %y")转时间结构体（平台依赖）

time.mktime(tm)结构体转数字

time.sleep(2.5)
time.clock()

t0 = time.time()
procedure()真实时间消耗
print time.time() - t0, "seconds wall time"

type(object) is types.IntType

gc.collect
del root
程序不会创建自引用数据时可以禁用gc.disable

for line in fileinput.input("samples/sample.txt"):
fileinput.isfirstline()
fileinput.filename()
fileinput.lineno()

if line[-2:] == "\r\n":
line = line[:-2] + "\n"

shutil.copy
shutil.copytree

tempfile.mktemp()快速创建名称唯一的临时文件
用完要用os.remove(tempfile)
file = open(tempfile, "w+b")
file.write("*" * 1000)
file.seek(0)
print len(file.read()), "bytes"
file.close()

tempfile.TemporaryFile()创建并打开文件
调file.close() 文件就被删除了


stdout = sys.stdout
sys.stdout = file = StringIO.StringIO()
重定向输出到stringio
print file.getvalue()

try:
	import cStringIO更快
	StringIO = cStringIO
except ImportError:
	import StringIO

os.path.getsize(filename)

mmap操作系统内存映射函数
file = open(filename, "r+")
size = os.path.getsize(filename)
data = mmap.mmap(file.fileno(), size)
repr(data[:10])
repr(data.read(10))
data.find("small")
repr(data[index-5:index+15])

捕获异常后打印堆栈
traceback.print_exc()

fp = StringIO.StringIO()
traceback.print_exc(file=fp)
message = fp.getvalue()

def function():
	raise IOError, "an i/o error occurred"
try:
	function()
except:
	info = sys.exc_info()
	for file, lineno, function, text in traceback.extract_tb(info[2]):
		print file, "line", lineno, "in", function
		print "=>", repr(text)
	print "** %s: %s" % info[:2]


errno使用
try:
	fp = open("no.such.file")
except IOError, (error, message):
	if error == errno.ENOENT:
		print "no such file"
	elif error == errno.EPERM:
		print "permission denied"
	else:
		print message

try:
	fp = open("no.such.file")
except IOError, (error, message):
	print error, repr(message)
	print errno.errorcode[error]

sys.argv = ["myscript.py", "--echo", "--printer", "lp01", "message"]
opts, args = getopt.getopt(sys.argv[1:], "ep:", ["echo", "printer="])

usr = getpass.getuser()
pwd = getpass.getpass("enter password for user %s: " % usr)

glob(pattern)返回满足模式的文件列表，返回的是完整路径
for file in glob.glob("samples/*.jpg"):
	print file

fnmatch.fnmatch(file, "*.jpg"):匹配文件类型
pattern = fnmatch.translate("*.jpg")转成正则表达式

random.randint(100, 1000)包括上界
不包括上界
random.random()
random.uniform(10, 20)
random.randrange(100, 1000, 2)

random.choice([1, 2, 3, 5, 9])
a=[1, 2, 3, 5, 9]
random.shuffle(a)//a里的顺序被打乱了

hash = md5.new()
hash.update("spam, spam, and eggs")
print hash.digest()2进制
print hash.hexdigest()16进制
base64.encodestring(hash.digest()) base64编码

千万别忘记内建的伪随机生成器对于加密操作而言并不合适. 千万小心.

compressed_message = zlib.compress(MESSAGE,zlib.Z_BEST_COMPRESSION)
decompressed_message = zlib.decompress(compressed_message)

encoder = zlib.compressobj()
data = encoder.compress("life")
data = data + encoder.flush()


code 模块提供了一些用于模拟标准交互解释器行为的函数.
compile_command 与内建 compile 函数行为相似, 但它会通过测试来保证你传
递的是一个完成的 Python 语句.

co = code.compile_command(script, "<stdin>", "exec")
exec co

//再打开个控制台，感觉没啥大用，可以当断点手动打印环境变量用
console = code.InteractiveConsole()
console.interact()

threading.Thread类
self.lock = threading.Lock()锁
self.lock.acquire()加锁
self.lock.release()释放
thread类需实现def run(self):
thread类开始
Worker().start()

Queue 模块提供了一个线程安全的队列 (queue) 实现

优先级队列
class PriorityQueue(Queue.Queue):
	"Thread-safe priority queue"
	def _put(self, item):
	# insert in order
		bisect.insort(self.queue, item)

import popen2, string
fin, fout = popen2.popen2("sort")
fout.write("foo\n")
fout.write("bar\n")
fout.close()
print fin.readline(),
print fin.readline(),
fin.close()


marshal 和 pickle 模块用于在不同的 Python 程序间共享/传递数据.
cPickle更快，因为用c写的

pprint 模块几乎可以将任何 Python 数据结构很好地打印出来(提高可读性).
repr 模块可以用来替换内建同名函数. 该模块与内建函数不同的是它限制了很
多输出形式: 他只会输出字符串的前 30 个字符,

判断字节顺序
ord(array.array("i",[1]).tostring()[0])==1为intel，小端
或者用sys.byteorder判断是little还是big

struct.pack("ihb", 1, 2, 3)
struct.unpack("ihb", buffer)

data = [1, 2, 3]
buffer = apply(struct.pack, ("!ihb",) + tuple(data))或buffer = struct.pack("!ihb", *data)
struct.unpack("!ihb", buffer)

数据
import marshal
value = (
"this is a string",
[1, 2, 3, 4],
("more tuples", 1.0, 2.3, 4.5),
"this is yet another string"
)
data = marshal.dumps(value)

代码
code = compile(script, "<script>", "exec")
data = marshal.dumps(code)
exec marshal.loads(data)

pickle可以处理类但不能处理code

pickle.dumps(value, 1)binary模式，内存占用更小

copy_reg 模块注册你自己的扩展类型. 这样 pickle 和 copy 模
块就会知道如何处理非标准类型.

def code_unpickler(data):
return marshal.loads(data)
def code_pickler(code):
return code_unpickler, (marshal.dumps(code),)
copy_reg.pickle(types.CodeType, code_pickler, code_unpickler)

pprint打印的整齐

# note: this overrides the built-in 'repr' function
from repr import repr
# an annoyingly recursive data structure
data = (
"X" * 100000,
)
data = [data]
data.append(data)
print repr(data)

formatter 和 writer . formatter 将 HTML 解析器的标签和数
据流转换为适合输出设备的事件流( event stream ), 而 writer 将事件流输出
到设备

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.connect((HOST, PORT))
t = s.recv(4)
s.close()


service = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
service.bind(("", PORT))
service.listen(1)
channel, info = service.accept()
t = struct.pack("!I", t)
channel.send(t)
channel.close()

udp
s = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
# send empty packet
s.sendto("", (HOST, PORT))
t, server = s.recvfrom(4)
t = struct.unpack("!I", t)[0]
s.close()


service = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
service.bind(("", PORT))
data, client = service.recvfrom(0)
t = struct.pack("!I", t)
service.sendto(t, client)


is_readable = [service]
is_writable = []
is_error = []
r, w, e = select.select(is_readable, is_writable, is_error, 1.0)
if r:
channel, info = service.accept()
channel.send(t) # send timestamp
channel.close()


asyncore 模块提供了一个 "反馈性的( reactive )" socket 实现. 该模块允许
你定义特定过程完成后所执行的代码, 而不是创建 socket 对象
dispatcher 外, 这个模块还包含一个 dispatcher_with_send 类. 你可
以使用这个类发送大量的数据而不会阻塞网络通讯缓冲区.


print locale.getdefaultlocale()


import pstats
import profile
def func1():
for i in range(1000):
pass
def func2():
for i in range(1000):
func1()
p = profile.Profile()
p.run("func2()")
s = pstats.Stats(p)
s.sort_stats("time", "name").print_stats()