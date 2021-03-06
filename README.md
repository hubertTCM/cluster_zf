## 中医药方聚类
>这个项目是基于中医药自动组方，地址：https://github.com/gcaxuxi/cluster_2
>原项目是通过药方中药物频数相关特征，根据药物间的扩展熵（基于互信息量），最终得到相关性最高的几种药物组合。
>本项目的研究对象是药方数据中的症状信息，计算症状之间的相关性，把相关性高的症状组合聚类，最终得到若干种症状组合。
环境：python3.5 +

#### 文件列表：
- **p1_preprocess.py**
	负责对样本数据进行处理，最后输出包括药物的集合和频率等文件保存到本地
- **p2_relatives.py**
	根据上述保存的药物频率，计算由复杂系统熵构造的相似度（本质为互信息），并由此构建亲友团
- **p3_cluster.py**
	互为亲友团的药物我们称之为强相关组合，由此构建最大的强相关组合
- **4.validate.py**
	未使用该文件，为原项目的验证程序
- **prescript_cluster.py** 主程序文件，调用其他文件中的函数，实现所有功能
- data
	- **test2.csv** 数据文件
	- **hebing.txt** 同义词文件

#### 数据格式：
- test2.csv<br>

| 序号      |    方名  | .. | 主治 | 主治实体 | .. |
| ----- | ---------- | --- | ---------------------------------------- | --- | --- |
| 10000163 | 龙胆泻肝汤 | .. | 肝胆实火上扰，症见头痛目赤，胁痛口苦...  |  头痛 目赤 胁痛 口苦   |..|
| 10000195 |  保阴煎   | .. | 阴虚血热之带下淋浊，血崩便血，月经提前... | 饮食不化 胸脘痞闷 肠鸣 泄泻    |..|
| 10000242 | 参苓白术散 | .. | 饮食不化，胸脘痞闷，肠鸣泄泻，四肢乏力... | 带下色白 清稀如涕 面色恍白 倦怠    |..|
>数据分析主要使用的是`主治实体`	这一列。

- hebing.txt<br>
不孕 无子 全不产 绝产 断绪<br>
健忘 善忘 喜忘 多忘<br>
偏头痛 头偏痛 偏头风 偏正头风<br>
>同义词表，主要用来把词义近似的实体词替换成相同的词

#### 目标和功能：

&emsp;&emsp;待分析的数据是妇科相关的一部分药方，目的是研究症状之间的相关性，得到若干个症状的组合类。根据[《复杂系统方法学与中医证候建模》](1)153页的**无监督复杂系统熵聚类算法**，[陈建新.中医证候的复杂系统建模及其与疾病的相关性研究](2)论文，最终得到的类就对应于中医诊断中的证型。也就是说，通过该聚类算法，最终能够把药方主治信息映射为药方对应的证型信息，实现对药方性质的一些分析。<br>
&emsp;&emsp;在中医自动组方研究过程中，我们的最终目标是实现计算机的智能开方，即计算机分析患者的症状及年龄性别相关信息，给出若干个药方，这些药方可以是典籍记载的（验方），也可能是之前从来没有记载的。<br>
&emsp;&emsp;经典的分类算法，解决的是多特征对应几个标签的问题，（比如：通过一个人的性格、身高、是否抗冻、普通话等级等，来判断一个人是北方人还是南方人，这里有四个特征，两个标签），而在自动组方中，如果把主治症状作为药方的特征，最终预测的标签不能是药方，因为数据集中的药方只对应唯一的一组症状，无法进行训练分类。<br>
&emsp;&emsp;中医的诊断过程是，通过望闻问切四诊信息，推出病人的证型，进而考虑治法，最后给出药方或者药物剂量。对比我们的药方数据，中间缺失了证型的信息，而如果进行分类算法，证型应该适合作为标签。<br>
&emsp;&emsp;复杂系统熵聚类算法解决的就是这个问题，如果能够把若干症状聚类为证型，之前的<症状>--<药方>这种对应关系就可以展开为<症状>--<证型>--<药方>这样的对应关系，为之后的药方推荐做一个基础。<br>
#### 具体步骤：
主文件prescript_cluster.py中，进行了简单的过程注释，现在这里详细说明一下：<br>
**预处理：**
1.






[1]:https://baike.baidu.com/item/%E5%A4%8D%E6%9D%82%E7%B3%BB%E7%BB%9F%E6%96%B9%E6%B3%95%E5%AD%A6%E4%B8%8E%E4%B8%AD%E5%8C%BB%E8%AF%81%E5%80%99%E5%BB%BA%E6%A8%A1/2572271
[2]:http://www.wanfangdata.com.cn/details/detail.do?_type=degree&id=Y1625412


