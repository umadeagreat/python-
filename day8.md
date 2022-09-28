# 学习001：掷骰子
import random

counters = [0] * 6 "创建列表"
for i in range(6000):
    face = random.randint(1, 6)
    counters[face - 1] += 1 "进行投掷，并且将结果计入列表"
for face in range(1, 7):
    print(f"{face}点出现了{counters[face - 1]}次") "输出结果"
# 学习002：列表相关函数
list.remove()
list.append()
list.insert()
list.sort()
list.reverse()
list.pop()
list.count()
list.index()
list.clear()
列表之间的比较是对应索引指数元素值的一一比较
注意生成式语法的使用
# 学习003：元组相关
当将多个逗号分隔的值赋给一个变量时，该变量自动成为一个元组
# 学习004：字符串的相关运算
1、可通过ord函数来获得字符串对应编码，字符串比较的也是字符一一对应的编码
（is运算符比较的是内存地址，逻辑运算符比较的是字符串中每个字符对应的编码）
2、字符串和元组一样，也是不可变类型
3、字符串相关函数：
s.capitalize()
s.upper()
s.lower()
s.title()
s.find() #返回的都是首字母的索引# s.rfind()
s.index() s.rindex() #前面加上r表逆向查找：相当于直接找到最后一次出现的位置#
s.startswith()
s.endswith()
s.isdigit() #是否只由数字构成#
s.isalpha() #是否只由字母构成#
s.isalnum() #是否由字母和数字构成#
s.center(宽度，"")# 将字符串居中
s.rjust(宽度，) #将字符串右对齐
s.ljust(宽度，)#将字符串左对齐
s.zfill(len(s)) #在字符串左侧补零
s.strip() #修剪左右两端空格及字符串
s.replace()
s.split("",4) #以“”隔开为基准，将字符串拆分为单词，后面为要使用的拆分符号个数#
"%".join(s.split()) #用前面的符号连接字符串#
a.encode("")
b.decode()表示编码和解码，其中编码和解码对应的类型应为同一类型
注意字符串占位符的使用：>10d表示在左边补位，<10d表示在右边补位，10代表所要补位的位数
# 学习005 集合的相关运算：
一、生成的集合是无序的，因此不能再用指数索引的方法去找到对应的元素；
集合本身不能作为集合中的元素（因为是可变的，比如顺序不确定），而不可变类型为hashable类型，可作为集合元素
二、相关函数：
取交集：
set1 & set2
set1.intersection(set2)
取并集：
set1 | set2
set1.union(set2)
取差集：
set1- set2
set1.difference(set2)
取对称差集，即不含交集的并集：
set1 ^ set2
set1.symmetric_difference(set2)
集合的比较运算：
< 真子集
<= 子集
set1.issubset(set2) set1是否为set2的子集
set2.issuperset(set1)set2是否为set1的超集
三、集合的方法：
set.add() #添加一个数
set.update() #括号内是一个集合
set.discard()#删除指定元素
set.remove() #此法建议先做成员运算确定是否在集合内，再删除，否则返回错误
set.pop() #随机删除集合内某一个元素
set.clear() #清空集合
set1.isdisjoint(set2) #判断两个集合是否没有相同元素，没有则返回True
# 学习006：字典
注：1、字典中的键必须是不可变类型，字典本身是可变类型，可以作为字典的值
一、创建字典的两种方法：
** xinhua = dict(x1=?,x2=?.....)
** xinhua = {"x1":x1,"x2":x2....}
xinhua = dict(zip("abc","123"))，用zip函数进行一一对应
xinhua = {x:x ** 3 for x in range (1:5)}，用生成式语法创建字典
二、字典的相关运算：
len(person) #输出的是键的个数，对字典中的元素进行for循环输出的是键的名称"
person["tel"] = 1808033921 #这种步骤可以直接修改字典中键对应的值，也可以增加不存在的键对
三、字典的方法：
dic.get() #对于存在的键，即获得对应的值；对于不存在的键，则是往字典中添加括号中的键和值#
dic.keys() #获得字典中所有的键#
dic.values() #获得字典中所有的值#
dic.items() #获得字典中所有的键值对#
dic.pop(1002),#删除该键值对并返回该值#
dic.pop("",{})#删除一个不存在的键值对，返回花括弧里的内容，没什么意义#
dic.popitem()#删除字典最后一组键值对并返回对应的键值对#
dic.setdefault()#往字典中添加键值对的一种方法#
dic.update(others)#将others这个字典添加到dic字典中#
# 练习001：输入一段话，统计每个英文字母出现的次数。
sentence = input("请输入一句话")
count = {}
for ch in sentence:
    if "a" <= ch.lower() <= "z":
        count[ch] = count.get(ch, 0) + 1

for keys, values in count.items():
    print(f"{keys} 出现了 {values}次")
# 练习002：在一个字典中保存了股票的代码和价格，找出股价大于100元的股票并创建一个新的字典
stocks = {
    'AAPL': 191.88,
    'GOOG': 1186.96,
    'IBM': 149.24,
    'ORCL': 48.44,
    'ACN': 166.89,
    'FB': 208.09,
    'SYMC': 21.29
}
new = {keys:values for keys,values in stocks.items() if values > 100}
print(new)




