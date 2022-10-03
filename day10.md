# 面向对象编程入门
# 案例1：定义一个类描述数字时钟
import time


class Clock:
    def __init__(self, hour=0, minute=0, second=0): #定义属性#
        self.hour = hour
        self.minute = minute
        self.second = second

    def show(self): #若该函数为__repr__，则打印对象输出return中的结果#
        return f"{self.hour:02d}:{self.minute:02d}:{self.second:02d}"
          #百分号可用冒号替代:%d-直接按位数输出；%2d：右对齐按两位输出空格补位；%-2d：左对齐按两位输出空格补位；
          %02d：右对齐按两位输出，空格的地方补0；%.2d强制按小数点后两位输出#
    def run(self):
        self.second += 1
        if self.second == 60:
            self.minute += 1
            self.second = 0
            if self.minute == 60:
                self.hour += 1
                self.minute = 0
                if self.hour == 24:
                    self.hour = 0


clock = Clock(23, 59, 58) #创建对象#
while True:
    print(clock.show()) #给对象发消息读取当前时间#
    time.sleep(1)
    clock.run() #给对象发消息使其走字#
    
    总结：调用类中的函数就是在给对象发消息使其运行对应的程序，一般步骤为：定义类-创建对象-给对象发消息
    
 # 案例2：定义一个类描述平面上的点，要求提供计算到另一个点距离的方法
 import math
class Point(object):
    def __init__(self, x=0, y=0):
        self.x = x
        self.y = y

    def move(self, dx, dy):
        self.x += dx
        self.y += dy
        return f"{self.x}, {self.y}"

    def distance(self, other): #other代表另一个对象#
        dx = self.x - other.x
        dy = self.y - other.y
        return math.sqrt(dx ** 2 + dy ** 2)

    def __str__(self): #与__repr__的区别在于：str是可读的返回的是字符串，repr主要用于调试返回的是对象本身，举例datetime()#
        return  f"({self.x},{self.y})"
        
# 面向对象编程进阶：
# 学习001：可见性和属性装饰器
class Student:

    def __init__(self, name, age):
        self.__name = name#在属性前面添加__代表不可见#
        self.__age = age

    def study(self, course_name):
        print(f'{self.__name}正在学习{course_name}.')

    @property #通过这种装饰器来获得属性#
    def name(self):
        return self.__name

    @property
    def age(self):
        return self.__age

    @name.setter #通过这种装饰器来修改属性#
    def name(self, name):
        self.__name = name or "无名氏" #只要修改的属性不为空值则被赋值，否则为无名氏#

    @age.setter
    def age(self, age):
        self.__age = age or "未知"

stu1 = Student("wangdachui", 20)
print(stu1.name, stu1.age)
stu1.name = ""
stu1.age = ""
print(stu1.name, stu1.age)
总结：虽然属性会被设为不可见，但是可以通过装饰器的方法来获得和修改

# 学习002：__slots__魔法:
class Student:
    __slots__ = ('name', 'age')  #限定对象的属性只能为name和age#

    def __init__(self, name, age):
        self.name = name
        self.age = age


stu = Student('王大锤', 20)
# AttributeError: 'Student' object has no attribute 'sex'
stu.sex = '男' #若没有slots魔法，则正常情况下是为对象添加并输入一个sex的属性#

# 学习003：作用于类的静态方法
import math
class Triangle(object):
    def __init__(self, a, b, c):
        self.a = a
        self.b = b
        self.c = c

    @staticmethod #静态方法，对于类而言判断是否能构成三角形#
    def is_valid(a, b, c):
        return a + b > c and a + c >b and b + c > a

    def length(self): #对象方法：计算周长#
        return self.a + self.b + self.c

    def area(self): #对象方法：计算面积#
        p = self.length() / 2
        return math.sqrt(p * (p -self.a) * (p - self.b) * (p - self.c))

t1 = Triangle(3, 4, 5)
print(t1.is_valid(3, 4, 5))
print(t1.area())
print(t1.length())

# 学习004：类的继承
class Person():
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def sleep(self):
        print(f"{self.name}正在睡觉")

    def eat(self):
        print(f"{self.name}正在吃饭")

class Student(Person): #子类括号里为父类#
    def __init__(self, name, age, course): #初始化过程中子类需要的属性#
        super(Student, self).__init__(name, age) #通过super函数继承父类的属性和方法（？）#
        self.course = course #子类自己另外添加的属性#

    def learn(self):
        print(f"{self.name}正在学习{self.course}")

class teacher(Person):
    def __init__(self, name, age, title, course):
        super().__init__(name, age)
        self.course = course
        self.title = title

    def teach(self):
        print(f"{self.title} {self.name} is teaching {self.course}")

t1 = teacher("Mary", 24, "professor", "Math")
t1.teach()



 
