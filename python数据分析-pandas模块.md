# pandas模块：   
pandas模块是一个**基于NumPy**的开源**数据分析库**，提供了快速、灵活、易用的**数据结构和数据分析工具**。     

**!!!!!预设：表格 中英文 对齐**：中文占用的字符和英文、数字占用的字符不一样，调用 pd.set_option() ：  
**pd.set_option('display.unicode.ambiguous_as_wide', True)**  
**pd.set_option('display.unicode.east_asian_width', True)**  

**#读取销售数据，并将第一列设置为行索引：  df = pd.read_csv('数据表格.csv', index_col=0)**
#获取不同行： 5、10、20 的行数据并打印出来：print(df.loc[['5','10','20']])
#获取 7 到14行 的数据并打印出来：print(df.loc['7':'4'])
#获取列标签'团队' 为A的 所有数据并打印出来：print(df.loc[df['团队']=='A'])

  
主要数据结构**Series（一维数据）和DataFrame（二维数据）**，可以处理各种数据格式，如CSV、Excel、SQL数据库等，支持数据清洗、缺失值处理、数据重组、数据分析和可视化等功能。  
pip install pandas -i https://pypi.doubanio.com/simple/   
#这句话后面 -i https://pypi.doubanio.com/simple/ 表示使用豆瓣的源，这样安装会更快  
  
### 或者在Anaconda环境下，配置这一库的方法：  
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


  
## 1、 Series  一维数据，S大写  
  
类似于 Numpy 中一维数组的对象，由**索引--数据**组成。例子：  
print(pd.Series([2, 4, 6, 8], index=['a', 'b', 'c', 'd']))  #不特指时默认列表[]索引：index=[0，1，2，3]  
或使用**字典{}**：  键作为数据标签，值作为相对应的数据  
print(pd.Series({'a': 2, 'b': 4, 'c': 6, 'd': 8}))  

