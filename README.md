#一.题目背景#
###1.数据
2000条口碑商店的信息，6900多万条交易数据，550多万条浏览数据；  
user_pay表记录了用户在各商家进行线下消费的情况，不包含线上支付；    
user_view表记录了口碑平台上各商家的线上浏览记录；  
###2.目标
根据已有数据训练回归模型，预测各商家在特定14天内的客流量（线下交易量）；   
#二.建模
##（一）对单个商家进行建模##
###1.数据
先只使用user_pay的交易数据和天气数据，尝试不同的回归模型；以商店1862为例进行尝试；   
####2.特征
输入：日期信息（周几、是否为公共节假日）、天气情况（温度，下雨）；   
输出：日流量；   
###3.问题
* 训练数据的选取：商家的运营情况存在增长期和稳定期，即使在稳定期也会存在异常值；暂时从稳定期开始选取，且去除异常值，但千万条数据没法都手动选取稳定期；     
* 数据的转化：数据特征中存在汉字，如下雨、晴等；是否可以用湿度衡量？但没有湿度的数据；

##（二）对全国的商家进行统一建模
建立全国性的模型时候需要考虑各个商家的信息；但商家的特征中存在汉字；  

#三.SVR程序说明#
###1.实现
对单一商家（ID：1862），进行数据处理，建模，预测   
###2.主要内容
+ 处理后的支付信息和天气数据存于文件'1862_pay_Info.txt'和'1862_weather.txt'中；   
+ 分析数据，从流量的稳定期开始选择训练数据，对于稳定期中存在的流量异常值，在SVR中尝试引入异常值的处理（‘outlierfraction’）；  
+ 以星期几、最高温度、最低温度作为输入，以流量为输出，训练线性回归和SVR模型（选择rbf核，归一化等参数）；  

###3.结果
线性回归的loss为0.1左右，SVR的loss为0.05左右    

-By cjh    
20170121
