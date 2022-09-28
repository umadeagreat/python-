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