print（S1+S2）: (直接相加：数据对齐)将相同数据标签的数据进行了计算  
print(s1.add(s2, fill_value=0))  # 调用 Series 的 **.add() 方法**，fill_value 为数据缺失对应时的默认值    
![image](https://github.com/user-attachments/assets/960d6c9f-0bc9-419f-8caf-b481076d2b22)  


    
## 2、 DataFrame  二维数据（表格）表格中的每一行或每一列都是一个 Series    
   

  
构建 DataFrame 最常用的方法：传入一个由**等长列表**组成的字典。即字典里每个值都是列表，且它们的长度必需相等。   
data = {
  '炸鸡': [14, 20,30],
  '面包': [7, 3,6],
  '可乐': [8, 13,9],
  '烤肠': [10, 6,2]
}                          #每列标签：表头
df = pd.DataFrame(data, index=['2020-01-01', '2020-01-02'，'2020-01-03'])  #每行标签（索引）
print(df)

 
import pandas as pd   
df = pd.DataFrame({'炸鸡': [14, 20], '面包': [7, 3], '可乐': [8, 13], '烤肠': [10, 6]})    

## 查看行或列： 
通过 **.loc** 访问特定 **行+列**：  **df.loc['行标签', '列标签']**   

**查看列(行不能通过该直接查看定位)：  print(df[['可乐', '炸鸡']])**  
**通过 .loc['列标签'] 访问特定列**    

**通过 .loc['行标签'] 访问特定行** 
#loc 属性不仅支持“索引”，还支持“切片”，需要写成 **.loc[start:end]** **包含start和end**   
传入一个 标签列表 可获取 loc 中不连续的行。例如 **df.loc[['行1', '行3', '行5']]**   
print(df.loc[[True, False, True, False, True]])   #将第 1、3、5 行数据筛选出来  #**选中该行（True），忽略该行（False）**
选中比较区间：**df.loc[df['语文'] > 90]**    #df.loc[df['语文'] > 90]  ==  df[df['语文'] > 90]  


### 修改列：  df['可乐'] = [18, 23]           #重新赋值    
### 修改行： #重新赋值为长度和列数相等的列表  
1、赋值为一个数字；  
2、赋值为长度和列数相等的列表。  
3、**df.loc['行标签-学号', '列标签-语文成绩'] = 90 定位到行和列来修改特定的数据**  


### 新增列：  df['糖果'] = [3, 5]          #对表格中不存在的列直接赋值添加列  
### 新增行：  
**传入表格中不存在的索引**  
#添加一名学生 S06，ta 成绩全为 90：  df.loc['S06'] = 90  
#添加一名学生 S07，ta 三门课成绩分别为 85，90，85:  df.loc['S07'] = [85, 90, 85]  

### 删除列：   df = df.drop('列标签-语文', axis=1)    #.drop() 第一个参数是要删除的列名/索引。  axis 表示针对行或列进行删除，axis = 0 删除对应行，axis = 1 删除对应列，axis 默认为 0。  
### 删除行：   df = df.drop('行标签-学号S02') 
 

![image](https://github.com/user-attachments/assets/cd7a4945-c9ca-4bb0-8330-c9d5b03bb941)  



    
### 使用 pandas 导入导出表格文件.csv  
   
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
#### 最大值  df['总和'].max()  
  
#### 最小值  df['总和'].min()  
  
#### 平均  df['总和'].mean()  
  
#### 求和  df['总和'].sum()  
  
#### 用 sort_values() 方法对表格进行排序：  
df = df.sort_values('总和', ascending=False)    #第一个参数是要排序的列（表格所有数据都跟随其改变顺序），排序默认升序，将 ascending 设为 False 改成降序，最大排第一： df.head(1)   
   
#### df.to_csv('2019年销售数据修改后.csv', index=False)     
导出表格数据,传入 index=False 是因为不希望将最左侧的索引保存到文件中  



## 3、 数据分类、分区: pd.cut(,,) 

mean_total = df['总和'].mean()  
start = df['总和'].min() - 1  
end = df['总和'].max()  
df['绩效'] = pd.cut(x=df['总和'],  
                   bins=[start, mean_total * 0.9, mean_total * 1.1, mean_total * 1.2, end],  
                   labels=['不合格', '合格', '良好', '优秀'])   

df['新加一列等级划分']=pd.cut( x数据=df['分数'] ，bins分类依据[start,end] ， labels类别标签['不及格','优秀'] )   
按某一列数据将其分割成若干区间，得到的 result 是一个 Series 类型变量  
![image](https://github.com/user-attachments/assets/01d88eb2-7a82-47cf-9db8-a04c76315dcd)  
## 数据透视:  pivot_table() 函数 重组表格   得到数据透视表 pivot 
pivot = df.pivot_table(  
  index='团队',  # 数据透视表的行  
  columns='绩效',  # 数据透视表的列  
  aggfunc={  
    '工号': 'count' # 统计不同团队、不同绩效等级的员工数量  
  }  
)   
tier_table = pivot['工号']  #tier, 等级，通过 '工号' 索引访问对工号列的统计结果（计数）  
tier_table['优秀率'] = tier_table['优秀'] / tier_table.sum(axis=1)  


**index**：数据透视表的**行**； **columns**：数据透视表的**列**； **aggfunc**："agg" 是单词 aggregate 的缩写，含义为“聚合”。在这里我们需要指定**对哪一列**数据进行何种**统计操作**，得到新表格单元格的值。对 '工号' 列执行计数（'count'）操作，写成代码就是 aggfunc={'工号': 'count'}  
![image](https://github.com/user-attachments/assets/83918de1-4923-463b-9573-de9977a87a5c)  

![image](https://github.com/user-attachments/assets/b3cb9a3f-458c-4998-a3b6-b139c48d0eef)  

## 4、 数据筛选:  
  ![image](https://github.com/user-attachments/assets/cea80754-14f3-4cdd-b528-fa4ce8cbbb4d) 
 并且&       result=df[()&()] 同时满足2个条件  
 或者|       result=df[()|()]   满足任何1个条件 
 result = df[(df['绩效'] == '优秀') | (df['绩效'] == '不合格')]
 
![image](https://github.com/user-attachments/assets/d0e325a4-a287-4354-add6-43933d03db50)   

![image](https://github.com/user-attachments/assets/6e09cf6f-8f13-4801-88e3-5b1042d82885)
  










































