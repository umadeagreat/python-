# 练习001：设计一个函数产生指定长度的验证码，验证码由大小写字母和数字构成
import random


def generate_code(code_len=4):#函数括号内为默认属性值#

    all_chars = '0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ'
    last_pos = len(all_chars) - 1
    code = ''
    for _ in range(code_len):
        index = random.randint(0, last_pos)
        code += all_chars[index]
    return code
-----------------------------------------------------------------------------
# 练习002：设计一个函数返回给定文件名的后缀名
def back(filename):
  index = filename.find(".")
  name = filename[index:]
  print(name)
 -------------------------------------------------------------------------------
 # 练习003：设计一个函数返回传入的列表中最大和第二大的元素的值
 def max2(x):
    m1, m2 = (x[0], x[1]) if x[0] > x[1] else (x[1], x[0])
    for index in range(2, len(x)):
        if x[index] > m1:
            m2 = m1
            m1 = x[index]
        elif x[index] > m2:
            m2 = x[index]
    return m1, m2
 --------------------------------------------------------------------------------
 # 练习004：计算指定的年月日是这一年的第几天
 def is_leap_year(year):


def which_day(year, month, date):
  
    days_of_month = [
        [31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31],
        [31, 29, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31]
    ][is_leap_year(year)] #如果后面的列表为True，则采用下面一列，False则用上面一列#
    total = 0
    for index in range(month - 1):
        total += days_of_month[index]
    return total + date
 ---------------------------------------------------------------------------------
 # 练习005：打印杨辉三角
 def main():
    num = int(input('Number of rows: '))
    yh = [[]] * num
    for row in range(len(yh)):
        yh[row] = [None] * (row + 1)
        for col in range(len(yh[row])):
            if col == 0 or col == row:
                yh[row][col] = 1
            else:
                yh[row][col] = yh[row - 1][col] + yh[row - 1][col - 1]
            print(yh[row][col], end='\t')
        print()


if __name__ == '__main__':
    main()
