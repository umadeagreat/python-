# 学习001：关于类和对象的定义与使用：
class Student(object):#定义类#
    def __init__(self, name, age):
        self.name = name
        self.age = age
    def study(self,course_name):
        print("%s正在学习%s"% self.name, course_name)
    def watch(self):
        if self.age < 18:
            print("%s正在观看pekki pigs" % self.name)
        else:
            print("%s正在观看north park" % self.name)



def main():#定义对象#
    stu1 = Student("Lihua", 24)
    stu1.study("思想品德")
    stu1.watch()
    stu2 = Student("Hanmei", 15)
    stu2.study("Science")
    stu2.watch()

if __name__ == "__main__":#一种方法，可保证导入该模块时该模块的代码不会被运行#
    main()
----------------------------------------------------
# 学习002：property装饰器：
class Person():
    def __init__(self, name, age):
        self._name = name
        self._age = age

    @property
    def name(self):
        return self._name

    @property
    def age(self):
        return self._age

    @age.setter
    def age(self,age):
        self._age = age

    def play(self):
        if self._age < 16:
            print(f"{self._name}正在下飞行棋")

        else:
            print(f"{self._name}正在下五子棋")


def main():
    mab = Person("Mab", 14)
    mab.play()
    mab.age = 22 #修改时不用再写下划线，下划线是为了保密#
    mab.play()

if __name__ == "__main__":
    main()
-------------------------------------------------------------
# 学习003：静态方法，判断能否构成三角形：
from math import sqrt


class Triangle():
    def __init__(self, a, b, c):
        self.a = a
        self.b = b
        self.c = c

    @staticmethod
    def is_valid(a, b, c):
        return a + b > c and a + c > b and b + c > a

    def peremeter(self):
        return self.a + self.b +self.c

    def area(self):
        p =  self.peremeter()/2
        return sqrt(p * (p - self.a) * (p - self.b) * (p - self.c))



def main():
    a, b, c = 1, 2, 3 #先看能否构成三角形，若能够，才建立一个三角形，从而进行周长和面积的计算#
    if Triangle.is_valid(a, b, c):
        t = Triangle(a, b, c)
        print(t.peremeter())
        print(t.area())
    else:
        print("不能构成三角形")


if __name__ == "__main__":
    main()
 ------------------------------------------------------------------
#学习004：类方法的使用:
from time import time, localtime, sleep


class Clock(object):
    def __init__(self, hour = 0, minute = 0, second = 0):
        self._hour = hour
        self._minute = minute
        self._second = second

    @classmethod
    def now(cls):#获取现在的时间#
        ctime = localtime(time())
        return cls(ctime.tm_hour, ctime.tm_min, ctime.tm_sec)

    def run(self):
        self._second += 1
        if self._second == 60:
            self._minute += 1
            self._second = 0
            if self._minute == 60:
                self._hour = 1
                self._minute = 0
                if self._hour == 24:
                    self._hour =0

    def show(self):
        return "%02d:%02d:%02d" % \
               (self._hour , self._minute, self._second)


def main():
    clock = Clock.now()
    while True:
        print(clock.show()) #展示要显示的时间#
        sleep(1)
        clock.run() #继续运行显示时间#

if __name__ == "__main__":
    main()
-------------------------------------------------------------------
# 练习001：定义一个类描述数字时钟
from time import sleep


class Clock(object):
    def __init__(self,hour = 0, minute = 0, second = 0):
        self._second = second
        self._minute = minute
        self._hour = hour
    def run(self):
        self._second += 1
        if self._second == 60:
            self._minute += 1
            self._second =0
            if self._minute == 60:
                self._hour += 1
                self._minute = 0
                if self._hour == 24:
                    self._hour = 0
    def show(self):
        return "%02d:%02d:%02d" % \
               (self._hour, self._minute, self._second)

def main():
    clock = Clock(23, 59, 58)
    while True:
        print(clock.show())
        sleep(1) #括号中是令程序暂停的秒数#
        clock.run()


if __name__ == "__main__":
    main()
 -------------------------------------------------------------------
 # 练习002：定义一个类描述平面上的点并提供移动点和计算到另一个点距离的方法
 from math import sqrt


class Point():
    def __init__(self, x = 0, y = 0): #只是初始化值，也可以通过后面的函数进行改变#
        self.x = x
        self.y = y

    def move_to(self, x, y):
        self.x = x
        self.y = y

    def move_by(self, dx, dy):
        self.x += dx
        self.y += dy

    def distance(self, other): #other指的是已被定义的另一个属于同一类的变量？#
        dx = self.x - other.x
        dy = self.y - other.y
        return(sqrt(dx ** 2 + dy ** 2)) #出现在之前函数的变量可使用于下一个函数定义中#

    def __str__(self):
        return "(%s, %s)" % (str(self.x), str(self.y))  #将对象变成字符串，展示给用户看#

def main():
    p1 = Point(3, 5)
    p2 = Point()
    print(p1)
    print(p2)
    p2.move_to(-1, 2)
    print(p2)
    print(p1.distance(p2))

if __name__ == "__main__":
    main()
