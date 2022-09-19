import openpyxl as xl
#找到相关函数之后点进详细说明，看函数名称是如何使用的，函数文件名仅为文件名#
from openpyxl.chart import BarChart, Reference


def vgsale(filename):
    ###顺序：创建工作簿>选择要工作簿中要处理的表单###

    #一个excel表格里可能有好几张表单，此步骤为将整个excel表变为py工作簿#
    wb = xl.load_workbook("filename.xlsx")
    #此步骤为选择该excel工作簿中的表单，表单名称为什么下面就输入什么#
    sheet = wb["Sheet1"]

    ###顺序：选择单元格>对单元格中的数值进行处理并赋予新名称>在表单中创建新的变量名称>将该名称对应的变量值添加到单元格中###
#对于excel表格而言，想要的第一行就是表格中对应的数字，但因为python规则，最后一行应为实际行数+1#
    for row in range(2, sheet.max_row + 1):
        #cell代表对应的单元格#
        cell = sheet.cell(row, 7)
        #cell.value代表单元格的值x.y中，y代表x的某种属性#
        correct_sales = cell.value * 0.9
        #在表格对应位置中建立新的单元格#
        correct_sales_cell = sheet.cell(row, 13)
        #将值赋给新的单元格#
        correct_sales_cell.value = correct_sales
#Reference代表想要取得的值#
    vg_values = Reference(sheet,
                          min_row = 2,
                          max_row = 5,
                          min_col = 13,
                          max_col = 13
    )


###顺序：建立条形图>为条形图添加数据>将条形图添加到表格中>保存表格###
#此为建立一个空白条形图#
    chart = BarChart()
    #此为为上述定义的条形图添加数值#
    chart.add_data(vg_values)
    #此为将条形图添加到表单中#
    sheet.add_chart(chart, "o8")
#保存表单#
    wb.save("filename.xlsx")
