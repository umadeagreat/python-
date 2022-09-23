# 学习001：可为函数设定参数的默认值
from random import randint


def roll_dice(n=2):
    """摇色子"""
    total = 0
    for _ in range(n):
        total += randint(1, 6)
    return total


def add(a=0, b=0, c=0):
    """三个数相加"""
    return a + b + c


#如果没有指定参数那么使用默认值摇两颗色子#
print(roll_dice())
#摇三颗色子#
print(roll_dice(3))
print(add())
print(add(1))
print(add(1, 2))
print(add(1, 2, 3))
#传递参数时可以不按照设定的顺序进行传递#
print(add(c=50, a=100, b=200))
----------------------------------------------
# 学习002：为函数设定可变参数：一般是不确定参数数量的情况
#在参数名前面的*表示args是一个可变参数#
def add(*args):
    total = 0
    for val in args:
        total += val
    return total
#在调用add函数时可以传入0个或多个参数#
print(add())
print(add(1))
print(add(1, 2))
print(add(1, 2, 3))
print(add(1, 3, 5, 7, 9))
---------------------------------------------------
# 练习001：写最大公约数和最小公倍数的函数
def biggest(m, n):
    if m > n:
        m, n = n, m
    for i in range(m, 0, -1):
        if m % i == 0 and n % i == 0:
            return i


def smallest(m, n):
    small_num = m * n / biggest(m, n)
    print(small_num)
    return small_num
----------------------------------------------------
# 练习002：判断一个数是否为回文数的函数
def pand(number):
    num = number
    reverse_num = num % 10
    while num > 10:
        num //= 10
        reverse_num = reverse_num * 10 + num % 10
    return number == reverse_num
----------------------------------------------------
# 练习003：判断一个数是否为素数的函数
def is_prime(number):
    for i in (2, number):
            return number % i != 0
---------------------------------------------------
#练习4：判断一个数是否为回文素数#
from bands import is_prime, is_huiwen
❤❤if __name__ == '__main__':
    num = int(input('请输入正整数: '))
    if is_huiwen(num) and is_prime(num):
        print('%d是回文素数' % num)
