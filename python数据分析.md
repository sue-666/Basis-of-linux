# pandas模块：   
pandas模块是一个**基于NumPy**的开源**数据分析库**，提供了快速、灵活、易用的**数据结构和数据分析工具**。   
主要数据结构**Series（一维数据）和DataFrame（二维数据）**，可以处理各种数据格式，如CSV、Excel、SQL数据库等，支持数据清洗、缺失值处理、数据重组、数据分析和可视化等功能。  
pip install pandas -i https://pypi.doubanio.com/simple/   
#这句话后面 -i https://pypi.doubanio.com/simple/ 表示使用豆瓣的源，这样安装会更快  
  
## 或者在Anaconda环境下，配置这一库的方法：  
打开Anaconda Prompt软件：  ![image](https://github.com/user-attachments/assets/f43bf376-ff7e-4079-8f04-147937d86eb0)  
在Python的使用过程中，我们常常由于不同Python版本以及不同第三方库版本的支持情况与相互之间的冲突情况，而需要创建不同的Python虚拟环境：  
**conda env list**   #浏览当前Anaconda中的全部环境的情况  
**conda create -n py39**   #得到一个Python版本与base环境中Python版本一致的虚拟环境  
**conda create -n py36 python=3.6**   #指定Python版本的虚拟环境
**conda activate py36**   #使用某py36虚拟环境
**conda deactivate**   #退出当前虚拟环境
**conda remove -n py39 --all**   #删除某个虚拟环境


  
### 在一个名称为pystudy的Python虚拟环境中配置pandas库： 
**conda activate pystudy  
conda install -c anaconda pandas  
输入y开始pandas库的配置工作**  

  
import pandas as pd #引入 pandas 模块   


  
## Series  一维数据，S大写  
  
类似于 Numpy 中一维数组的对象，由**索引--数据**组成。例子：  
print(pd.Series([2, 4, 6, 8], index=['a', 'b', 'c', 'd']))  #不特指时默认列表[]索引：index=[0，1，2，3]  
或使用**字典{}**：  键作为数据标签，值作为相对应的数据  
print(pd.Series({'a': 2, 'b': 4, 'c': 6, 'd': 8}))  

print（S1+S2）: (直接相加：数据对齐)将相同数据标签的数据进行了计算  
print(s1.add(s2, fill_value=0))  # 调用 Series 的 **.add() 方法**，fill_value 为数据缺失对应时的默认值    
![image](https://github.com/user-attachments/assets/960d6c9f-0bc9-419f-8caf-b481076d2b22)  


    
## DataFrame  二维数据（表格）表格中的每一行或每一列都是一个 Series    
   
表格中有中文时：中文占用的字符和英文、数字占用的字符不一样，调用 pd.set_option() 使表格对齐显示：  
pd.set_option('display.unicode.ambiguous_as_wide', True)  
pd.set_option('display.unicode.east_asian_width', True)  
  
构建 DataFrame 最常用的方法：传入一个由**等长列表**组成的字典。即字典里每个值都是列表，且它们的长度必需相等。   
data = {
  '炸鸡': [14, 20,30],
  '面包': [7, 3,6],
  '可乐': [8, 13,9],
  '烤肠': [10, 6,2]
}                          #每列标签：表头
df = pd.DataFrame(data, index=['2020-01-01', '2020-01-02'，'2020-01-03'])  #每行标签（索引）
print(df)


## 列的查改增删  
import pandas as pd   
df = pd.DataFrame({'炸鸡': [14, 20], '面包': [7, 3], '可乐': [8, 13], '烤肠': [10, 6]})    
  
### 查看列：  
print(df[['可乐', '炸鸡']])     #中括号加列名  
### 修改列：  
df['可乐'] = [18, 23]   #重新赋值    
### 新增列：  
df['糖果'] = [3, 5]    #对表格中不存在的列直接赋值添加列  
### 删除列：   .drop() 方法  
df = df.drop('面包', axis=1)  #.drop() 第一个参数是要删除的列名/索引。axis 表示针对行或列进行删除，axis = 0 删除对应行，axis = 1 删除对应列，axis 默认为 0。  


    
# 使用 pandas 导入导出表格文件.csv  
   
导入导出 .csv 文件,方法是 df = pd.read_csv() 和 df.to_csv()
导入导出 Excel 文件，方法是 df = pd.read_excel() 和 df.to_excel()   
df = pd.read_excel('2019年销售数据.xlsx', sheet_name='工作表1')  # 导入工作表1，Excel 有多个工作表时  
df.to_excel('2019年销售数据.xlsx', index=False, sheet_name='工作表1')  # 导出到工作表1  
  
import pandas as pd  
**df = pd.read_csv('2019年销售数据.csv')**   #使用 pd.read_csv() 函数，将其导入到 pandas 中 
print(type(df))  
print(df.head())  # 使用 .head() 方法来查看前 5 条数据, print(df.head(2)): 查看前2条    
print(df.tail())   # .tail()查看末尾的数据  
**print(df.info())**   # 通过 info() 方法查看整个表格的大致信息, 有几行几列，以及哪列有多少条缺失数据  
![image](https://github.com/user-attachments/assets/d6ea608a-0afe-4f13-9e07-9cfab27dbb9a)  
**print(df.describe())**   # 通过 describe() 方法来快速查看数据的统计摘要,从上往下分别表示数量、平均数、标准差、最小值、25% 50% 75% 位置的值和最大值  
![image](https://github.com/user-attachments/assets/f8bb08c2-cf71-476f-ae6b-00207ce904a9)  

通过列的增加 定义一列新的计算结果：
df['总和'] = df['第一季度'] + df['第二季度'] + df['第三季度'] + df['第四季度']  
![image](https://github.com/user-attachments/assets/d1dcc891-ee5a-4b32-b0b0-5df939c2d2e2)  
  
调用 max()、min()、mean()、sum() 等方法来计算最大值、最小值、平均值以及求和等：  
## 最大值  df['总和'].max()  
  
## 最小值  df['总和'].min()  
  
## 平均  df['总和'].mean()  
  
## 求和  df['总和'].sum()  
  
## 用 sort_values() 方法对表格进行排序：  
df = df.sort_values('总和', ascending=False)    #第一个参数是要排序的列（表格所有数据都跟随其改变顺序），排序默认升序，将 ascending 设为 False 改成降序，最大排第一： df.head(1)   
   
## df.to_csv('2019年销售数据修改后.csv', index=False)   # 导出表格数据  
#传入 index=False 是因为不希望将最左侧的索引保存到文件中  



## 数据划分:



































