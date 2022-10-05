# 第23课：用python读写csv文件

将数据写入csv文件：
import csv
import random
with open("scores.csv", "w") as file: #当创建一个新的文件时"w"是必不可少的#
    writer = csv.writer(file)
    names = ["A", "B", "C", "D", "E"]
    writer.writerow(["姓名", "语文", "数学", "英语"]) #以列表中行的形式写入csv文件#
    #writer = csv.writer(file, delimiter='|', quoting=csv.QUOTE_ALL)：dilimiter是指定分隔符，通常情况下默认为逗号，quoting是包围值的字符，默认为双引号
    for name in names:
        scores = [random.randint(50, 100) for _ in range(3)]#对于每一姓名，生成三个(50, 100)的分数#
        scores.insert(0, name) #insert方法前面的数字代表索引的位置，后面代表需要插入的内容#
        writer.writerow(scores) #以列表三行形式写入csv文件#
        
从csv文件中读取数据：
import csv
with open("scores.csv", "r") as file: #"r"，必不可少#
    reader = csv.reader(file, delimiter = "|") #delimiter在这里表示取消分隔符的意思，此步为创建对象#
    for data_list in reader: #对于reader这个对象中的每一行来说（把每一行看成一个列表）#
        print(reader.line_num,end="\t") #"\t"是制表符的意思，此步为输出每一行的行序#
        for elem in data_list: #对于每一行中的每一个元素#
            print(elem, end="\t") #输出元素#
        print() #print()函数在末尾起的是换行的作用#
        
# 第24课：用python读写excel文件
读：不会，代码有出入
写：
import random
import openpyxl as xl

wb = xl.Workbook() #通过Workbook创建工作簿#
sheet = wb.active #在工作簿里创建表单#
sheet.title = "Scores" #为表单命名#

titles = ("姓名", "语文", "数学", "英语") #创建一个元组，使其为列名称#
for col_index, title in enumerate(titles): #enumerate是索引指数对应元素，索引指数从0开始，所以需要+1#
    sheet.cell(1, col_index + 1, title)

names = ("A", "B", "C", "D", "E") #创建一个元组，使其为行名称#
for row_index, name in enumerate(names):
    sheet.cell(row_index + 2, 1, name) #之前的列名称已经占据一行，所以从第二行开始，其余同上#
    for col_index in range(2, 5):#从第二列开始#
        sheet.cell(row_index + 2, col_index, random.randint(50, 100)) #一行一列被占据，要写入的内容从第二行第二列开始#

wb.save("考试成绩工作簿.xlsx") #保存工作簿，注意后面需要标明文件类型#
注：（
1、行名、列名应该为一个元组
2、为了方便用户使用，表格行与列的计数都是从1开始的，注意与索引指数之间的关系
3、2007版本的excel文件为xls类型，openpyxl不能处理，openpyxl处理的应该是新版本的xlsx文件）


运用公式进行计算：
import openpyxl

wb = openpyxl.load_workbook("考试成绩工作簿.xlsx")
sheet = wb["Scores"]

sheet["E1"] = "平均分" #在表格中命名一个新的列#
for i in range(2, 7): #从第二行第六列开始记录新的数据#
    sheet[f"E{i}"] = f"=average(B{i}:D{i})" #公式表达和excel中差不多，只是也需要加双引号#
wb.save("考试成绩.xlsx")

生成统计图表：
import openpyxl as xl
from openpyxl.chart import BarChart, Reference #Barchart为条形图，Reference是引用#

wb = xl.Workbook(write_only=True)
sheet = wb.create_sheet()

rows = [("类别", "销售A组", "销售B组"),
         ("手机", 30, 50),
         ("平板", 90, 60),
         ("笔记本", 45, 70),
         ("外围设备", 20, 10),
         ]
#以由元组构成的列表形式输入数据，每一元组对应的是一个行，注意数字不要用双引号！！#
for row in rows:
    sheet.append(row) #往表格中按行添加数据#

chart = BarChart()
chart.type = "col" #表格类型#
chart.style = 10  #表格样式#
chart.title = "销售对比图" #表格名称#
chart.y_axis.title = "销量" #表格纵轴#
chart.x_axis.title = "类别" #表格横轴#
data = Reference(sheet, min_col=2, min_row=1, max_row=5, max_col=3) #要引用的表格内容，记为datas，实际上这一步是引用要进行对比的数据#
cats = Reference(sheet,min_col=1, min_row=2, max_row=5) #要引用的表格内容，记为cats，实际上这一步是引用进行对比的种类名称（细分，所对比的总体共有的属性）#
chart.add_data(data, titles_from_data=True) #将数据添加到表格中，后面的bool值表示默认引用的数据的第一行为所进行对比的两个类（进行对比的总体）#
chart.set_categories(cats)#将cats作为数据对比的类型#
chart.shape = 4 #一共四种属性进行对比#
sheet.add_chart(chart, "A10") #将表格添加到表单中#

wb.save("fine.xlsx")
import openpyxl as xl
from openpyxl.chart import BarChart, Reference

wb = xl.Workbook(write_only=True)
sheet = wb.create_sheet()

