# 第20课：python标准库初探
## 1.base-Base64编解码模块
content = "content"
base64.b64encode(contend.enconde()) #content内容变为base64编码模式#
base64.64decode(content).decode #content内容变为正常模式#
----------------------------------------------------------------
## 2.collections-容器数据类型模块：
(1)namedtuple:接受类型的名称和属性列表来创建一个类
Card = namedtuple('Card', ('suite', 'face'))
card1 = Card('红桃', 5)
print(card1) #Card(suite='红桃', face=5)#
print(f'{card1.suite}{card1.face}') #红桃5#

(2)counter-统计列表中出现次数最多的元素：
from collections import Counter

words = [
    'look', 'into', 'my', 'eyes', 'look', 'into', 'my', 'eyes',
    'the', 'eyes', 'the', 'eyes', 'the', 'eyes', 'not', 'around',
    'the', 'eyes', "don't", 'look', 'around', 'the', 'eyes',
    'look', 'into', 'my', 'eyes', "you're", 'under'
]
counter = Counter(words) #Counter中的内容是一个字典，键是元素名称，键值是该元素出现的次数#
# 打印words列表中出现频率最高的3个元素及其出现次数
for elem, count in counter.most_common(3): #若括号内为空，则统计的是每一个元素与其出现的次数#
    print(elem, count)
    
## 3.hashlib - 哈希函数模块：哈希函数把数据压缩成摘要，对于相同的输入，哈希函数可以生成相同的摘要
--------------------------------------------------------------------------------------------------
## 4.heapq-堆排序模块：
import heapq

list1 = [34, 25, 12, 99, 87, 63, 58, 78, 88, 92]
print(heapq.nlargest(3, list1)) #找出列表中最大的三个元素，个数在前，对象在后#
print(heapq.nsmallest(3, list1)) #找出列表中最小的三个元素，个数在前，对象在后 #

list2 = [
    {'name': 'IBM', 'shares': 100, 'price': 91.1},
    {'name': 'AAPL', 'shares': 50, 'price': 543.22},
    {'name': 'FB', 'shares': 200, 'price': 21.09},
    {'name': 'HPQ', 'shares': 35, 'price': 31.75},
    {'name': 'YHOO', 'shares': 45, 'price': 16.35},
    {'name': 'ACME', 'shares': 75, 'price': 115.65}
]
#找出价格最高的三只股票#
print(heapq.nlargest(3, list2, key=lambda x:x["price"])) #list2是一个由字典构成的列表，key提供了作为关键词的键名，需要比较的就是其所对应的键值#
#找出持有数量最高的三只股票#
print(heapq.nlargest(3, list2, key=lambda x: x['shares']))
-----------------------------------------------------------------------------
## 5.itertools - 迭代工具模块
import itertools

for value in itertools.permutations('ABCD'):#产生ABCD的全排列:A44,有24种，按顺序
    print(value)

for value in itertools.combinations('ABCDE', 3):#产生ABCDE的五选三组合:C53，有10种，不按顺序
    print(value)

# 产生ABCD和123的笛卡尔积
for value in itertools.product('ABCD', '123'): #笛卡尔积：前后两个元素各自循环对应#
    print(value)

# 产生ABC的无限循环序列
it = itertools.cycle(('A', 'B', 'C')) #通过next函数将intertools.cycle函数中的每个元素都循环#
print(next(it))
print(next(it))
print(next(it))
print(next(it))
-------------------------------------------------------------------------------
## 6.random-随机数和随机抽样模块：
radiant(a, b) #随机返回一个整数n，使得a<=n<=b;相当于randrange(a, b+1)#
random() #括号为空，默认范围[0, 1)之间的随机浮点数#
choice(seq)
choices(polulation, weight= None, *, cum_weights = None, k = 1) #随机放回抽样，population是总体，k为所抽取的样本个数#
sample(population,k) #同上#
shuffle(x[, random]) #将x这个序列随机打乱位置：洗牌#
expovariate(lambda) #指数分布#
gammavariate(alpha, beta) #伽马分布#
gaussvariate(mu, sigma) = normalvariate(mu, sigma)#高斯分布，又称正态分布#
paretovariate(alpha)#帕累托分布#
weibullvariate(alpha, beta) #威布尔分布#
-----------------------------------------------------------------------------------
## 8 os.path-路径操作相关模块
--------------------------------------------------------------------------------
## 9 uuid-UUID生成模块
------------------------------------------------------------------------------
# 第21课：文件读写和异常处理
## 1. 读写文本文件：（要先将文件导入到pycharm中，拖拽）
读：
file = open('致橡树.txt', 'r', encoding='utf-8') #保证所要打开的文件与encoding编码一直才能顺利打开#
print(file.read())
file.close()

file = open('致橡树.txt', 'r',encoding="utf-8") #逐行读取#
for line in file:
    print(line,end="")
file.close()

