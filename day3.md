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
