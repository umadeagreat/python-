#d5##学习001：找出所有水仙花数#
for i in range(0, 10):
    for j in range(0, 10):
        for k in range(0, 10):
            numb = i * 100 + j * 10 + k
            if i ** 3 + j ** 3 + k ** 3 ==  numb and len(str(numb)) == 3:
                print(numb)
-------------------------------------------------------------------------
#学习002：正整数的反转#
num = int(input("please type a number: "))
re = 0
while num > 0 :
    re = re * 10 + num % 10
    num //= 10
print(re)
------------------------------------------------------------------------
#学习003：百钱买百鸡#
num = 100
for x in range(0, 20):
    for y in range(0, 33):
        z = 100 - x - y
        money = 5 * x + 3 * y + (1 / 3) * z
        if  money == 100:
            print(x, y, z)
----------------------------------------------------------------------
#学习004：CRAPS赌博游戏#
from random import randint
money = 1000
while money > 0:
    print("你的总资产为%f元" % money)
    need_go_on = False
    while True:
        debt = int(input("你想要下注多少： "))
        if 0 < debt <= money:
            break
    first = randint(1, 6) + randint(1, 6)
    print("玩家掷出了%d点" % first)
    if first == 2 or first == 3 or first == 12:
        print("庄家赢！")
        money -= debt
    elif first == 7 or first == 11:
        print("玩家赢！")
        money += debt
    else:
        need_go_on = True
    while need_go_on:
        need_go_on = False
        twice = randint(1, 6) + randint(1, 6)
        print("玩家掷出了%d点" % twice)
        if twice == 7:
            print("庄家赢！")
            money -= debt
        elif twice == first:
            print("玩家赢！")
            money += debt
        else:
            need_go_on = True
else:
    print("你的钱都输光了，游戏结束")
 ------------------------------------------------------------
#练习001：生成斐波那契数列的前20个数#
number_0 = 1
number_1 = 1
count = 0
while count < 20:
    number_0 += number_1
    number_1 += number_0
    count += 2
    print(number_0)
    print(number_1)
------------------------------------------------------------
#练习002：找出10000以内的完美数#
import math

for num in range(2, 10000):
    sum = 0
    for i in range(1, int(math.sqrt(num)) + 1):
        if num % i == 0:
            sum += i
            if i > 1 and num // i != i:
                sum += num // i
    if num == sum:
        print(num)
------------------------------------------------------------
#练习003：找出100以内的素数#
import math

for num in range(2, 100):
    is_prime = True
    for i in range(2, int(math.sqrt(num))+1):
        if num % i == 0:
            is_prime = False
            break
    if is_prime:
        print(num, end = " ")

# int是向下取整；round是四舍五入；math.ceil是向上取整每一个数的因子，
# 除自己本身和1之外，因子不会超过平方根向下取整
# 如18：平方根向下取整为4,则有4*4<18<4*5
------------------------------------------------------------
