## 古典密码

#### 替换密码
http://quipqiup.com/

#### 维吉尼亚密码
* 解密工具
    * https://www.mygeocachingprofile.com/codebreaker.vigenerecipher.aspx 


#### Playfair
###### 原理 
Playfair 密码（Playfair cipher or Playfair square）是一种替换密码，1854 年由英国人查尔斯 · 惠斯通（Charles Wheatstone）发明，基本算法如下：

1. 选取一串英文字母，除去重复出现的字母，将剩下的字母逐个逐个加入 5 × 5 的矩阵内，剩下的空间由未加入的英文字母依 a-z 的顺序加入。注意，将 q 去除，或将 i 和 j 视作同一字。
2. 将要加密的明文分成两个一组。若组内的字母相同，将 X（或 Q）加到该组的第一个字母后，重新分组。若剩下一个字，也加入 X 。
3. 在每组中，找出两个字母在矩阵中的地方。
    * 若两个字母不同行也不同列，在矩阵中找出另外两个字母（第一个字母对应行优先），使这四个字母成为一个长方形的四个角。
    * 若两个字母同行，取这两个字母右方的字母（若字母在最右方则取最左方的字母）。
    * 若两个字母同列，取这两个字母下方的字母（若字母在最下方则取最上方的字母）。
新找到的两个字母就是原本的两个字母加密的结果。

以 playfair example 为密匙，得

```
P L A Y F
I R E X M
B C D G H
K N O Q S
T U V W Z
```
要加密的讯息为 ```Hide the gold in the tree stump```

```HI DE TH EG OL DI NT HE TR EX ES TU MP```
就会得到

```BM OD ZB XD NA BE KU DM UI XM MO UV IF```
>工具 
CAP4

#### Polybius
###### 原理 
Polybius 密码又称为棋盘密码，其一般是将给定的明文加密为两两组合的数字，其常用密码表
```
1	2	3	4	5
1	A	B	C	D	E
2	F	G	H	I/J	K
3	L	M	N	O	P
4	Q	R	S	T	U
5	V	W	X	Y	Z
```
举个例子，明文 HELLO，加密后就是 ```23 15 31 31 34```s。

#### 培根密码
特点：
* 只有两种字符
* 每一段的长度为 5
* 加密内容会有特殊的字体之分，亦或者大小写之分。

#### 栅栏密码
原理：栅栏密码把要加密的明文分成 N 个一组，然后把每组的第 1 个字连起来，形成一段无规律的话。
本质上就是置换密码

#### 曲路密码
原理曲路密码（Curve Cipher）是一种置换密码，需要事先双方约定密钥（也就是曲路路径）
![曲路密码](picture/曲路密码.PNG)

#### 列移位加密
本质上也是置换密码

#### 01248密码(云影密码)
该密码又称为云影密码，使用 0，1，2，4，8 四个数字，其中 0 用来表示间隔，其他数字以加法可以表示出 如：28=10，124=7，18=9，再用 1->26 表示 A->Z。

#### JSFuck
JSFuck 可以只用 6 个字符 []()!+ 来编写 JavaScript 程序。
> 工具 
JSFuck 在线加密网站 http://www.jsfuck.com/

#### BrainFuck
Brainfuck，是一种极小化的计算机语言
> 工具
https://www.splitbrain.org/services/ook

#### 猪圈密码
#### 舞动的小人密码
这些密码本质上是以一些符号代替英文字母，只要把英文字母替换上去就可解密，实质上可以使用词频分析

#### 键盘密码
所谓键盘密码，就是采用手机键盘或者电脑键盘进行加密。
##### 手机键盘密码
手机键盘加密方式，是每个数字键上有 3-4 个字母，用两位数字来表示字母
##### 电脑键盘棋盘
电脑键盘棋盘加密，利用了电脑的棋盘方阵
##### 电脑键盘坐标
电脑键盘坐标加密，利用键盘上面的字母行和数字行来加密
##### 电脑键盘 QWE
电脑键盘 QWE 加密法，就是用字母表替换键盘上面的排列顺序
##### 键盘布局加密
简单地说就是根据给定的字符在键盘上的样子来进行加密。
> 例：密文：```4esxcft5 rdcvgt 6tfc78uhg 098ukmnb```。试着在键盘上按照字母顺序描绘一下，可得到 ```0ops``` 字样

### 解题技巧
1. 如果遇到一段无脑的密文然后没有任何的提示，那么考虑替换密码，代换密码，哈希函数，直接上破解网站进行破解
2. 遇到给定的.py文件的题目，首先需要分析其主要运用的加密逻辑，与古典密码进行比较，若是一种新提出的方案，一般都会给出足够的信息作为突破口。


## 流密码

#### 伪随机数生成器PRNG

##### 随机性的严格性 
* 随机性：随机数应该不存在统计学偏差，是完全杂乱的数列。
* 不可预测性：不能从过去的序列推测出下一个出现的数。
* 不可重现性：除非数列保存下来，否则不能重现相同的数列。

#### 码安全伪随机数生成器

#### 例题：woodman - Google CTF
```py
class SecurePrng(object):
    def __init__(self):
        # generate seed with 64 bits of entropy
        self.p = 4646704883L
        self.x = random.randint(0, self.p)
        self.y = random.randint(0, self.p)

    def next(self):
        self.x = (2 * self.x + 3) % self.p
        self.y = (3 * self.y + 9) % self.p
        return (self.x ^ self.y)
```
目标是要求出前100个随机数。
前面几个随机数很容易就可以知道，假设是sol1和sol2，因此可以写出相应的表达式，然后由于相乘的系数只为2和3，因此实际上求模的时候最多只会减去3个p，因此可以通过枚举减去的p的数量来猜测x0和y0的值。这里只要找出了两个明文就可以把x0和y0恢复出来。

> 首先需要模拟x和y模p是减去p的个数kx，ky

> 对于每一个候选比特串tx，都枚举0和1表示当前的第i bit，记为bi；把枚举出的bi添加到候选比特串的第i位中。然后把tx和sol1进行异或求出另一个比特串ty，再把tx和ty代入随机数生成的函数中(模p就使用减去kx和ky表示)，并把结果进行异或得到guess2，把guess2的低i位与sol2的低i位进行比较，如果相等，那么就把tx加入新一轮的候选，第i轮结束后，使用新一轮的候选覆盖第i轮的候选作为第i+1轮候选。

> 以此类推，直到所有bit都选择完毕，这样一来用最后剩下的候选进行测试，


#### 反馈移位寄存器
![反馈移位寄存器.jpg](picture/反馈移位寄存器.jpg)
* $a_0, a_1, ... , a_{n-1}$位初态
* F 为反馈函数或者反馈逻辑。如果 F 为线性函数，那么我们称其为线性反馈移位寄存器（LFSR），否则我们称其为非线性反馈移位寄存器（NFSR）。
* $a_{i+n} = F(a_i, a_{i+1},...,a_{i+n-1}$

##### 线性反馈移位寄存器 - LFSR

##### B-M 算法 (一种求解线性反馈移位寄存器的算法)

#### 非线性反馈移位寄存器
* 非线性组合生成器，对多个 LFSR 的输出使用一个非线性组合函数
* 非线性滤波生成器，对一个 LFSR 的内容使用一个非线性组合函数
* 钟控生成器，使用一个（或多个）LFSR 的输出来控制另一个（或多个）LFSR 的时钟
代表 Geffe