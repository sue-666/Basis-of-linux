# pandas模块：   
pandas模块是一个**基于NumPy**的开源**数据分析库**，提供了快速、灵活、易用的**数据结构和数据分析工具**。   
主要数据结构**Series和DataFrame**，可以处理各种数据格式，如CSV、Excel、SQL数据库等，支持数据清洗、缺失值处理、数据重组、数据分析和可视化等功能。  
在Anaconda环境下，配置这一库的方法：  
打开Anaconda Prompt软件：  ![image](https://github.com/user-attachments/assets/f43bf376-ff7e-4079-8f04-147937d86eb0)  
在Python的使用过程中，我们常常由于不同Python版本以及不同第三方库版本的支持情况与相互之间的冲突情况，而需要创建不同的Python虚拟环境：  
**conda env list**   #浏览当前Anaconda中的全部环境的情况  
**conda create -n py39**   #得到一个Python版本与base环境中Python版本一致的虚拟环境  
**conda create -n py36 python=3.6**   #指定Python版本的虚拟环境
**conda activate py36**   #使用某py36虚拟环境
**conda deactivate**   #退出当前虚拟环境
**conda remove -n py39 --all**   #删除某个虚拟环境




在一个名称为py38的Python虚拟环境中配置pandas库： 
**activate py38  
conda install -c anaconda pandas  
输入y开始pandas库的配置工作**
原文链接：https://blog.csdn.net/zhebushibiaoshifu/article/details/129421118
