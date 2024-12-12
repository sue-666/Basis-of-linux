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
  '炸鸡': [14, 20，30],
  '面包': [7, 3，6],
  '可乐': [8, 13，9],
  '烤肠': [10, 6，2]
}                          #每列标签：表头
df = pd.DataFrame(data, index=['2020-01-01', '2020-01-02'，'2020-01-03'])  #每行标签（索引）
print(df)



