file = open('致橡树.txt', 'r', encoding='utf-8') #将文件按行读取到一个列表容器中#
lines = file.readlines()
for line in lines:
    print(line,end='')
file.close()
写：#这里的改变可作用于原来桌面上的txt文件#
file = open('致橡树.txt', 'w', encoding='utf-8') #w是清空之前的文本，重新写入文本##a是在原来文本的尾部添加新的内容#
file.write("\n标题：致橡树")
file.write("\n作者：舒婷")
file.write("\n时间：1977年3月")
file.close()
----------------------------------------------------------------------------------
## 2 异常处理机制：


① try/except组合：

file = None
try: #通过此步骤来查看可能出现的异常类型#
    file = open('致橡树.txt', 'r', encoding='utf-8')
    print(file.read())
except FileNotFoundError: #该文件不在pycharm中#
    print('无法打开指定的文件!')
except LookupError: #encoding编码未知#
    print('指定了未知的编码!')
except UnicodeDecodeError:
    print('读取文件时解码错误!')
finally: #无论是否异常都会执行此步骤，目的是为了关闭文件节省外部资源#
    if file:
        file.close()
 （注：except是用于捕获可能出现的异常并对其进行处理）
 
 
 
② 使用raise关键字来引发异常，采用try/except处理异常:
 class Inputerror(ValueError): #自定义异常类型#
    pass

def fac(num):
    if num < 0:
        raise Inputerror("只能计算非负整数的阶乘") #引发异常#
    if num in (0, 1):
        return 1
    return num * fac(num - 1)

flag = True
while flag:
    n = int(input("n = ")) #必须在循环内部，否则会一直循环#
    try: #try/except捕捉并处理异常#
        print(f"{n}! = {fac(n)}")
        flag = False
    except Inputerror as err:
        print(err)


③ 上下文语法： #with是一种上下文语法，作用是替代finally，使得代码更加简单，但条件是必须符合上下文管理器协议#
try:
    with open('致橡树.txt', 'r', encoding='utf-8') as file:
        print(file.read())
except FileNotFoundError:
    print('无法打开指定的文件!')
except LookupError:
    print('指定了未知的编码!')
except UnicodeDecodeError:
    print('读取文件时解码错误!')

④ 读写二进制文件：#这种操作也能在pycharm中生成实际的电脑文件##也是需要被打开的文件必须在pycharm中#
try:
    with open('guido.jpg', 'rb') as file1: #rb读二进制文件#
        data = file1.read()
    with open('吉多.jpg', 'wb') as file2: #创建一个jpg文件，wb写入二进制文件#
        file2.write(data) #打开file2，并把file1的内容复制到file2#
except FileNotFoundError:
    print('指定的文件无法打开.')
except IOError:
    print('读写文件时出现错误.')
print('程序执行结束.')
------------------------------------------------------------------------------
# 第22课：对象的序列化与反序列化：
## 1.json数据类型与python的对应：
python json
dict - object
list/tuple - array
str - string
int/float - number
bool - boolean
None - null
## 2.读写json格式的数据:
json模块的四个重要函数：
dump：将python对象序列化到一个新的json文件中
dumps:将python对象处理为json格式的字符串
load:将json格式的数据反序列化为对象
------------------------------
①dump函数与dumps函数的使用：

import json

my_dict = {
    'name': '骆昊',
    'age': 40,
    'friends': ['王大锤', '白元芳'], #此为一个列表#
    'cars': [
        {'brand': 'BMW', 'max_speed': 240},
        {'brand': 'Audi', 'max_speed': 280},
        {'brand': 'Benz', 'max_speed': 280}
    ] #此为一个列表，列表里面是字典#
}
print(json.dumps(my_dict)) #中文字符都用Unicode编码显示，英文和数字与原来一样#
with open("data.json","w") as file: #"w"是代表写入#
    json.dump(my_dict, file) #创建一个json文件，其中写入的内容与dumps函数得到的编码是一样的#

②load函数的使用：
import json
with open("data.json","r") as file: #"r"代表采用读的模式#
    my_dict = json.load(file) #将json数据反序列化，还原成python中的字典#
    print(type(my_dict)) #类型是一个字典#
    print(my_dict) #输出字典#
--------------------------------------------
# 3.使用网络api获取数据：本例使用的是天行数据，需要先申请接口，然后到控制台选择调试，获取自己的key密钥
import requests

resp = requests.get('http://api.tianapi.com/woman/index?key=fece5fdd1c19a153da274ab137e1d653&num=10')#通过get函数向新闻接口发起请求，key=API即自己申请的接口密钥，num为所需要得到的新闻数量#
if resp.status_code == 200: #若该属性值即status_code是2开头的值，则请求成功#
    data_model = resp.json() #通过json方法将resp处理为python中的字典#
    for news in data_model["newslist"]:#将newslist看作键名，title和url为键值#
        print(news['title']) #新闻的标题#
        print(news['url']) #新闻的来源地址#
        print('-' * 60) #将每条新闻隔开#

