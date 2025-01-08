## 安装第三方库:  
**`pip install -i https://pypi.tuna.tsinghua.edu.cn/simple plotly`**    
Plotly 中的 `图表 (Figure)` 由两部分组成：`数据图形 (trace)` 和 `布局 (layout)` ,前者指用来表示数字的具体形状，比如柱状图中的矩形柱，散点图中的点等，而布局指所有图表中通用的组件，包括标题、图例、x 轴，y 轴等，以及图表中各个元素的排列关系。  
![image](https://github.com/user-attachments/assets/d3ddd521-5c6c-49f4-9ff2-2e23500af5ee)   
作图步骤：准备数据 ----- 创建空图表 ----- 将数据转化为**数据图形trace** 加入图表 ----- 添加或修改图表**布局layout**部件 ----- 调整数据图形、布局样式 ***  
![image](https://github.com/user-attachments/assets/0fd01a89-f843-498d-aa47-7b49820c09db)    

## 1、准备数据 ----- 2、创建空图表：     
### `python3` 进入python交互界面执行python命令(myenv环境下)：  
**`import plotly.io as pio`,`pio.renderers.default ="chrome"` 设置预览打开方式为谷歌浏览器**  

`import pandas as pd`   
`df = pd.read_csv("俱乐部月客流量.csv")`  
`print(df)`  
  
`from plotly.graph_objects import Figure` # 导入 Figure 类  
`figure = Figure()` # 创建一个空图表 figure  
`figure.show()` # 预览空图表，或保存为HTML文件：`figure.write_html("output.html")`,`print("图表已保存为 output.html")` 退出python后在linux终端打开网页：`xdg-open output.html`  
![image](https://github.com/user-attachments/assets/c68bcdb6-7e71-422e-a3a9-a9b99902f1d6)  
  
*** 
  
## 3、加入数据图形trace    
**柱形图Bar：** plotly.graph_objects 中的 Bar（柱形）类。它可以接受若干参数，其中最重要的有：  

x：x 轴数据来源，通常为列表、Series 等类型；  
y：y 轴数据来源，通常为列表、Series 等类型；  
name：该柱形图的名称，字符串类型。   
   
#导入必要的模块和类
`import pandas as pd`
`from plotly.graph_objects import Figure, Bar`
  
#导入数据
`df = pd.read_csv("俱乐部月客流量.csv")`
  
#创建一个空图表 figure
`figure = Figure()`
   
#创建柱形数据图形 old_members  
`old_members = Bar(x=df["月份"],y=df["老会员"],name='老会员')`
#将 old_members 添加进空图表 figure 中
`figure.add_trace(old_members)`

  
#创建柱形数据图形 new_members
`new_members = Bar(x=df["月份"], y=df["新会员"], name='新会员')`
#将 new_members 添加进 figure 中
`figure.add_trace(new_members)`
Plotly  默认以平行分组（group）的方式呈现各柱形图
![image](https://github.com/user-attachments/assets/9244e3dd-d693-445b-9b85-4ae27685f20b)  
  
***
  
## 4、修改柱形排列模式-布局layout：  
Plotly 中各数据图形之间的位置关系受图表 布局 （layout） 管辖，可调用 update_layout() 方法，通过设置 barmode（柱形排列模式）参数调整柱形图排列方式：  
**`figure.update_layout(barmode="stack")`**  （stack堆叠,group分组，overlay重叠，relative相对-正负值）
`figure.show()`  
![image](https://github.com/user-attachments/assets/ab1c2ce2-6f6e-4091-a9c8-bf07607145c1)  

*** 
  
## 5、调整数据图形样式(宽度、颜色、标题) :  
### 5.1 给柱形“瘦身” --- 修改柱形宽度:
控制柱形**宽度**的是 **width** 属性，默认值为 **1**，表示**占据该列宽度的 100%**。  
我们既可以在创建柱形数据图形时**指定 width 的值**，也可以借助 figure 的  **update_traces() 方法**随时调整：****
eg:  
`import pandas as pd`  
`from plotly.graph_objects import Figure, Bar`  
  
#导入数据  
`df = pd.read_csv("俱乐部月客流量.csv")`  
#创建一个空图表 figure   
`figure = Figure()`  
  
#**方法一：创建柱形图时指定宽度**   
`old_members = Bar(x=df["月份"], y=df["老会员"], name='老会员',width=0.4)`   #占列宽的 40%
`figure.add_trace(old_members)`  
  
#**方法二：先创建图形，再用 update_traces() 方法修改**   
`new_members = Bar(x=df["月份"], y=df["新会员"], name="新会员")`  
`figure.add_trace(new_members)`  #注意，需要先将 new_members 添加到 figure 中   
`figure.update_traces(width=0.4)`  #将 figure 中所有数据图形的宽度都设置为 40%  

### 5.2 颜色 颜色选取CSS网站：https://www.w3school.com.cn/cssref/css_colors.asp  
  
#**方法一：创建柱形图时指定柱形颜色**   
`old_members = Bar(x=df["月份"], y=df["老会员"], name="老会员",width=0.4,marker_color="CadetBlue")`  # 将柱形颜色设置为 CadetBlue（学员蓝）   
`figure.add_trace(old_members)`    
  
#**方法二：创建完成后借助 update_trace() 方法 调整柱形颜色** 要对两个柱形设置不同的颜色，使用 update_trace() 调整样式时，需要**传入 selector 参数指定修改对象**。     
Plotly 数据图形选择器 selector 有多种形态，其中最常用的为字典形态。例如我们想选中并修改 新会员 柱形数据图形，而该柱形有别于图表其它数据图形的最显著特征为 name（图形名称），因此我们可以编写如下选择器：  
#先创建图形，再用 update_traces() 方法修改  
`new_members = Bar(x=df["月份"], y=df["新会员"], name="新会员", width=0.4)`  
`figure.add_trace(new_members)` #注意，需要先将 new_members 添加到 figure 中    
`figure.update_traces(selector={"name": "新会员"},marker_color="MediumAquamarine")` #将 figure 中 "name" 为 "新会员" 的数据图形颜色修改为 MediumAquamarine（中度碧绿）    

### 5.3 设置图表标题   
  
**`from plotly.graph_objects import layout`** #Plotly 中的“标题”是一块单独的组件，隶属于 `plotly.graph_objects` 下的 `layout` 子模块。设置标题前，需要先导入`layout` 子模块
  
`fig_title = layout.Title(text='健身俱乐部每月客流人数',font={'size': 20,'color': 'CadetBlue'},x=0.5)`  #创建一个Title对象，传入标题内容（text）、标题字体（font）、水平位置(x)信息
![image](https://github.com/user-attachments/assets/bf621c7b-0479-4a04-b21c-c40210b1d30b)  
`font = dict(size=20, color='CadetBlue')` #可用 `dict()`函数来生成字典font={'size': 20, 'color': 'CadetBlue'}:  
**`fig_title = layout.Title(text='健身俱乐部每月客流人数',font=dict(size=20, color='CadetBlue'),x=0.5)`**  #0.5 是 [0, 1] 区间的中间数，所以表示水平居中  
figure.update_layout(title=fig_title)

*** 
  
#### 举例:   
import pandas as pd  
from plotly.graph_objects import Figure, Bar, layout  
  
#导入数据  
df = pd.read_csv("俱乐部月客流量.csv")  
  
#创建空白图表 figure  
figure = Figure()  
  
#创建老会员柱形图 old_members  
old_members = Bar(x=df["月份"], y=df["老会员"], name='老会员',  
                  width=0.4,  
                  marker_color="CadetBlue")  
#创建新会员柱形图 创建新会员柱形图  
new_members = Bar(x=df["月份"], y=df["新会员"], name='新会员',  
                  width=0.4,  
                  marker_color="MediumAquamarine")  
  
#将 old_members 和 new_members 添加到 figure 中  
figure.add_trace(old_members)  
figure.add_trace(new_members)  
    
#调整柱形排列模式  
figure.update_layout(barmode="stack")  
  
#创建一个标题，设置内容、字体和水平位置  
from plotly.graph_objects import layout  
fig_title = layout.Title(text='健身俱乐部每月客流人数',font=dict(size=20, color='CadetBlue'),x=0.5)  
#将标题添加到布局中  
figure.update_layout(title=fig_title)  
  
figure.show()  
*** 
  


















    
