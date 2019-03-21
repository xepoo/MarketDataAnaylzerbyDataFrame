# MarketDataAnaylzerbyDataFrame
A tool as Data Analyzer for commodity or stock by DataFrame 

1. 定义了一个类DataAnalyzer初始化的时候需要输入生成csv文件导出文件夹地址，和数据格式

1.1 方法db2df，输入vnpy使用行情数据库信息和读取品种信息，程序读取vnpy的指定评到指定开始到结束时间段的分钟k线数据；按照初始化格式返回生成DataFrame供分析；如果expeort2csv为True的话，会生成一个csv文件到指定地址

1.2 方法csv2df，输入指定路径的csv行情文件；程序读取csv文件；按照格式返回生成DataFrame供分析；如果expeort2csv为True的话，会生成一个csv文件到指定地址。把导入的字符串转换datetime格式，此时可能会有warning信息。

1.3 方法df2Barmin，输入DataFrame格式1分钟行情数据，和指定输出分钟k线，程序整合出对应分钟k线数据。比如输出1分钟行情数据csv，要求输出5分钟k先数据；程序输出5分钟K线信息DataFrame供分析。这里有点地方要注意，如果数据中一天开始第一个bar是9点，那么crossmin为1; 如果第一个是9点1分，此处为0。如果expeort2csv为True的话，会生成一个csv文件到指定地址。

1.4 方法dfcci，其实是一个示例方法，输入DataFrame格式分钟行情数据，和参数cciWindows，程序调用talib的cci方法，进行计算。返回带有新的一列cci数据的DataFrame。用来分析。如果expeort2csv为True的话，会生成一个csv文件到指定地址。打开就是这样一个东西。

2. 通过类的方法，读取一个rb1905行情数据，按照聚合出5分钟K线，在按照cci周期为15条K线计算cci值

2.1 画出cci的柱状分布图，CCI（Commodity Channel lndex）顺势指标是测量股价是否已超出常态分布范围的一个指数，波动于正无限大和负无限小之间。如下图x轴是cci值，y轴是出现次数。从图中可以看出cci数据是两个正太分布叠加，波峰在-80和＋80两个值，正负200之后，cci出现就变的很少，此时可以用DataFrame的数字分析功能找到更多数据。

2.2 计算每个时间点的当前价格，和之后第5根K线结束价格差，和cci的值做成散点图，

2.3 cci值在正负（100-200）区间，和（200-300）区间算是出现比较少，计算在这个区间出现时，之后第2，第4，和第6根K线结束价格增多还是减少概率