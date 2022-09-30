# 学习001：函数与模块
abs() #输出该数值的绝对值#
chr() #将Unicode转换为字符#
ord() #将字符转换为Unicode编码#
bin() #将整数转换为二进制字符串#
oct() #将整数转换为八进制字符串#
hex() #将整数转换为十六进制字符串#
pow() #进行幂运算#
round() #四舍五入取整数，可以指定保留小数点之后的位数#
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
