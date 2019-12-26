# 基于碳纳米管的多级纳米旋转传动系统的设计与研究

> 参考资料
 > [基于碳纳米管的多级纳米旋转传动系统的设计与研究所有相关的文件均可在此链接获得](https://github.com/ld269440877/images/tree/master/3CRTR)
>- 参考文献和endnote库文档及样式（文件夹3ClassPDFReference）
>- 所有电机、转子、定子的模型（文件夹Models_two_class）
>- 案例M1111S270-1111-1111-1111-1111的相关源文件（文件夹M1111S270-1111-1111-1111-1111）
>- 各个模型仿真旋转传动比和质心结果图像可以幕布中查看，[幕布链接](https://mubu.com/doc/2ynYkgt4_g)
>- LAMMPS常见错误[幕布链接](https://mubu.com/doc/1FEOeL5-ig)
>- VMD常见操作[幕布链接](https://mubu.com/doc/2Irn2aCEqg)
>- 主要参考
> [西北农林科技大学的文章SCI链接](https://www.sciencedirect.com/science/article/abs/pii/S0927025618304610?via%3Dihub)，[qiu_Compt Mater Sci_2018PDF链接](https://github.com/ld269440877/images/blob/master/3CRTR/3ClassPDFReference/qiu_Compt%20Mater%20Sci_2018.pdf)
> [Reversing rotation of a nanomotor by introducing a braking BNC nanotube - ScienceDirect](https://www.sciencedirect.com/science/article/abs/pii/S0927025618308103#bb0175)
>- 我的大论文和两篇小论文2019PDF[3CRTRPapers链接](https://github.com/ld269440877/images/tree/master/3CRTR/MyPapers)
>- [一劳永逸，打造自己的word常规模板 - 知乎](https://zhuanlan.zhihu.com/p/22737822?utm_source=wechat_session&utm_medium=social&s_s_i=0Jr%2F66LIPO69pu1XHpcJTQP3RFNwcbT5YPmgcocanUY%3D&s_r=0&wechatShare=1)
[Endnote的使用方法（史上最详细）](https://mp.weixin.qq.com/s/Qr5mvy4rQ-wAfEcE9i4ypA)

> 注：源码程序执行过程中会切换目录
> 1. `固定目录`代表源码文件所在目录，此目录不存储其他文件
> 2. `可变目录`代表切换到指定存储新建模型的文件夹内，该程序所产生的文件均在该目录下
> 3. 程序运行结束后会切换到`固定目录`，遵守一个模型一个文件夹原则

## 建模

### VMD创建单根碳纳米管模型

VMD创建碳纳米管模型，根据用途分类，分别存放在电机、转子、定子命名的文件夹内，每个碳纳米管模型的文件命名规则为`模型用途类型-半径-手性-长度-原子总数.gro`[碳纳米管gro文件](https://github.com/ld269440877/images/tree/master/3CRTR/Models_two_class)，[NanoTubeChiralityandRadii.xlsx](https://github.com/ld269440877/images/blob/master/3CRTR/NanoTubeChiralityandRadii.xlsx)

![VMD创建碳纳米管模型并分类](https://raw.githubusercontent.com/ld269440877/images/master/3CRTR/VMD创建碳纳米管模型并分类.png)

### python程序3CRTR模建并创建3CRTR模型相应的LAMMPS计算文件

- 3CRTR模建及其相应的LAMMPS计算文件都在本程序源码中一次性创建步骤依次为
1. 读取建模所需的[碳纳米管gro文件](https://github.com/ld269440877/images/tree/master/3CRTR/Models_two_class)
2. 设置3CRTR位置关系[如图3CRTR模型](https://raw.githubusercontent.com/ld269440877/images/master/3CRTR/3CRTR位置关系.png)
3. 将建模后的3CRTR模型保存为VMD格式的gro文件
4. 调用前面3CRTR模型的数据，将各组件模型末端添加氢原子
5. 合并3CRTR模型中的所有碳原子和氢原子
6. 输出[完整3CRTR模型的gro文件](https://github.com/ld269440877/images/blob/master/3CRTR/M1111S270-1111-1111-1111-1111/M1111S270-1111-1111-1111-1111.gro?1577334602536)
7. 根据需求，调用前面的数据编写用于LAMMPS读取[模型结构的data文件](https://github.com/ld269440877/images/blob/master/3CRTR/M1111S270-1111-1111-1111-1111/data.M1111S270-1111-1111-1111-1111?1577334771714)，保存
8. 根据需求，调用前面的数据编写用于LAMMPS计算的[in文件](https://github.com/ld269440877/images/blob/master/3CRTR/M1111S270-1111-1111-1111-1111/in.M1111S270-1111-1111-1111-1111?1577334813943)，保存
9. 根据需求，调用前面的数据编写用于Linux服务器提交任务的[lsf文件](https://github.com/ld269440877/images/blob/master/3CRTR/M1111S270-1111-1111-1111-1111/lsf.M1111S270-1111-1111-1111-1111)，保存
10. 根据需求，调用前面的数据编写[document文件](https://github.com/ld269440877/images/blob/master/3CRTR/M1111S270-1111-1111-1111-1111/documentM1111S270-1111-1111-1111-1111.txt?1577334910591)查看模型的设置和路径
11. 根据需求，调用前面的数据编写Linux下的shell脚本[rm_cp_bsub](https://github.com/ld269440877/images/blob/master/3CRTR/M1111S270-1111-1111-1111-1111/rm_cp_bsub2019923?1577334937694)，一键文本格式转换win->Linux、复制LAMMPS运行所需文件、提交任务

- 建模的源码及结构截图
[3CRTR建模的源码](https://github.com/ld269440877/images/blob/master/3CRTR/3CRTRBuildModel.ipynb?1577335106447)
![建模的源码结构图](https://raw.githubusercontent.com/ld269440877/images/master/3CRTR/建模的源码结构图.png)

## 数据分析及可视化

### 一个模型的数据分析及可视化

- 每个模型的数据单独处理同时可视化查看仿真结果
[单个模型的数据处理及可视化源码](https://raw.githubusercontent.com/ld269440877/images/master/3CRTR/3CRTRDataAnalysisandVisualization.ipynb)
![单个模型的数据处理及可视化源码图](https://raw.githubusercontent.com/ld269440877/images/master/3CRTR/单个模型的数据处理及可视化.png)
1. 计算转子1-3的质心
2. 计算转子1-3的旋转传动比RTR
3. 可视化
4. 设置轴标签：x轴的标签 Time(ns)和y轴的标签
5. 分别输出RTR和MC数据到CSV文件，行为数据记录-列为字段名称

### 多个模型的RTR和质心数据可视化面板图

- 多个模型的质心数据可视化32面板
[多个模型的质心数据可视化32面板源码](https://github.com/ld269440877/images/blob/master/3CRTR/3X2MCDataVisualization.ipynb?1577340221269)
![](https://raw.githubusercontent.com/ld269440877/images/master/3CRTR/多个模型的质心数据可视化32面板.png)
1. 读取模型质心的CSV文件
2. 设置每个模型的格式`M*-(n,m)-(n,m)-(n,m)-(n,m)`便于设置图片中的模型的编号
3. 设置图片中的模型编号样式
4. 可视化

- 多个模型的RTR数据可视化22面板
[多个模型的RTR数据可视化22面板源码](https://github.com/ld269440877/images/blob/master/3CRTR/2X2RTRDataVisualization.ipynb?1577339575965)
![](https://raw.githubusercontent.com/ld269440877/images/master/3CRTR/多个模型的RTR数据可视化22面板.png)
1. 读取模型旋转传动比的CSV文件
2. 设置每个模型的格式`M*-(n,m)-(n,m)-(n,m)-(n,m)`便于设置图片中的模型的编号
3. 设置图片中的模型编号样式
4. 可视化
