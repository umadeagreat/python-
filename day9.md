# 学习001：函数与模块
abs() #输出该数值的绝对值#
chr() #将Unicode转换为字符#
ord() #将字符转换为Unicode编码#
bin() #将整数转换为二进制字符串#
oct() #将整数转换为八进制字符串#
hex() #将整数转换为十六进制字符串#
pow() #进行幂运算#
round() #四舍五入取整数，可以指定保留小数点之后的位数#
# 学习002：关键词参数
1.若无特殊处理，默认函数中的参数全为位置参数(可按顺序调用参数，可不按顺序)，若希望用关键词= 参数命名，可在参数之前添加*（命名关键词参数）
2.位置参数：*args  关键词参数：**kwargs
3.*****位置参数（不带参数名的参数）必须出现在关键词参数（带有参数名的参数）之前，这两个参数的
# 学习003：高阶函数的用法
1.二元运算函数也可以在总函数定义时被赋予一个默认的函数运算
def calc(*args, init_values, op, **kwargs):

    result = init_values
    for arg in args:
        if type(arg) in (int, float):
            result = op(result, arg)
    for value in kwargs.values():
        if type(value) in (int, float):
            result = op(result, value) 
    return result


def add(x, y):
    return  x + y


def mul(x, y):
    return x * y

print(calc(1, 2, 3, init_value=0, op=add, x=4, y=5))  
print(calc(1, 2, x=3, y=4, z=5, init_values=1, op=mul)) #参数的位置可以跟设定时不一样，程序可以自动识别，赋给二元函数运算时不用加括号，加函数名称即可#

# 学习004：map和square函数：
def is_ou(number):
    return number % 2 == 0


def square(number):
    return number ** 2

number1 = [33, 56, 79, 68, 42, 21, 6, 3]
number2 = list(map(square, filter(is_ou, number1))) #map(所要使用的函数名称，所要处理的对象)：对后面的元素进行一一的函数映射；filter（条件，要被筛选的数列）：留下数列中符合条件的元素，条件是True or false，一般是根据bool值来判断#
print(number2)
采用生成法简化：number2 = list(number ** 2 for number in number1 if number % 2 == 0)
# 学习005：lambda函数：又称匿名函数，简单，只有一行代码
1.用lambda函数代替简单的is_ou函数和square函数
number2 = list(map(lambda x : x ** 2, filter(lambda x : x % 2 == 0,number1)))
2.用lambda函数、map函数生成is_prime函数，判断一个数是否为素数
is_prime = lambda x : x > 1 and all(map(lambda f : x % f, range(2, int(x ** 0.5) + 1))) #all函数代表如果所有的结果都为True则输出True#

# 学习006：装饰器函数
import random
import time


def download(filename):
    print(f"{filename}开始下载")
    time.sleep(random.randint(3, 6))
    print(f"{filename}下载完成")


def upload(filename):
    print(f"{filename}开始上传")
    time.sleep(random.randint(1, 4))
    print(f"{filename}上传完成")

def record_time(func): #参数为函数#
    def wrapper(*args, **kwargs):        ******#实际上真正进行运算的函数：参数为上一级参数的参数#
        start = time.time()
        result = func(*args, **kwargs)       ***************
        end = time.time()
        print(f"{func.__name__}完成所花费时间为{end - start}秒")   #func.__name__为一个属性，是函数的名称#
        return result   #函数必须有一个返回值#
    return wrapper

download = record_time(download) #用返回值覆盖原来的函数#
upload = record_time(upload)


download('MySQL从删库到跑路.avi')
upload('Python从入门到住院.pdf')
# 学习007：装饰器函数的语法糖功能以及删除功能
import random
import time
from functools import wraps


def record_time(func): #参数为函数#
    @wraps(func) #相当于赋予接下来的函数可删除功能#
    def wrapper(*args, **kwargs):    ******#实际上真正进行运算的函数：参数为上一级参数的参数#
        start = time.time()
        result = func(*args, **kwargs)
        end = time.time()
        print(f"{func.__name__}完成所花费时间为{end - start}秒") ******#func.__name__为一个属性，是函数的名称#
        return result #函数必须有一个返回值#
    return wrapper

@record_time
def download(filename):
    print(f"{filename}开始下载")
    time.sleep(random.randint(3, 6))
    print(f"{filename}下载完成")

@record_time
def upload(filename):
    print(f"{filename}开始上传")
    time.sleep(random.randint(1, 4))
    print(f"{filename}上传完成")

download('MySQL从删库到跑路.avi')
upload('Python从入门到住院.pdf')

download.__wrapped__('MySQL必知必会.pdf') #通过该属性删除函数的计时功能，即调用wraped的属性wrapped删除wrapper函数的运行#
upload = upload.__wrapped__
upload('Python从新手到大师.pdf')

# 学习008：函数的递归调用：


# 练习001：生成随机验证码
import random
import string


def yanzheng(code_len = 4):
    char = string.digits + string.ascii_letters #引用数字与字母#
    return "".join(random.choices(char,k=code_len))#join函数代表的是连接字符串#
    #random模块中的sample代表抽样不放回，choices代表抽样放回#
# 练习002：返回文件的类型
def back(filename,ignore_dot = True):
    index = filename.rfind(".")
    if index <= 0: #针对‘.’在0位和不存在（-1）的情况#
        return ""
    return filename[index + 1: ] if ignore_dot else filename[index:] #除以上情况之外都应直接输出，只是因为是生成式语法，所以需要添加else，实际else内容无意义#
    
# 练习003：判断一个所给的数是否为质数：
def is_zhishu(number):
    zhishu = True
    for i in range(2, number):
        if number % i == 0:
            zhishu = False
    return zhishu
    
 # 练习004：写出计算两个正整数最大公约数和最小公倍数的函数
def maxandmin(m,n):
    if m <= n:
        m , n = n , m
    for i in range(m, 0, -1):
        if m % i == 0 and n % i == 0:
            minimum = m * n / i
            return f"{i}为最大公约数，{minimum}为最小公倍数"
  
 # 练习005：写出计算一组样本数据描述性统计信息的函数
import math
def statistics(data):
    def distance(data): #极差#
        return max(data) - min(data)
        
    def average(data): #平均数#
        return sum(data) /len(data)

    def variation(data):#方差#
        sums = 0
        for i in data:
            sums += sum((i - average(data)) ** 2) / (len(data) - 1)
        return sums

    def s(data): #标准差#
        s = math.sqrt(variation(data))

    def median(data): #中位数#
        order,number = sorted(data), len(data)
        if number % 2 != 0:
            return order[number // 2]
        else:
            return average(order[number//2 - 1 : number//2 + 1])
 # 练习006：采用递归和循环的方法生成斐波那契数：
 递归的方法：
 def fib(n):
    if n in (1, 2):
        return 1
    return fib(n-1) + fib (n-2) #其实本质还是从1开始加，栈道，如果不懂的话可以去看可视化程序过程#

for i in range(1, 21):
    print(fib(i)) #但是执行步骤太多，从可视化程序来看已经突破1000#
    
循环的方法：
def fib(n):
    a, b = 0, 1
    for _ in range(n):
        a, b = b, a + b
        print(a)

 
