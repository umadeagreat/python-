比较运算符的存在优于赋值运算符，如flag0 = 1 == 1，将True赋给flag0
----------------------------------
#练习001：将华氏温度转换为摄氏温度#
#.1f代表此为小数点后一位的浮点型数据#
f = float(input("请输入您想要转换的华氏温度 "))
c = (f - 32)/1.8
print(f"{f:.1f}华氏度 = {c:.1f}摄氏度")
--------------------------------------
#练习002：输入圆的半径计算计算周长和面积#
import math
r = float(input("请输入圆的半径 "))
l = 2 * math.pi * r
s = math.pi * (r ** 2)
print(f"圆的周长为{l:.2f}，圆的面积为{s:.2f}")
--------------------------------------
#练习003：输入年份判断是不是闰年#
year = int(input("请输入您想要计算的年份："))
if year % 4 == 0  and year % 100 != 0 or\
    year % 400 == 0:
    print("此年份为闰年")
else:
    print("此年份为平年")
#关键点：一个数是否能被整除应用%#
-------------------------------------
#练习004：英制单位英寸与公制单位厘米互换#
choice = input("请输入您想要转换的单位（inch or cm）")
len = float(input("请输入您想要转换的长度 "))
if choice.upper() == "INCH":
    len_cm = len * 2.54
    print(f"{len} inch = {len_cm} cm")
elif choice.upper() == "CM":
    len_inch = len * 0.3937
    print(f"{len} cm = {len_inch} inch")
else:
    print("please type the correct unit")
--------------------------------------
#练习005：百分制成绩转换为等级制成绩#
#执行语句可以简化，但必须按顺序写范围#
score = float(input("please type your score: "))
level = ""
if score >= 90:
    level = "A"
elif 80 <= score:
    level = "B"
elif 70 <= score:
    level = "C"
elif 60 <= score:
    level = "D"
else:
    level = "E"
print(f"the level is {level}")
---------------------------------------
#练习006：输入三条边长，如果能构成三角形就计算周长和面积#
a = float(input("please type a: "))
b = float(input("please type b: "))
c = float(input("please type c: "))
if a + b > c and a + c > b and b + c > a :
    tri_l = a + b + c
    p = tri_l / 2
    tri_s = (p * (p - a) * (p - b) * (p - c)) ** 2 #海伦公式#
    print(f"三角形的周长为{tri_l},三角形的面积为{tri_s}")
else:
    print("不能构成三角形")
---------------------------------------
#练习007：猜谜游戏#
import random

answer = random.randint(1, 100)
counter = 0
while counter < 3:
    counter += 1
    number = int(input('请输入: '))
    if number < answer:
        print('大一点')
    elif number > answer:
        print('小一点')
    else:
        print('恭喜你猜对了!')
        break
else :
    print('你输了')
print('你总共猜了%d次' % counter)
--------------------------------------
#练习008：九九乘法表#
for i in range(1, 10):
    for j in range(1, i + 1):
        print('%d*%d=%d' % (i, j, i * j),end= "\t")
    print()
#其中，\t表示制表符，即用于对齐表格数据#
--------------------------------------
#练习009：输入一个正整数判断是不是素数#
number = int(input("Please type a positive number > 1:"))
if number > 1:
    for i in range(2, number):
        if number % i == 0:
            print("这个数并非素数")
            break                  #break是指当if成真则终止运行，若bool = False则一直循环#
    else:
        print("这个数是一个素数")
else:                             #与for同等级别的else语句，代表的是当循环完所有值之后都未能找到符合其条件的值，再执行的语句#
    print("请输入一个大于1的数")
 ------------------------------------
※※※#练习010：输入两个正整数，计算它们的最大公约数和最小公倍数#
x = int(input('x = '))
y = int(input('y = '))
if x > y:
    x, y = y, x
for factor in range(x, 0, -1):
    if x % factor == 0 and y % factor == 0:
        print('%d和%d的最大公约数是%d' % (x, y, factor))
        print('%d和%d的最小公倍数是%d' % (x, y, x * y // factor))
        break
#最小公倍数的公式：两数乘积/最大公约数，所以可先找最大公约数再找最小公倍数#
---------------------------------------
#练习010：打印如下所示的三角形图案#
row = int(input("请输入行数： "))
for i in range(1 , row+1):
    print(f"{'*' * i }")
    
row = int(input("请输入行数："))
nums = row + 1
for i in range(1 , nums):
    j = int(row - i)
    print(f"{' ' * j} {'*' * i }")
    
row = int(input("请输入行数： "))
nums = int(row * 2)
for i in range(1 , nums, 2):
    j = int((nums-i)/2)
    print(f"{' ' * j} {'*' * i } {'' * j}")
