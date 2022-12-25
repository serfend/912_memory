## 数据结构

### 1. 复杂度的计算

三种时间复杂度符号 大于$\Omega$ 等于$\Theta$ 小于$O$

#### 大师理论：

分治策略通常类似 $ T(n)=a·T(\frac{n}{b}) + O(f(n)) $ ，即将原问题分治成a个规模为$\frac{n}{b}$的子问题，`子问题的解`合并起来需要f(n)

估算方法主要看$n^{log_ba}·log^kn$ 与 f(n) 大小。看前面和后面谁大，取大的。如果一样大则多乘一个$log^{k+1}n$，k通常为0。

正因为a和b是底数关系，所以有$a^K$要对应$b^K$，即$T(n) = a·T(\frac{n}b)$等价于$T(n) = a^K·T(\frac{n}{b^K})$，举例： $f(n) = 3T(n/9) = 3^2T(n/9^2)=...=3^kT(n/9^k)$，令$n=9^k$将n消去，即有$f(n)=\sqrt{n}T(1)=O(\sqrt{n})$。

**![image-20221110092447375](https://raw.githubusercontent.com/serfend/res.image.reference/main/image-20221110092447375.png)**

1. [2022.912.1]

   $[logn]! = O(nloglogn)$

   错误。两边取对数，$log([logn]!)$ ， $logn + logloglogn$。

   $ \Theta(logn + logloglogn)$ = 

   而$log([logn]!)$ =$ \Theta(logn · loglogn)$，故左侧更高阶

2. [2021.912.1]

   从渐进意义上讲 $f(n)=2^{log^2n}$与$g(n)=n^{2020}$哪个增速更快，为什么？

   取对数$log(f(n)) = log^2n · log2$ ，$log(g(n)) = 2020 · log(n)$

   而logn > C，故f(n)更快

3. [2021.912.2]

   $f(n)=3(f(\frac{n}9)+O(1))$ 则从O记号的角度来讲，属于什么复杂度。

   因为$f(n)+O(1)=3(f(\frac{n}9+O(1)))=3^2(f(\frac{n}{9^2}+O(1)))=3^k(f(\frac{n}{9^k}+O(1)))$。

   令n=$9^k$=> $f(n)=3^k(f(1)+O(1))=O(3^k)=O(\sqrt{(3^k)^2})=O(\sqrt{n})$

4. [2020.912.1]

   $log^nn = \Theta(n^{logn})$

   错误。两边同时取对数，则有n · logn = logn logn，显然左边大于右边，故应为$log^nn = \Omega(n^{logn})$

5. 

### 2. 向量



### 3. 列表

1. [2020.912期末.7]

   在本课的学习中，曾出现过许多利用几何分布（算法执行到下一步停止的概率p）进行计算的实例，请举出4处并简要说明之。

   跳转表塔高，二叉堆上滤，快排pivot，字符串蛮力算法。

#### 邻接矩阵

1. [2022.912.13]

   矩阵压缩，一个 50*50 的对称矩阵 a[0, 49] [0, 49]，每个数据占两个数据位，行优先的前提下压缩到矩阵下三角，a\[0\]\[0\]起始下标对应的是十进制的 1000，a\[i\]\[j\]的地址是 2000（i<=j）， 则 i= _____ ; j =_____ 。

   i=4 j=31。行优先存储，且每个数据占2个数据位，开始位置为1000，目标位置为2000。故有： 目标位置是第 $ A = \frac{1000}2 +1  = 501$ 个元素。而从第0行到第i-1行元素个数分别为1,2,..,i个（因为题意是下三角），共有 $ S = \frac{(i+1)i}2 $ 个数据，而S<=A，即有i=31（S = 496），j = A - S = 501 - 496 = 5，j=4。同时行数<=列数，而根据题意i<=j，故i=4 j=31。

2. 

#### 快速排序

复杂度 最好和平均都是$T = O(nlogn)$

设置一个轴点，不断将小于它的数往前丢，大于它的数往后丢。因为不论原数组是否有序，都要这么干一遍，所以最好情况也是O(nlogn)

#### 选择排序

复杂度  $ T = O(nlogn)$，最坏情况 $ T = O(n^2) $

逆序数越多，排序消耗的时间越长，故后面会提到希尔排序来减少逆序数的交换次数。

1. [2020.912期末.2]

   对2020个数进行排序，只考虑swap，问最坏情况下至少需要交换多少次。

   2019。每次交换循环节最多+1。最坏情况考虑错排序列（比如5个元素，即54321，变成12345），一开始循环节为1, 排序完成后循环节为2020, 因此最少需要交换2019次。循环节指一个序列中从数当前位置到排序完成后位置是数当前位置的最小个数（没理解）

2. 

#### 归并算法

> 总复杂度$ T = O(nlogn) $
>
> 二路归并$ T = O(n) $
>
> 优势是排序很稳定（即不会因为排序导致同样大小的项之间顺序变乱），也方便顺序读取（适合分布式分发任务）。

1. [2022.912.2] / [2019.912.2]

   有序向量二路归并能在线性时间内完成，有序列表不能在线性时间完成。

   错。有序列表和有序向量的归并都在O(n)时间内完成

2. [2020.912.14] / [2019.912期末.11] / [2014.912期末2.14]

   底层算法不稳定的情况下，基数排序的结果（必然/未必）正确，（稳定/不稳定）。

   未必；不稳定。基数排序是指将所有待比较数值（自然数）统一为同样的数位长度，数位较短的数前面补零。然后，从最低位开始，依次进行一次排序。这样从最低位排序一直到最高位排序完成以后, 数列就变成一个有序序列。而当底层不稳定时，会导致一组数的顺序变动，从而结果可能错误。

3. 

#### 希尔排序 ShellSort


$$
\bold{Papernov-stasevic序列：}
\newline间隔 = 2^n-1
\newline T = O(n^{\frac32})
\newline
\newline \bold{Pratt序列：}
\newline 间隔 = 2^p3^a (2和3的倍数)
\newline T = O(nlog^2n)
\newline
\newline \bold{Sedgewick序列：}
\newline 间隔 = 9·4^k + 1 或4^k - 3·2^k+1
\newline 最坏复杂度T = O(n^{\frac43})
\newline 平均复杂度T = O(n^{\frac76})
$$


1. [2022.912.9]

   希尔排序序列是{0, 1, 3, 7, 15, …, 2^(k-1), …}，时间复杂度是 O(n^(3/2)) 。

   正确。这是Papernov-stasevic序列，时间复杂度为O(n^(3/2)) 这是邓公书中结论之一，在P355中。

   ![image-20221109090819243](https://raw.githubusercontent.com/serfend/res.image.reference/main/imgimage-20221109090819243.png)

2. 

#### K选取

[K选取参考文档](https://blog.csdn.net/u012604810/article/details/81430705)即选取前K个数（第K小或第K大的数）。

- 简单想法：目标进行快速排序，复杂度$O(nlogn)$

- 划分法：复杂度${O(n)}$quicksort的基础就是对数组进行划分，选取一个轴点(主元),使得比轴点大的数位于左侧，比轴点大的数位于右侧。

  > 其实就是不断移动轴点，每次移动都会让轴点左侧的数严格小于轴点，从而经过平均logn次移动选出第k小

  - 可以对数组进行划分，当轴点位置等于k-1时，正好找到第k小的元素；若轴点位置比k-1小，说明，第k小的元素在该轴点的右侧；反正在轴点的左侧。
  - 过程中划分通过快排来移动轴点，时间复杂度T(high-low) 
  - 将轴点依次向中心移动，复杂度O(logn)
  - 故总体复杂度T = $1 * T(n/2) + O(n) = O(n)$

1. [2020.912期末.6]

2. quickselect(A,k)中，给定n个数并随机置乱得到（无序）数列$\{a_1,a_2..,a_n\}$：

   (1) $a_i$与$a_j$进行比较的概率（表达式用n,i,j,k这些参数表示） 

   (2) $a_i$与$a_j$比较次数的期望

   (3) ？

   

   (1) 交换次数依赖于k的大小，概率 $P = \frac{2}{大数-小数+1}$ ，例如 i<j<k时 $ P = \frac{2}{k-i+1}$ ，i=k时 $P=\frac{2}{j-i+1}$

   (2) 期望比较次数E(n) = (n-1) + $\frac2n · \sum_{k=\frac{n}2}^{n-1}4k \le (n-1) + 3n \le 4n $

3. [2020.912.9] / [2014.912期中.3]

   存在CBA式算法，能够在O(n)的时间内从n个无序整数中找到最大的10%。

   正确。等价于找到前10%的轴点。实际上，只要不对选取的结果排序，那么选取k个的时间就是O(n)。

   



### 4. 栈和队列

1. [2014.912期中.10]

   字符串"123XY"中的字符经栈混洗之后，可得到()个合法的C++变量名(比如"YX321")

   5。栈混洗就是将字母放到前面，剩下的字母依次在后面不同的位置固定。然后其他字符的顺序变填充进去。YX321，XY321，X3Y21，X32Y1，X321Y共5个。

#### 逆波兰表达式

##### 算法核心：

操作符优先级：`(` `)`  <  `+` `-`  < `*` `/`  < `^` < `!` （和传统认知的优先级一致）

- 操作数直接入栈
- 运算符，查看栈顶运算符
  - 小于当前字符的运算符，当前运算符入栈
  - 大于当前字符的运算符，弹出栈顶操作符和2个操作数运算（如果是`!`则弹出1个）

**![image.png](https://raw.githubusercontent.com/serfend/res.image.reference/main/1636097977226-b1591e1c-b8df-47f1-89eb-39a3cc88c1ef.png)**



##### 逆波兰表达式的优势

- 逆波兰表达式相较于中缀表达式不用比较算数符优先级，所以计算效率比较高
- 为什么要转换：因为一个表达式可能需要做相同的多次求值（比如在一个循环里面），那么转换成逆波兰表达式只需要一次，后面计算就可以都用逆波兰表达式求值了，所以效率比较高



1. [2020.912.16]

   对于逆波兰表达式 0!1+23!4+^56!78!【X】/-9+的值为2017，则【X】处的符号为

   A.加号 B.减号 C.乘号 D.除号

   D。按优先顺序依次入栈计算。可以发现7和8后面有两个【!】操作符，意味着第四个一定是除号，否则数值将会因这两个阶乘，变得无比之大，故为D。

2. [2016.912.11]

   设计一个算法，把一个中序遍历ABCD-*+EF??(后面三个符号忘记了不过不重要)构造成如下图所示的二又树

   **![image-20221209214725015](https://raw.githubusercontent.com/serfend/res.image.reference/main/imgimage-20221209214725015.png)**

   a)描述算法思想 b)伪代码实现

   a) 创建一个栈，按中序序列遍历，发现操作数则入栈，发现操作符则取出栈顶两个元素组成双分支节点随后入栈，最终栈中的元素即为所求值。

   b)

   ```cpp
   BinNode* build(string s){
       stack<BinNode*> op;
       for(int i=0;i<s.size();i++){
           BinNode* node = new BinNode(s[i]); // 对每个元素
           if(s[i]>='A' && s[i]<='Z'){
               // 如果是操作符，将该节点的左右子树设置为栈顶两个元素
               node->lc = op.pop();
               node->rc = op.pop(); 
           }
           op.push_back(node); // 将该节点入栈
       }
       return op.pop();
   }
   ```

3. [2011.912期中.18]

   考察表达式求值算法。算法执行过程中的某时刻，若操作符栈中的括号多达2010 个，则此时栈的规模（含栈底的’\n’）至多可能多达？试说明理由，并示范性地画出当时栈中的内容。

   

   8045。4*n+5。栈中的内容是 \0 + \*^(+\*^(+...(+\*^ ! ，四种不同优先级的从小到大依次摆放，故每个括号最大对应4个元素。每个括号的右侧+第一个括号的左侧4个，以及表达式最后的阶乘，共有4n+4+1=4n+5个。

4. [2014.912期中.19]

   表达式`(0!+1)*2^(3!+4)-5/(6!/7!)-8+9)`对应的RPN为

   

### 5. 二叉树

1. [2016.912期末.25]

   以下数据结构，在插入元素后可能导致O(logn)次局部结构调整的是()
   A.AVL B.B-树 C.红黑树 D.伸展树 E.以上皆非

   BD。A和C都是O(1)，avl插入元素失衡后调整就复原，不会传播，删除才有可能是O(logn)；而红黑树无论插入还是删除元素局部结构调整都是O(1)，重染色才可能是O(logn)。





1. [2022.912.5]

   无向图从顶点s进行dfs得出的二叉树，s的出度为1，则s必定不是关节点。

   正确。s此时是树根，树根要是关节点，当且仅当有两个或两个以上的儿子，即树根度≥2。因此s不可能是关节点。

2. [2022.912.10]

   一棵伸展树经过访问后，节点被转换到根部，树的高度不一定降低 。

   答案：正确。伸展树经过访问后，树高可能降低，可能升高，也可能不变。举例真二叉树变高；变低和不变的显然易举例。

3. [2022.912.15]

   由关键码{0, 1, 2, …, 10}组成，且所有节点都是偶数度的二叉搜索树，共有____棵。

   42棵。节点是偶数度，故为真二叉树。2n+1个节点（或n+1个叶子节点）组成的真二叉树有$ Catalan(n) =  \frac{C_{2n}^n}{n+1}$个，即2n+1=11，n=5，Catalan(5)=42。

   > 这里因为是二叉搜索树，所以每一种情况的真二叉树中序遍历是一样的，并不需要进行再次分类讨论，如果这道题是真二叉树，那么还需要乘一个11的阶乘，即答案为42乘11!
   >
   > 2n+1个节点的真二叉树，有Catalan(n)种结构，由于“节点无差别”或者“二叉搜索树”的限制，每个节点数值都是固定的，所以不同的结构数就是二叉树的棵树

4. [2022.912.19]

   已知任何一棵多叉树可以通过长子-兄弟法表示为二叉树，二叉树的层次遍历法也可用于多叉树，现给出二叉树节点定义如下:

   请设计如下要求的遍历函数，并配合必要的注释:

   ```cpp
   struct BinNode{
   	int data;
       BinNode *lc;
       BinNode *rc;
   };
   void traverse(BinNode *x) {
   	//x是二叉树T的根节点，T对应了一棵多叉树M的长子-兄弟表示法
       //要求输出全部节点的数值，遍历次序等价于M的层次遍历次序    
       //不可以使用递归，也不可以改变T的结构
   	//不得使用队列和栈以外的辅助数据结构
       //时间和空间复杂度皆为O(n)，n为节点数量
   }    
   ```

   说明该算法的原理证明该算法的正确性证明该算法的时间、空间复杂的为O(n)。

   解：长子兄弟表示法，即节点的左节点为长子，右节点为兄弟。该层次遍历为访问时先将下一层的长子入列后，再遍历当前队列所有节点。

   ```cpp
   #include<Queue>;
   void traverse(BinNode *x) {
       Queue<BinNode> Q;
   	Q.push(x); // 初始化队列
       while(!Q.empty()){
           BinNode x = Q.pop();
           while(x){
               if(x->lc) Q.push(x->lc); // 将长子入列
               printf("%d",x->data); // 将当前节点所有的兄弟（右节点）遍历
               x = x->rc;
           }
       }
   }  
   ```

   

   ```mermaid
   graph TB
   0((根));1((1层长子));2((1层兄弟));3((2层长子));4((2层长子));6((2层兄弟));7((3层长子));10((2层兄弟));
   1 --> 3;1 --> 2;2 --> 4;3 --> 7;3 --> 6;2-->10;0-->1;
   ```

   

5. [2021.912.7]

   找出一个二叉搜索树

   ```cpp
   struct BstNode{
   	int size,key;
       BinNode *lc;
       BinNode *rc;
   };
   int count(BstNode *T,int lo,int hi) {
   	// 通过伪代码实现算法
       // 计算lo与hi之间所有节点的数目
       // 要求时间复杂度O(h)，空间复杂度O(1)
   }    
   ```

   (1) 写出算法主体

   (2) 给出算法原理并说明正确性

   (3) 证明你的算法符合时间空间复杂度要求

   

   (1) 

   ```cpp
   int count(BstNode *T,int  lo,int hi){
       BstNode node_lo = search(lo);
       BstNode node_hi = search(hi);
       BstNode common_anscestor = LCA(node_lo,node_hi);
       int result = 0;
       BstNode cur = common_anscestor->lc;
       while(cur!=node_lo){
       	if(cur->rc)result += cur->rc->size;
           cur = cur->lc;
           result++;
       }
       cur = common_anscestor->rc;
       while(cur!=node_hi){
           if(cur->lc)result += cur->lc->size;
           cur = cur->rc;
           result++;
       }
       return result + 1;
   }
   ```

   (2) lo和hi之间所有的节点个数，就是他们到他们共同父节点之间包含的节点数。lo与hi之间的节点数目是从lo和hi的共同祖先到他们之间所有的节点。故步骤为：

   1. node_lo = search(lo),node_hi = search(hi) // 根据数值搜索对应的节点
   2. common_ancestor = LCA(node_lo,node_hi) // LCA为逐个遍历父节点，直到发现两个节点遍历到同样的节点，该节点为共同祖先。
   3. node_lo_count = current->rc?->size + 1 + lo_count(current->lc); // 内侧节点个数 以及自己 以及外侧继续遍历
   4. return result + 1; // 加上共同祖先这一个节点

   (3) Search到目标节点每轮都会深入一层，使得h+1，T = O(h)

   获取共同祖先因仅判断当前节点是否一致，使得h-1，且最多判断到根节点，T = O(h)；

   遍历两侧每轮都会深入一层，使得h+1，故T = O(h)

   故总复杂度为 T = O(h)

   

   

6. [2022.912期末.1]

   在一个二叉树中，每个节点只记录了父亲节点指针。请设计一个算法找到任意两个节点x和y的最近公共祖先 LCA，

   要求:

   - 时空复杂度均不超过 O(depth(x) + depth(y))
   - 如果一个节点为 NULL，则返回另一个节点
   - 允许使用基本数据结构
     请写出思路、关键技巧与算法伪代码描述

   ```cpp
   Node *lca(Node *x,Node *y){
       if(!x)return y;
       if(!y)return x; // 如果一个节点为 NULL，则返回另一个节点
       stack<Node *>linkx,linky; // 允许使用基本数据结构
       while(x){linkx.push(x);x=x->parent;} // 将xy的路径分别记录到栈中
       while(y){linky.push(y);y=y->parent;}
       // 该两个栈中必然存在公共部分，至少是根节点，两个栈的顶端必然都是根节点
       Node* result;
       while(!linkx.empty()&&!linky.empty()){
       	x = linkx.pop();
           y = linky.pop();
           if(x!=y)break;
           result = x; // 如果两者相等 则仍是公共祖先
       }
       return result;
   }
   ```

   

7. [2022.912期末.2]

   - 在一个二叉树中，每个节点**只记录了左右孩子指针**。
   - 请设计一个算法找到任意两个节点x和y的通路，要求:
     - **从给定的根节点r出发**
     - 时间复杂度不超过O(n)
     - 不允许使用其他数据结构
     - 为了简化题目，只要求输出通路上所有的点，对输出顺序无要求
   - 请写出思路、关键技巧与算法伪代码描述

   

   因为只给了左右孩子，故只能是先遍历到左右孩子相对位置，过程中检查两者搜索是否是lca，时间复杂度O(n)。（如果有更多信息比如二叉树的data或parent的话，可以通过搜索方法降低到O(logn)）

   ```cpp
   /*
   从根节点出发，输出两个孩子的通路
   @params Node* p 父节点
   @params Node* x 孩子A
   @params Node* y 孩子B
   */
   bool PrintPathTo(Node* p,Node* x,Node* y){
       if(p==NULL)return false;
      	bool is_child =(p==x||p==y); // 判断当前是否已到孩子节点
       if(is_child){
           p->print();
           return true;
       }
       bool has_child = PrintPathTo(p->rc,x,y); // 判断子层级是否有目标
       has_child = PrintPathTo(p->rc,x,y) || has_child; // 防止出现 或关系 而被提前结束
       if(has_child)p->print();
       return has_child;
   }
   ```

   

8. [2020.912.21]

   A,B,C,D和F都是3分每题，E为5分

   struct BinNode{// 二又树节点
   BinNodePosi(T) lc;
   BinNodePosi(T) rc;
   int size;

   }

   Binode的定义大致如上
   A.n个节点的完全二又树左子树的规模为___，请给出递推公式
   B.给出A的伪代码实现
   C.中序遍历序列第k个节点
   D.splayto(a, x)，a为x的祖先，通过zigzag操作将x调整变为a的孩子，若a为NULL，x调为根节点

   E.给出将一棵树转化为完全二叉树的算法(时间复杂度O(nlogn)，递归深度不超过O(logn))
   F.证明你的算法可以达到复杂度和迭代深度的要求

   

   A. 完全二叉树，所以高度=h(满二叉树) + 如果有余数则+1，且h=[${log_2}^n$]。设此二叉树最后一层节点数为a，则有a=n-2^(h-1)。左子树规模为2^(h-1) - 根节点1 + min(a,左子树最后一层满树的情况2^(h-1)) = 2^(h-1) - 1 + min(a,2^(h-1)) = 2^(h-1) - 1 + min(n-2^(h-1),2^(h-1))

   B. 

   ```cpp
   int left_count(int n){
       int height = Math.ceil(Math.log(2,n));
       int last_level = n - Math.pow(2,height-1);
       int last_level_left = Math.min(last_level,Math.pow(2,height-1));
       int left_child = Math.pow(2,height-1) - 1;
       int result = left_child + last_level_left;
       return result;
   }
   ```

   C. 中序遍历，则是从左到右依次遍历的，故可以比较k是当前位置的左边还是右边，递归。

   ```cpp
   BinNodePosi(T) searchK(BinNodePosi(T) root,int k){
       if(k==1&&!root->lc)return root; // 边界
       int offset = k - root->lc->size - 1; // 判断目标在当前的左边还是右边
       if(offset==0)return root; // 目标就是当前
       else if(offset<0)return searchK(root->lc,k); // 目标在当前左边，则序号不变
       return searchK(root->rc,offset); // 目标在当前右边，则减掉左侧及当前节点，往右边看
   }
   ```

   

   D.splayto函数实现，因为a为x的祖先，故a不可能是NULL，如果是NULL则二叉树不合法

   ```cpp
   void splayto(BinNodePosi(T) a,BinNodePosi(T) x){
       if(a==x->parent)return;
       if(a==x->parent->parent){
           // a是x的直接祖先
           if(x==x->parent->lc){
               // 如果x是其父亲的左孩子
               zig(p);
               return;
           }
           zag(p);
           return;
       }
       // 否则则需要先通过zigzag将x上移到其直接祖先的位置，旋转时先注意先后
       if(x==x.parent.lc && x.parent == x.parent.parent.lc){zig(g);zig(p);}
       else if(x==x.parent.lc && x.parent != x.parent.parent.lc){zig(p);zag(g);}
       else if(x!=x.parent.lc && x.parent == x.parent.parent.lc){zag(p);zig(g);}
       else {zag(g);zag(p);}
       splayto(a,x); // 然后继续向上检查
   }
   ```

   

   

   

9. [2020.912期末.5]

   **![image-20221110153018769](https://raw.githubusercontent.com/serfend/res.image.reference/main/image-20221110153018769.png)**

   判断同构：两课树可以通过有限次`交换左右子树`变为同一棵树。

   ```cpp
    //判断两棵树是否同构
    int Isomorphic(Ptree t1,Ptree t2){
   	 if((t1==NULL)&&(t2==NULL))return 1;//都为空
   	 if(((t1==NULL)&&(t2!=NULL))||((t1!=NULL)&&(t2==NULL))) return 0;//一个为空另一个不为空
   	 if(t1->data!=t2->data) return 0;//根节点的值不一样
   	 if((t1->lchild==NULL)&&(t2->lchild==NULL)) return Isomorphic(t1->lchild,t2->rchild);
   	 if(((t1->lchild!=NULL)&&(t2->lchild!=NULL))&&(t1->lchild->data==t2->lchild->data))//没有交换 
   		 return (Isomorphic(t1->lchild,t2->lchild)&&Isomorphic(t1->rchild,t2->rchild));//如果两个都不为空且左儿子相等，应该递归的找左对应左，右对应右
   	 else
   		 return (Isomorphic(t1->lchild,t2->rchild)&&Isomorphic(t1->rchild,t2->lchild));//否则就是交换了，递归的判断左对应右，右对应左
    
    };
   ```

   (1) 从根节点开始递归判断两边的树是否同构

   (2) 检查空集；检查根节点；检查两边的树是否交换；递归进入两边的子节点；

   (3) 不难看出，每个层级都相应一致，每个子层级都会被对应考虑，故所有情况都已被考虑。

   

10. [2020.912.17]

   对于叶节点为（）的真二叉树，其数量等于2018对括号所组成的合法表达式数量。

   2019。n个括号组合的个数、n个进栈出栈的种数、n+1个叶子节点、2n+1个节点的二叉树的形状数等，都属于卡特兰数，符合通项$ \frac{C_{2n}^{n}}{n+1} $。记作Catalan(n)。

11. [2019.912.5]

    对于⼆叉树，通过先序遍历和后序遍历不能确定其层次遍历。

    错。先序中序/后序中序可以确定唯一一棵二叉树。先序后序因为无法确定单分支节点是左孩子还是右孩子故无法唯一确定二叉树，但是层序遍历不需要确定单分支是左还是右，故可以直接确定。

    ```javascript
    function pre_post_to_level(pre,post){
        const result = []
        const to_run = []
        to_run.push([pre,post])
        function run(pre,post){
            const left = pre[0]
            const right = post[post.length-1]
            if(!left && !right)return 
            result.push(left)
            // 单节点仅递归一边的即可
            if(left===right)return to_run.push([pre.slice(1,pre.length),post.slice(0,post.length-1)])
            result.push(right)
            const left_index = post.findIndex(x=>x===left)
            const right_index = pre.findIndex(x=>x===right)
            to_run.push([pre.slice(1,right_index),post.slice(0,left_index)])
            to_run.push([pre.slice(right_index+1,pre.length),post.slice(left_index+1,post.length-1)])
        }
        while(to_run.length){
            const i = to_run.shift()
            run(i[0],i[1])
        }
        return result 
    }
    
    const pre = '124758936'.split('')
    const post = '749852631'.split('')
    const result = pre_post_to_level(pre,post)
    console.log(result.join('') === '123456789')
    ```

    



#### 哈夫曼编码

将待编码的字符频率从小到大排序，每次都取出最小的两个数作为一个二叉树左右节点，并把它们的频率加起来，作为这个二叉树新的频率重新放到排序中，重复以上步骤。

1. [2020.912.18]

   9个字符出现频率分别为0 1 1 2 3 5 8 13 21，其哈夫曼编码最大长度为___

   8。构造树，发现就是一个单链树，然后从上往下数长度（如果只有一个根，长度为0，即从0开始数），共有8。

2. 

5. 

### 6. 图

#### 最小生成树 Prim算法

- 最小支撑树

  - 连通网络N = (V; E)的子图T = (V; F)
  - 支撑/spanning = 覆盖N中所有顶点
  - 树，连通且无环，|V| = |F| + 1;加边出单环，再删除同环边即恢复为树；删边不连通，再加联通边即恢复为树
  - 同一网络的支撑树不唯一
  - 对负边也适用
  - 应用：电信公司，假设电信线路使之覆盖全国；网络设计师

- 割&极短跨边

  - 设（U; V \ U）是N的一个割(Cut），即将点集划分为两个集合
  - 若uv是该割的一条极短跨边，则必存在一颗包含uv的MST

- 递增式构造,套用PFS框架

  - 选出优先级最高的跨边ek及其对应顶点vk，并将其加入Tk，随后，更新V\Vk中所有顶点的优先级
  - 注意，优先级数随后可能改变的顶点，必与vk邻接
  - 因此，只需枚举vk的每一邻接顶点v，并取priority(v) = min(priority(v), ||vk, v||)
  - 以上完全符合PFS规范，唯一要做的就是按照prioUpdate()规范，编写一个改变优先级的函数

- > [最小生成树 Prim算法 参考](https://blog.csdn.net/weixin_45781228/article/details/119053038)

#### DFS

- 算法步骤

  > 为每个顶点记录被发现的和访问完成的时刻，对应的时间区间[dTime(v),fTime(v)]均称作v的活跃期（active duration）

  - 将当前节点标记为`DISCOVERED（已发现）`，检查当前节点邻居状态。
    - 处于`UNDISCOVERED（未发现）`：则将该点加入路径，将该点.父 = 当前节点
    - 处于`DISCOVERED`：意味着在此处发现一个有向环路，将该边标记为`后向边（back edge）`
    - 对于有向图，还可能处于`VISITED状态`，根据活跃期判断是否是当前节点祖先
      - 若是，标记为`前向边（forward edge）`。（即到达的节点之前就访问过了，没什么意义）
      - 否则，标记为`跨边（cross edge）`

  - 将当前节点标记为`VISITED（访问完毕）`

  - 所有访问过的顶点通过parent[]指针依次联接得到结果

- 有向无环图存在拓扑排序，有环或无向则不存在。拓扑排序是不断排序并删除掉每次没有出度的点，最终删除的顺序就是拓扑排序。



1. [2021.912.6]

   对于有向无环图，DFS的逆序是否构成一个拓扑排序，如果能请证明，如果不能请给出反例。

   因访问而变成VISITED的顶点A出度是0，而剔除A点后剩下出度为0的点即为A的前驱。那么，按此法回溯，DFS的逆序便是原图的行走顺序（即拓扑排序）

   （有向无环图意味着有且只有一条路径可以不遗漏地从起点到终点）。

2. [2020.912.11]

   有向图经过DFS后的k条边被标记为后向边，则它不一定恰有k个环路

   正确。k条边被标记为后向边说明至少有k个环路，因为多个环路可能共用一条后向边。

3. [2020.912.13]

   有向无环图的拓扑排序是

   A.被发现的顺序 B.被发现的逆序 C.回溯的顺序 D.回溯的逆序

   D。拓扑排序即从出发点到结束点的顺序。而DFS结束后回溯时是从结束点回到出发点的。

4. [2016.912期末.31]

   在有向图G中，存在一条自顶点V通向u的路径，且在某次DFS中有dTime[v]<dTime[u]，则在这次DFS所生成的DFS森林中，v是否一定是u的祖先？若是，请给出证明；若不是，请举出反例。

   错。存在出度大于1的点，使得既经过v又经过s，如v<-->S-->u中v和S是双向的，那么在dfs树里v和u便不是祖先关系，二是兄弟关系。

5. [2019.912期末.3]

   在图DFS()算法中的default分支，将dTime(v) < dTime(u)改为dTime(v) < fTime(u)同样可行。

   正确。由于dTime(u) < fTime(u)，而且任意两个节点的活跃期区间要么是包含要么就是不相交，所以dTime(v) < fTime(u)就可以推出dTime(v) < dTime(u)。



#### BFS

1. [2022.912.6] 同2014期末

   对于无向图，从任意顶点出发，进行 BFS，队列中的头节点与尾节点到起始节点距离之差均不大于 1 

   正确。

   **![image-20221109082712193](https://raw.githubusercontent.com/serfend/res.image.reference/main/image-20221109082712193.png)**

2. 

### 7. 高级搜索树

#### 左式堆/二叉堆

- npl（null path length）空节点最大路径长度，即从x到外部节点的最近距离。

- 左式堆插入、删除的复杂度皆为O(logn)

- 左式堆是处处满足“左倾性”的二叉堆，即任意节点都满足 npl(lc(x)) $\ge$ npl(rc(x))

  - **![image-20221111132146371](https://raw.githubusercontent.com/serfend/res.image.reference/main/image-20221111132146371.png)**

- 左式堆合并

  - 合并时由上向下挨个合并，如果npl右侧少于左侧，则交换左右。
  - **![image-20221111132259786](https://raw.githubusercontent.com/serfend/res.image.reference/main/image-20221111132259786.png)**
  - 蛮力算法O(nlogn)、Floyd算法O(n)

- 完全二叉堆

  - 逻辑结构须等同于完全二叉树，即“结构性”。堆顶以外节点优先级不高于其父节点，即“堆序性”。

  - 建堆 

    - 蛮力算法 或者 自上而下上滤 都是 O(nlogn)

    - Floyd算法（从下往上逐个合并堆）O(n)

      - 插入单个复杂度（检查之前两个堆顶与待合并节点的大小，决定合并后的新堆顶）O(1)

        插入时导致上滤，但是平均上滤次数非常少，可以认为是常数次。

  - 删除 O(logn) （因为可能会导致下滤，下滤平均log(n)次）

1. [2022.912.4] 

   左式堆兄弟子堆满足 L.height>=R.height 。

   错误。经典错误，左式堆只满足L.npl≥R.npl。

2. [2022.912.14]

   一个伸展树中所有节点都是偶数度，最深的叶节点需要经过 11 条边才能到达数根，则该二叉树最少有_____个节点 。

   23。偶数度，h=11+1=12，故每个非叶子结点具有左右孩子，考虑极端，即每层均是一个叶子节点。总节点数 = 12(每层根节点)+11(加一个叶子结点) = 23

3. [2020.912.4]

   完全二叉**堆**删除元素在最坏情况下事件复杂度为O(logn)，平均情况下复杂度为O(1)

   错误。平均情况是从被删除的节点开始下滤操作，直到到外部节点，共O(logn)。

4. [2020.912.5]

   crane算法将左式堆A和B合并成左式堆H，则H右侧链上的节点未必都来自A或B的右侧链。

   正确。因为出现右侧npl大于左侧的时候，就会交换左右，从而使得合并完成的新堆中左右节点皆有可能全面存在。

5. [2020.912.7]

   建立一个完全二叉堆的时间复杂度为O(nlogn)

   错误。floyd建堆因只需要O(n)。

6. [2014.912期末.10]

   多叉堆比二叉堆插入慢，删除快。

   错。之所以快是因为树高更小，而叉过多的时候会导致每层需要干的活变多。通过推导，相比二叉堆：三叉堆快，四叉堆一样，之后的都没有二叉堆快。

7. [2023.912模拟.38]

   对于完全三叉堆，对于秩为r的任意节点，可以在O(1)的时间内确定其在任何高度h上祖先的秩。

   错。只有二四八叉堆有该性质。秩：当前关键码的序数。

#### 胜者树、败者树

> k路归并排序

[https://www.freesion.com/article/463336168/](https://www.freesion.com/article/463336168/)

胜者树：二叉树左右节点比较，胜方向上继续比较，败方将败方序号记录到父节点.data。

败者树：二叉树左右节点比较，败方向上继续比较，并将败方序号记录到父节点.data。



1. [2020.912.3]

   败者树删除的时间复杂度在常系数上优于胜者树。

   正确。败者树重赛时不需要访问兄弟节点，故时间少。

2. [2016.912期末.17]

   与胜者树相比，败者树在重赛过程中，需反复将节点与其兄弟进行比较。

   错。败者树不需要反复将节点与其兄弟进行比较，但胜者树是这样的。

3. [2014.912期末a.19]

   将1983个数字取前三大，最少比较多少次。

   2002。1983-1+2*10=2002。锦标赛树先建满二叉树 $log_21983=11$，建树时候得到第一大的数，随后重赛2次得到第二大第三大的数。重赛每层对比1次，需对比10次（不是满树、所以最少对比11-1=10次）。故总次数为1983建树-1根节点+2\*10两次重赛=2002。如果是k选取的话只需要对比

   

#### AVL树

- 每次插入都会检查当前平衡，并通过3+4旋转修复不平衡。每次插入的时间复杂度是O(1)
- 删除可能会导致失衡传递，从而复杂度是O(logn)



1. [2022.912.7]

   AVL树删除节点后，经过若干次旋转，子树高度可能复原，不至于失衡传播。

   正确。

   **![image-20221109082911697](https://raw.githubusercontent.com/serfend/res.image.reference/main/image-20221109082911697.png)**

   **![image-20221109082926671](https://raw.githubusercontent.com/serfend/res.image.reference/main/image-20221109082926671.png)**

2. [2021.912.5]

   **![image-20221110100721322](https://raw.githubusercontent.com/serfend/res.image.reference/main/image-20221110100721322.png)**

   (1) 目标删除点为v(自己)，v的父亲为p(parent)，p的父亲为g(grand parent)。同时，需要注意的是，v的父亲节点寻找失衡节点g，g的较高一个的孩子是p。

   (2) connect34顾名思义其实就是3个节点4个子树相连，共有LL LR RL RR 4种。前面3个（vpg大小）按中序排序，后面4个按中序排序(T0-T3)

   **![image-20221110104042067](https://raw.githubusercontent.com/serfend/res.image.reference/main/image-20221110104042067.png)**

   (3) connect34需要按实际的图，从左到右的顺序，传入v,p,g,T0,T1,T2,T3。故有

   LL connect34(v,p,g,v->lc,v->rc,p->rc,g->rc)

   LR connect34(p,v,g,p->lc,v->lc,v->rc,g->rc)

   RL connect34(g,v,p,g->lc,v->lc,v->rc,p->rc)

   RR connect34(g,p,v,g->lc,p->lc,v->lc,v->rc)

   四种情况分别如下图。

   

   ```mermaid
   graph TB
   p((p));v((v));g((g1));T0(T0);T1(T1);T2(T2);T3(T3);
   g-->p-->v;v-->T0;v-->T1;p-->T2;g-->T3;
   
   p2((p));T02(T0);v2((v));g2((g2));T12(T1);T22(T2);T32(T3);
   g2-->p2-->T02;p2-->v2;v2-->T12;v2-->T22;g2-->T32;
   
   v3((v));g3((g3));T03(T0);T13(T1);T23(T2);T33(T3);p3((p));
   g3-->T03;g3-->p3;p3-->T33;p3-->v3;v3-->T13;v3-->T23;
   
   g4((g4));T04(T0);T14(T1);T24(T2);T34(T3);p4((p));v4((v));
   g4-->T04;g4-->p4;p4-->T14;p4-->v4;v4-->T24;v4-->T34;
   ```

   

   

3. [2020.912.6]

   AVL树在插入一个节点后可能引起$O(logn)$次局部重构。

   错。AVL不论如何调整都是调当前项的，故只调O(1)次。（删除的话可能会导致失衡传递，从而调O(logn)次）

4. [2010.912期中.10]

   在包含2010个节点的AVL树中，最高与最低叶节点的深度差可达（）

   7。Fib-AVL树的高度是最少节点情况下最高的，高度h的fib-AVL的规模是fib(h+3)-1，而fib(17)<2010<fib(18)，故最大高度为14，即深度差为14-[14/2]=14-7=7。

   **![image-20221211100359131](https://raw.githubusercontent.com/serfend/res.image.reference/main/imgimage-20221211100359131.png)**

#### B树

m阶B树每个层级最多有m-1个关键码，关键码和关键码之间有关节点，每个节点共m个关节点，用于挂下一层级。

>一颗m阶的B树定义如下：
>1）每个结点最多有m-1个关键字。
>2）根结点最少可以只有1个关键字。
>3）非根结点至少有 Math.ceil(m/2)-1个关键字。
>4）每个结点中的关键字都按照从小到大的顺序排列，每个关键字的左子树中的所有关键字都小于它，而右子树中的所有关键字都大于它。
>5）所有叶子结点都位于同一层，或者说根结点到每个叶子结点的长度都相同。

**![image-20221110150004629](https://raw.githubusercontent.com/serfend/res.image.reference/main/image-20221110150004629.png)**

- 插入关键码，先调用search找到当前插入的地方，插入到该节点中。
  - 如果超出该层级最大数（m-1个），则将发生上溢，将第[m/2]个移到父节点中，该节点左右分裂成两个节点作为左右孩子。

- 删除关键码，先调用search找到即将删除的节点，将即将删除的节点和该节点直接后继（数值排序上，该节点的下一个节点）交换后，删除该节点。
  - 删除过程中如果出现节点个数不足m/2，则将通过旋转父节点，以从其另一侧节点借。如果兄弟节点也没有足够的关键码，则将父节点下溢合并。

1. [2022.912.17]

   在有 400 个关键码的 20 阶 B-树，查找最大需要比较______次 。

   39。比较次数最多，故使得每层关键码最少，为10个，故400个关键码一共可以形成3层（10^2=100<N=400<10^3=1000）。而总次数=每层比较的关键码个数19*层数2+根节点1个=39个。

2. [2020.912期末.4]

   **![image-20221110143926820](https://raw.githubusercontent.com/serfend/res.image.reference/main/image-20221110143926820.png)**

   (1) 当总数m为奇数时，再次删除，高度必减少；当总数为偶数时，则不一定。

   因为如果插入导致树增高，则一定是原先的树发生上溢，并传播到了根节点。

   如果此时总数m为奇数，则左右孩子个数均为 (m-1)/2 ，已经是B树最少的关键码。故再删除时必然降低

   如果此时总数m为偶数，则左孩子个数m/2，右孩子个数为 m/2-1，状态可能是正常的。故删除的时候不一定发生下溢，即不一定恢复高度。

   

   

3. [2010.912期中.19]

   高度为 3 的5 阶B‐树，至多可存放（ ）个关键码，至少需存放（ ）个。

   124；17。5阶3高度的B树，则其每层最多放4个关键码5个节点，1、2层最少放(5/2)-1 = 2个 3个节点，3层最少放1个。

   最多个数 = 4（第一层） + 5（第一层的关节点）*4（第二层） + (5\*5)（第二层的关节点）\*4（第三层） = 4 + 5\*4 + 25 \* 4 = 124

   最少个数 = 2（第一层） + 3（第一层的关节点）*2（第二层）+ (3\*3) \* 1（第三层） = 2 + 6 + 9 = 17

4. [2019.912期末.1]

   考查包含2018个关键码的16阶B-树，约定根节点常驻内存，且在各节点内部采用顺序直找.

   a)在单次成功查找的过程中，至多可能需要读多少次磁盘?请列出估算的依据

   b)在单次成功查找的过程中，至多可能有多少个关键码需要与目标关键码做比较?请列出估算的依据。

   

   a) 3。B-树是满二叉树结构，且每层至少放[m/2]个，则2018=8^4.+个，即树高最大为4，而根节点常驻内存不需要磁盘读取，故次数为4-1=3次。

   b)46。为了使得比较次数最多，则在每层的关键点个数要尽可能少，和a的情况是一样的，高度为4，比较次数为15个关键码*3层+根节点1个关键码=46次。

####  势能

> **![image-20221109082306917](https://raw.githubusercontent.com/serfend/res.image.reference/main/imgimage-20221109082306917.png)**

1. [2022.912.3]

   无论如何，伸展树的节点总势能不超过O(nlogn)

   正确。当伸展树是单链的时候，总体势能为O(nlogn)。当为满树时，总势能为O(n)

2. 

#### 红黑树

- 规则

  1. 节点是红色或黑色。

  2. 根节点是黑色。

  3. 每个叶子节点都是黑色的空节点（NIL节点）。
  4. 每个红色节点的两个子节点都是黑色。(从每个叶子到根的所有路径上不能有两个连续的红色节点)
  5. 从任一节点到其每个叶子的所有路径都包含相同数目的黑色节点。

1. [2022.912.8]

   若红黑树删除导致双黑修正进行了 Ω(logn)次重染色，则至少旋转一次 

   错误。双黑操作进行O(logn)次重染色，不一定需要旋转，如一直进行（2B），最后一次进行（2R），则一直进行染色，最后调整完成。

   **![image-20221109083059605](https://raw.githubusercontent.com/serfend/res.image.reference/main/imgimage-20221109083059605.png)**

2. [2022.912.16]

   红黑树一条路经上有 5 个红节点，则树最少有______个节点 。（只需要算内部节点）

   62。红黑交替，根节点为黑，则h=10（每个黑下面对应一个红）。红黑树的性质要求任意节点到根节点经过的黑色节点数相同，为使得节点数尽量少，故假设树右侧比左侧高，左侧全为黑节点，则任意一层左侧节点应为满二叉树，每个的总数 = $ 2^{右侧剩余黑节点数} - 1 $。总节点数 = $ \ {\sum_{i=1}^{4}}{2·(2^i - 1)} + h  $ = 2·(16-1+8-1+4-1+2-1) + 10 =  26*2+10 = 62

3. [2021.912.8]

   红黑树结构，如果不显式记录颜色，通过隐式记录应该如何操作？

   不显式记录颜色，则将数变成一个多叉树。将每个节点的高度将不再是当前高，而是原本黑色节点的高度。

   即有如果p节点父亲g->height = p->height + 1 = x->height+1则p节点为红色，其他情况均为黑色。

   而如果p是根节点的话，那么一定是黑色。

4. [2020.912.8]

   红黑树中所有节点的黑深度和黑高度之和相等

   错。深度：从根到节点的长度。高度：从节点到外部节点的长度。红黑节点的黑深度相同，红节点的黑高度=黑节点黑高度-1（因为黑节点自己也算高）

5. 

### 8. 词典

#### 跳转表

查询和维护平均时间复杂度O(logn)。纵向移动的时间是O(1)

[跳转表方法](https://blog.csdn.net/cwl110120/article/details/106163301)

**![image-20221111144358704](https://raw.githubusercontent.com/serfend/res.image.reference/main/image-20221111144358704.png)**



1. [2020.912.12]

   在n个节点的跳转表中，单个词条的期望塔高是O(logn)

   错误。跳转表的特性是逐层随机减半，故塔高符合几何分布 $p^{k-1} · (1-p)$，期望E = 1/(1-p)  = 2。整个表的塔高才是O(logn)

2. 

#### 散列表

### 9. 优先级队列



### 10. 串

> 蛮力算法$ T = O(m·n) $，**在字母表增大的时候，不太会出现最坏情况，则$T=O(m+n)$**

#### kmp字符串匹配

在字母表比较小的时候（如二进制字符串 `0、1`）效率远高于蛮力算法

$T=O(m+n)$

> 本质是通过`记忆`来`预测`。经过前一轮比对，我们已经清楚地知道，子串T[i - j, i)完全由'0'组成。记住这一性质便可预测出：在回退之后紧接着的下一轮比对，前j - 1次比对必然都会成功。因此，可直接令i保持不变，令j = j - 1，然后继续比对。如此，下一轮只需1次比对，共减少j - 1次！
>
> **![image-20221109111205705](https://raw.githubusercontent.com/serfend/res.image.reference/main/image-20221109111205705.png)**

##### next表

故保存一个next表，用以记录当单个字符匹配失败时应该回退到哪个字符去。

>**![image-20221109105328726](https://raw.githubusercontent.com/serfend/res.image.reference/main/image-20221109105328726.png)**

##### 执行流程

![image-20221109131022873](https://raw.githubusercontent.com/serfend/res.image.reference/main/image-20221109131022873.png)****

```cpp
/*
KMP算法 从Text中搜索Pattern，返回位置
@params P Pattern模式串（待搜索串）
@params T Text文本串
@return 
*/
int match ( char* P, char* T ) { 
    int* next = buildNext(P); // 构造next表
    int n = (int)strlen(T), i = 0; // 文本串指针
    int m = (int)strlen(P), j = 0; // 模式串指针
    while (j < m && i < n) // 自左向右逐个比对字符
        if (0 > j || T[i] == P[j]) // 若匹配，或P已移出最左侧（两个判断的次序不可交换）
            { i++; j++; } // 则转到下一字符
        else // 否则
            j = next[j]; // 模式串右移（注意：文本串不用回退）
    delete []next; // 释放next表
    return i - j;
}
```

```cpp
/*
构造模式串P的next表，即某字符匹配失败时，应该回到什么地方开始新的匹配的表。
@params P Pattern模式串（待搜索串）
@return next表
*/
int* buildNext ( char* P ) {
    size_t m = strlen(P), i = 0; // “主”串指针，永远都是不断增加的
    int* N = new int[m]; // next表
    int j = N[0] = -1; // 模式串指针，-1是为了等效一个-1位置是一个通配符，以完整算法。
    while (i < m - 1)
        if (0 > j || P[i] == P[j]) { // 匹配则记录到next表
            i++; j++;
            N[i] = j; // 此句可改进为 （将教训也利用起来），如下
            // N[i] = (P[i]!=P[j]?j:N[j]); // 判断下一个字符，如果字符不一致则可用j，否则只能用更早之前的N[j]
            continue
        }  
    	// 失配则将模式串指针回到上一个next表位置
    	j = N[j];
    return N;
}
```



##### next表改进

思想是将“教训”也利用起来，N[j] = (P[j]!=P[j]?j:N[j]); // 如果字符不一致则可用j，否则只能用更早之前的N[j]。

这里的教训指的是，在当前位置已经判断过了X字符失配，故如果上一个字符也是X字符的话那么将必然失配，所以一次往回多移一些，跳过这个必然的失配。



##### 在做题中快速手写next表

改进前的表手填方式：检查到当前的子串前一个字符和总字符串前缀有多少个相同，就按顺序填多少。

改进后的表手填方式：在改进前的基础上，每到匹配上的位置时，如果P[i]和P[j]是相同的，同则回到N[j] （这里的N[j]就是上一步算出来的Next表里Next[j]），否则同改进前(回到j)。或者换个思路，先把next表中每次1234...的最大数位置填上，如下表是1...8 1 1 1 1 1..2 ，然后按上面的方法再把别的空填上。

|            | 1    | 2    | 3    | 4    | 5    | 6    | 7    | 8    | 9    | 10   | 11   | 12   | 13   | 14   | 15   | 16   | 17   | 18   | 19   | 20   |
| ---------- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| 模式串     | A    | B    | C    | A    | B    | C    | A    | B    | C    | A    | B    | A    | A    | A    | A    | A    | B    | A    | B    | C    |
| 改进前next | -1   | 0    | 0    | 0    | 1    | 2    | 3    | 4    | 5    | 6    | 7    | 8    | 1    | 1    | 1    | 1    | 1    | 2    | 1    | 2    |
| 改进后next | -1   | 0    | 0    | -1   | 0    | 0    | -1   | 0    | 0    | -1   | 0    | 8    | 1    | 1    | 1    | 1    | 0    | 2    | 0    | 0    |

```javascript
// javascript演示
function buildNext(data){
    const len = data.length
    const N = new Array(len).fill(0)
    let i = 0 , j = N[0] = -1
    const j_arr = [0]
    while(i<len-1){
        if(0>j||data[i]===data[j]){
            i++,j++
            j_arr.push(j)
            N[i] = j
            continue
        }
        j = N[j]      
    }
    return [N,j_arr]
}
function buildNextEx(data){
    const len = data.length
    const N = new Array(len).fill(0)
    let i = 0 , j = N[0] = -1
    const j_arr = [0]
    while(i<len-1){
        if(0>j||data[i]===data[j]){
            i++,j++
            j_arr.push(j)
            N[i] = (data[i]!=data[j]?j:N[j])
            continue
        }
        j = N[j]      
    }
    return [N,j_arr]
}

function buildResult(data){
    const ml = new Array(`${data.length}`.length+1).fill(' ').join('') // max_length
    const to_result = (s)=>(s.split && s.split('') || s).map(i=>`${i}`).map(i=>ml.substr(0,ml.length-i.length) + i).join('')
    const a = to_result(data)
    const b = buildNext(data).map(to_result)
    const c = buildNextEx(data).map(to_result)
    const items = [`index of i :${to_result(new Array(data.length).fill(0).map((i,index)=>index))}`,
                   `raw content:${a}`,'',
                   `next result:${b[0]}`,
                   `next2result:${c[0]}`,
                  ]
    console.log(items.join('\n'))
}

buildResult('ABCABCABCABAAAAABABC')
buildResult('HHFBHHFHHFBSHFHJHHFBHHFHH')
```



1. [2020.912.15]

   模式串和文本串均由26个字母组成，那么蛮力算法在最好情况下的时间复杂度（小于/等于/大于），在平均情况下的时间复杂度（小于/等于/大于）KMP算法。

   等于；等于。最好情况两者都是O(m+n)，平均情况因为考虑到模式串和文本串长度一样，故消耗的时间均为2（KMP没有机会学习“经验”便匹配结束）

2. [2020.912.19]

   模式串HHFBHHFHHFBSHF改进后的next表next[13] = __ ，next[0] = __。

   next[13] = 1；next[0] = -1。

   | next表 | 0    | 1    | 2    | 3    | 4    | 5    | 6    | 7    | 8    | 9    | 10   | 11   | 12   | 13   |
   | ------ | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
   | 模式串 | H    | H    | F    | B    | H    | H    | F    | H    | H    | F    | B    | S    | H    | F    |
   | 改进前 | -1   | 0    | 1    | 0    | 0    | 1    | 2    | 3    | 1    | 2    | 3    | 4    | 0    | 1    |
   | 改进后 | -1   | -1   | 1    | 0    | -1   | -1   | 1    | 3    | -1   | 1    | 0    | 4    | -1   | 1    |

3. 在KMP匹配的过程中，当主程序运行到i,j的状态时，意味着之前至少做过i次成功匹配以及i-j次失败匹配。

   错。应该是等于i次成功匹配和不超过i-j次失败。i-j初始值是0，成功时i和j同时+1，失配时next[j] < j，严格单调增加，故最多有i-j次失配。

#### bm字符串匹配

> 通过提高判断出`失败`的效率，提高整体效率。（或只做失败的匹配，将后面的教训优先吸收）
>
> 反向匹配，把pattern倒着匹配。
>
> 在字符集比较大的时候，失败概率高，所以bm算法优势更为明显。$ T = O(n) $
>
> bm在没有gc(good chars)表的时候在字符集很小的时候，字符重复概率高，退化为蛮力算法。$ T = O(m*n) $
>
> **![image-20221109144941515](https://raw.githubusercontent.com/serfend/res.image.reference/main/image-20221109144941515.png)**

- 坏字符 bc表(bad chars)

  **![image-20221109145445976](https://raw.githubusercontent.com/serfend/res.image.reference/main/image-20221109145445976.png)**

  ```cpp
  /*
  构造Bad Charactor Shift表：O(m + 256)，用于决定`匹配过程中发现失配，则下一次向后移动的个数`。
  例如 bc['m'] = 4，表示m字符出现失配时，应该向后移动4位
  @params P pattern字符串
  @return
  */
  int* buildBC ( char* P ) { // 
  	int* bc = new int[256]; // BC表，与字符表等长
      for (size_t j = 0; j < 256; j ++) bc[j] = -1; // 初始化：首先假设所有字符均未在P中出现
      for (size_t m = strlen(P), j = 0; j < m; j ++) // 自左向右扫描模式串P
      	bc[ P[j] ] = j; // 将字符P[j]癿BC项更新为j（单调逑增）
      return bc;
  }
  ```

  

- 好后缀gs表(good suffix)

  > 通过吸收`经验`（即KMP算法思想），使得向右滑动更快，当发生失配时，直接向左移动x个字符。
  >
  > **![image-20221109150757688](https://raw.githubusercontent.com/serfend/res.image.reference/main/image-20221109150757688.png)**
  >
  > **![image-20221109150823014](https://raw.githubusercontent.com/serfend/res.image.reference/main/image-20221109150823014.png)**

  - ms(max matched suffix)子串：pattern的后缀，匹配最大的自身串。

    > 下图中`ICE` `RICE` `ICED...PRICE`为三个ms串，他们都匹配了pattern整个串。

  - ss表(suffix strlen)：最大匹配后缀长度表，即pattern中ms子串的长度。

    > 上面三个ms对应的ss分别为其各自的长度 3 4 15

  **![image-20221109152311818](https://raw.githubusercontent.com/serfend/res.image.reference/main/image-20221109152311818.png)**

  ```cpp
  /*
  构造ss表 最大匹配后缀长度表，用于下一步构造gs表 O(p_len)
  @params P pattern模式串
  @return
  */
  int* buildSS ( char* P ) {
      int p_len = strlen(P); 
      int* ss = new int[p_len]; // Suffix Size表
      ss[p_len - 1] = p_len; // 对最后一个字符而言，与之匹配的最长后缀就是整个P串
      // 以下，从倒数第二个字符起自右向左扫描P，依次计算出ss[]其余各项
      int p_last = p_len-1;
      // cur_start:current start position.
      for (int cur_start=p_last, current_end=p_last, j=cur_start-1; j>=0; j--){
          int p_end_len = p_last-current_end; // 从倒数第二个字符起自右向左扫描P
          if ((cur_start< j) && (ss[p_end_len+j] <= j-cur_start)){ // 当前扫描出的字符有j-cur_start个的长度均相同
              ss[j] = ss[p_end_len+j]; // 直接用此前已计算出的ss[]
              continue;
          }
          current_end = j; cur_start = __min(cur_start,current_end);
          while ((0 <= cur_start) && (P[cur_start] == P[p_end_len+cur_start])){
              cur_start--; // 找到字符串不相等的地方     
          }
          ss[j] = current_end - cur_start; // 长度等于字符串开始到结束
      }
      return ss;
  }
  ```

  **![image-20221109174303919](https://raw.githubusercontent.com/serfend/res.image.reference/main/image-20221109174303919.png)**

- 构造ss表

  - 从末尾往前看，每次看到一个和后缀一样的串则将该串一样的个数标上，其他地方填0。
  - 最后一位肯定是整个串等于它自己，故写自己的长度
    - 例如AAACBCABCABC，则ss为00010200300 12




- 构造gs表的时候主要分两种情况：一种是ss[j]=j+1，一种是ss[j]<j+1

  - 初始化所有的gs[i]=m

  - 一种是MS整个就是一个匹配的串，$$ss[j] = j+1 $$ ，有i从当前到m-j-1之间所有的gs[i] = m-j-1

  - 另一种是MS[j]是P[0,j]的真后缀，ss[j] $\le$ j，有gs[m-ss[j]-1] = m-j-1 
    - 最后将gs[m-1] = 1（等价于j=m-2时的情形，gs[m-ss[m-2]-1]是gs[m-0-1]，即gs[m-1]=m-j-1=m-m+2-1=1）


  ```javascript
  /*
  构造gs表（good suffix后缀位移量表）。用于匹配失败时，借助前期经验向右滑动的位置
  @params P pattern模式串
  @return
  */
  int* buildGS ( char* P ) {
      int* ss = buildSS( P ); // Suffix Size table
      size_t p_len = strlen( P ); 
      int* gs = new int[p_len]; // Good Suffix shift table
      for (size_t i=0;i<p_len;i++) gs[i] = p_len; // 初始化全部为字符长
      // i为当前gs表进度，j为ss表使用
      int p_last = p_len-1;
      for (size_t j=p_last;0<=j;j--) // 逆向逐一扫描各字符P[j]
      {
          if (j + 1 != ss[j])continue; // 若P[0, j] != P[p_last-j, p_last]，则继续扫描
          for (size_t i=0;i<p_last-j;i++) // 否则对于P[p_last-j]左侧的每个字符P[i]而言
              gs[i] = p_last-j; // p_last-j都是gs[i]的一种选择
      }
      for (size_t j = 0; j < p_last; j++) 
      	gs[p_last-ss[j]] = p_last-j; // p_last-j必是其gs[p_last-ss[j]]值的一种选择
      delete [] ss;
      return gs;
  }
  ```

  

- 总结几个表的实例

**![image-20221109154910079](https://raw.githubusercontent.com/serfend/res.image.reference/main/image-20221109154910079.png)**

```javascript
function buildSS(data){
    const m = data.length 
    const ss = new Array(data.length).fill(0)
    ss[m-1] = m
    for(let lo=m-1,hi=m-1,j=lo-1;j>=0;j--){
        if((lo<j) && (ss[m-hi+j-1]<=j-lo)){
            ss[j]=ss[m-hi+j-1]
        }else{
            hi=j
            lo = Math.min(lo,hi)
            while((0<=lo)&&(data[lo]===data[m-hi+lo-1])){
                lo--
            }
            ss[j] = hi - lo
        }
    }
    return ss
}

function buildGS(data){
    const ss = buildSS(data)
    const m = data.length
    const gs = new Array(m).fill(m)
    for(let i=0,j=m-1;j>0;j--){
        if(j+1===ss[j]){
            while(i<m-j-1)gs[i++] = m - j - 1
        }
    }
    for(let j =0;j<m-1;j++){
        gs[m-ss[j]-1] = m - j - 1
    }
    return gs
}


function buildResult(data){
    const ml = new Array(`${data.length}`.length+1).fill(' ').join('') // max_length
    const to_result = (s)=>(s.split && s.split('') || s).map(i=>`${i}`).map(i=>ml.substr(0,ml.length-i.length) + i).join('')
    const a = to_result(data)
    const b = to_result(buildSS(data))
    const c = to_result(buildGS(data))
    const items = [`index of j :${to_result(new Array(data.length).fill(0).map((i,index)=>index))}`,`raw content:${a}`,`ss   result:${b}`,`gs   result:${c}`]
    console.log(items.join('\n'))
}

buildResult('MIAMI')
buildResult('BARBARA')
buildResult('CINCINNATI')
buildResult('PHILADELPHIA')
buildResult('ladygaga')


```



1. [2022.912.11]

   如果 bm 算法仅使用 gs 策略而不使用 bc 策略则不能保证在最好情况下有 O(n/m)的时间复杂度（n 为文本串长度，m 为模式串长度）

   错误。注意是最好情况下，则有gs和bc都是O(n/m)。同2019期末判断题第26题。

2. [2019.912期末.12]

   相比于KMP算法，BM算法更适合于大字符集的应用场合

   正确。因为bm算法就是利用了“匹配失败”概率大的特点而去学习“教训”。字符集越大，单个字符匹配失败概率越大，故优势越大。

3. [2014.912期末.15]

   写ladygaga的GS表

   88888261。

   | j         | 0    | 1    | 2    | 3    | 4    | 5    | 6    | 7    |
   | --------- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
   | p         | l    | a    | d    | y    | g    | a    | g    | a    |
   | ss        | 0    | 1    | 0    | 0    | 0    | 2    | 0    | 8    |
   | m-ss[j]-1 |      | 6    |      |      |      | 5    |      | -    |
   | m-j-1     |      | 6    |      |      |      | 2    |      | -    |
   | gs        | 8    | 8    | 8    | 8    | 8    | 2    | 6    | 1    |

4. [2016.912期末.27]

   对随机生成的二进制字符串，gs表中gs[0]=1的概率为（）

   $\frac{1}{2^{m-1}}$。gs[0] = 1则说明模式串是同一个字符，假设字符表有n个字符则概率为 $1/n^{m-1}$。换成选项中的同底得到答案选B。

#### hash散列匹配

- 散列计算

  - 通过将字符串转换为一个一个的散列，使得每次匹配一个子串只需要O(1)的时间。

  - 指纹计算可以是类似于取模的方式，例如对于136373637924文本串，6379模式串。

    - R=10,M=123 => Dm = $ R^{m-1} \% M = 10^3 \%123 = 16 $ 

    - 模式串的 $ Hash = (6+3+7+9)*16 = 400 $，同理文本串的Hash分别为208	304	304	304	304	304	400	336	352，即400匹配成功。

- 散列冲突解决办法

  - （闭散列）双向平方试探
    - 桶大小M
      - 当M是合数：装填成功的个个数不定。
      - 当M是素数：装填成功的**恰好**会有[M/2]种，且由试探的前[M/2]取遍。
      - 当M符合4k+3时，可以装填满100%
    
  - （开散列）开放式散列存储
    - 通过在一个桶内记录多个数据，节约了桶空间，但是会导致单个桶的局部性变差。

> 需要注意的是，为了使得计算散列的时间接近于O(1)，需要将后一个指纹借助前一个指纹得到，而不是重新计算
>
> ```cpp
> /*
> 子串指纹快速更新算法
> @params hashT 上一个指纹值
> @params T 待匹配文本
> @params m 模式串文本的总长度
> @params k 当前子串指针位置
> @params Dm 由hash进制转换而来，=(R^(m-1)) % m
> */
> void updateHash ( HashCode& hashT, char* T, size_t m, size_t k, HashCode Dm ) {
>     hashT = ( hashT - DIGIT ( T, k - 1 ) * Dm ) % M; //在前一指纹基础上，去除首位T[k - 1]
>     hashT = ( hashT * R + DIGIT ( T, k + m - 1 ) ) % M; //添加末位T[k + m - 1]
>     if ( 0 > hashT ) hashT += M; //确保散列码落在合法匙间内
> }
> ```

1. [2022.912.18]

   **![image-20221109103501595](https://raw.githubusercontent.com/serfend/res.image.reference/main/image-20221109103501595.png)**

   根据题意，即插入数会先余13，填入表中。因为是双向平方，即碰到冲突就按平方加减后再取余。

   而余13=4k+1，不等于4k+3，故是无法通过双向平方遍历完所有桶的，可以多尝试几个数，可以发现如下图，2021将无法填入。

   注意**正常情况下**桶存储装填因子>0.5时将触发rehash，以增加桶容量。

   |      | 0            | 1            | -1           | 2            | -2           | 3            | -3           | 4            | -4           |      |      |      |      |      |      |      |      |      |      |      |      |      |
   | ---- | ------------ | ------------ | ------------ | ------------ | ------------ | ------------ | ------------ | ------------ | ------------ | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
   |      | N+0²     %13 | N+1²     %13 | N-1²     %13 | N+2²     %13 | N-2²     %13 | N+3²     %13 | N-3²     %13 | N+4²     %13 | N-4²     %13 | 0    | 1    | 2    | 3    | 4    | 5    | 6    | 7    | 8    | 9    | 10   | 11   | 12   |
   | 44   | 5            | 6            | 4            | 9            | 1            | 1            | 9            | 8            | 2            |      |      |      |      |      | 44   |      |      |      |      |      |      |      |
   | 35   | 9            | 10           | 8            | 0            | 5            | 5            | 0            | 12           | 6            |      |      |      |      |      | 44   |      |      |      | 35   |      |      |      |
   | 18   | 5            | 6            | 4            | 9            | 1            | 1            | 9            | 8            | 2            |      |      |      |      |      | 44   | 18   |      |      | 35   |      |      |      |
   | 58   | 6            | 7            | 5            | 10           | 2            | 2            | 10           | 9            | 3            |      |      |      |      |      | 44   | 18   | 58   |      | 35   |      |      |      |
   | 71   | 6            | 7            | 5            | 10           | 2            | 2            | 10           | 9            | 3            |      |      |      |      |      | 44   | 18   | 58   |      | 35   | 71   |      |      |
   | 32   | 6            | 7            | 5            | 10           | 2            | 2            | 10           | 9            | 3            |      |      | 32   |      |      | 44   | 18   | 58   |      | 35   | 71   |      |      |
   | 84   | 6            | 7            | 5            | 10           | 2            | 2            | 10           | 9            | 3            |      |      | 32   | 84   |      | 44   | 18   | 58   |      | 35   | 71   |      |      |
   | 2021 | 6            | 7            | 5            | 10           | 2            | 2            | 10           | 9            | 3            |      |      |      |      |      |      |      |      |      |      |      |      |      |

2. [2020.912期末.1]

   一个容量M=4079（素数）的哈希表，使用双向平方试探法，共插入了1231个词条，但在下一次插入时触发了rehash操作，问该哈希表此时的状态及rehash的原因。

   2848。4079 = 4k+3，因此可以装满整个表长，因此发生重散列意味着装填因子为百分百，所以有4079-1231=2848个懒惰删除的桶。

   > 如果总数不是4k+3的话，将会在装填因子>0.5的时候，即有一半以上被占用的时候发生rehash来扩大hash表。
   >
   > 注意此题使用的是双向平方，而如果题目是单项平方，则应在50%时便rehash。

3. [2019.912期末.8]

   采用单向平方策略的散列表，只要长度M不是素数，则每一组同义词在表中都不会超过[M/2]个。

   错误。不是素数的时候，装填成功的个数不定。例如M=10，就有0 1 4 9 6 5这6个数可被装填>[M/2]

4. [2020.912.10]

   开放式散列与封闭式散列更可以有效利用局部缓存。

   错。显然开放式会导致局部（即单个桶）存储过多，从而导致在局部范围内需要O(n)去查找。

5. 

#### kr字符串 hash全字匹配

1. [2022.912.12]

   kr 算法在匹配失败后**无法**在 O(1)内找到下一个 。

   错误。可在O(1)找到

   **![image-20221109094055380](https://raw.githubusercontent.com/serfend/res.image.reference/main/image-20221109094055380.png)**6

   

2. 





## 操作系统

### 系统结构

### 中断及系统调用

1. [2022.912.9]

   外部设备产生中断后，操作系统一定会响应中断

   错误。如果产生的中断是可屏蔽类型的，则操作系统不受影响（例如键盘输入）

2. [2021.912.4]

   可以通过改变某个寄存器位的方式停止时钟中断。

   错误。时钟中断是系统级（内部）的，没法屏蔽。只有外部的中断才能屏蔽

3. [2020.912.11]

   给出系统调用的四个分类，例如xx类完成xx的创建、撤销和退出 

   fork完成进程的创建；read读取输入流；exec用于程序加载和执行；wait用于父进程等待子进程结束；kill完成进程的退出；

4. [2021.912.9]

   缺页异常后
   A.中断服务例程前会保存通用寄存器(大概意思是中断响应会保存通用寄存器)

   B.异常处理后，回到发生缺页的指令继续执行

   C.异常处理后，回到发生缺页的指令的下一条继续执行

   D.异常处理后，由软件恢复pc。

   B。考点:异常处理。A中断服务例程保存通用寄存器 C.回到缺页指令继续执行 D说法不对，应该是异常处理例程中恢复PC

   

5. [2020.912.2]

   ucore时钟中断设为10ms出发一次，所以ucore不能实现小于10ms的周期定时间隔。

   对。定时需要靠时钟中断，且是最小的单位了，是不可被屏蔽的中断。

6. 

   

### 内存管理

- 虚拟存储的组成

总位数=log2(总虚拟空间)位
虚拟地址=页目录号+页号+页内偏移
页目录位数=log2(页表大小)位
单个页表中页表项号数=log2(页表大小/页表项大小)位
页内偏移位数=总位数-页目录个数-一个页的表项个数
页内大小=2^页内偏移位数

#### 伙伴系统

当申请$2^{u-1}<s\le 2^{u}$大小时，会分配$2^u$整个块给该进程，剩余区域作为空闲区。合并的时候会选取和当前相等的空闲块的区域合并，例如[1k=malloc|1k|2k|4k|8k|16k]，则释放的时候会依次合并。

1. [2022.912.4]

   当进程用完所有虚拟地址空间后，多级页表比一级页表所占的内存空间大

   错误。虚拟地址不会影响多级页表的内存分配，多级列表内存是随着真实使用而惰性增加的。

2. [2022.912.8]

   通过页表机制可以实现进程间共享内存

   正确。共享内存就是通过页表的地址指向（映射）实现的。

3. [2022.912.10]

   最优页面置换算法（OPT）属于栈式算法（Stack），存在 Belady 异常现象

   错误。LRU和OPT属于栈层级的算法，不会去请求页。所谓*Belady*现象（像个女的一样婆婆妈妈没完没了报告缺页）是指：采用FIFO算法时，如果对—个进程未分配它所要求的全部页面，有时就会出现分配的页面数增多但缺页率反而提高的异常现象。

4. [2022.912.11]

   反置页表的每一个页表中存在____、____、____和hash冲突页表项 链表指针，在反置页表地址转换过程中，hash函数的输入量是____和____，输出用作____，如页表项中的内容和hash函数输出不一致，则会出现____。

   A. 进程控制块 B. 文件标识符 C. hash冲突 D. 标志位 E. 物理页号 F. 虚拟页号 G. 进程ID

   标志位(D)、虚拟页号(F)、进程ID(G)、虚拟页号(F)、进程ID(G)、物理页号(E)、hash冲突(C)。

   说白了就是进程通过散列解决地址冲突，为了更好散列，所以每个页表（标志位用来显示当前页的状态如valid dirty protection等）用了虚拟页id和进程id来算出hash，得到物理页id，从而解决冲突。反置页表(Inverted Page Table)所有进程共用，减少内存的使用，但是会增加内存查询的耗时。

5. [2021.912.1]

   clock算法可以通过修改和读取页表中的访问位实现

   正确。时钟置换算法是将页表上的访问位修改实现，读写时标为1，之后如果缺页想找这个页表的时候会判断其访问位是否为0，是则置换它，否则找下一个

6. [2019.912.1]

   X86-32虚拟存储系统中，4KB页面大小为4KB，采用二级页表，一级页表可以不在内存中。

   错误。一级页表必须在内存中。通过访问一级页表来寻找二级页表，此时二级页表可以不在，即一级页表的页表项有效位为0。

7. [2019.912.5]

   CPL<=DPL[门]和CPL<=DPL[段]， \__\_表示请求时可以和门特权级相同， ___表示请求时应低于段的特权级。

   CPL<=DPL[门]；CPL<=DPL[段]。DPL门和段的区别，段大于门。特权级到段时则说明CPL小于段。

### 进程及线程

进程、线程、协程，全局性依次递减，用户性依次递增。

- 孤儿进程

  - 孤儿进程指的是在其父进程执行完成或被终止后仍继续运行的一类进程。参考学习，https://www.cnblogs.com/anker/p/3271773.html
  - 一个父进程退出，而它的一个或多个子进程还在运行，那么那些子进程将成为孤儿进程。

- 僵尸进程

  - 僵尸进程是指完成执行（通过 exit 系统调用，或运行时发生致命错误或收到终止信号所致），但在操作系统的进程表中仍然存在其进程控制块，处于"终止状态"的进程。
  - 一个进程使用fork创建子进程，如果子进程退出，而父进程并没有调用wait或waitpid获取子进程的状态信息，那么子进程的进程描述符仍然保存在系统中，这种进程成为僵尸进程。

- 进程的几种状态

  - 创建-->就绪<-->运行-->退出
    运行-->等待-->就绪

    > 故即使从任务管理器kill阻塞的进程，进程也会先进入运行态再退出。

- vfork操作时使用copy on write机制，fork操作时使用完全copy。

  - vfork时顾名思义。不会复制任何东西，直接共用父进程的。直到有写操作时才复制，

1. [2022.912.2]

   用信号量可以实现管程

   正确。管程和信号量是等价的，两者可以相互实现。管程其实就是加了synchronized关键字的函数，其执行变成同步的。

2. [2019.912期末.3]

   基于mesa机制的管程在执行条件变量的signal操作过程中，不会睡眠。

   正确。只有Hoare机制才会睡眠。mesa机制是直接让T2开始执行直到结束。Hoare机制是T2执行后便释放T1，随后再释放T2。

   **![image-20221130231108074](https://raw.githubusercontent.com/serfend/res.image.reference/main/imgimage-20221130231108074.png)**

3. [2022.912.3]

   在 shell 中输入”ls | more”，shell 会建立两个子进程，并在这两个进程之间建立管道（pipe）

   正确。`|`符号表示管道，将其左侧的输出发送给右侧。ls：列举目录的程序，more：分屏逐屏输出文字。

4. [2021.912.3]

   每个进程有且仅有⼀个PCB

   正确。PCB（Process Control Block）进程控制块。用来描述进程状态信息。

5. [2020.912.8]

   PCB中的当前工作目录可以加速文件的查找

   正确。相当于相对路径来获取文件

6. [2021.912.5]

   如果系统中有M个进程，那处于就绪队列中的进程数最多为M-1

   正确。系统非阻塞状态时，每个时刻必然有至少1个进程处在运行态。而如果系统阻塞，则所有的进程都会变成阻塞态，任何进程都不是就绪态。

7. [2021.912.6]

   如果⼀个父进程在有许多子进程的状态下退出了，它的子进程将变为僵⼫进程。

   错误。应该是变成孤儿进程。父进程没了子进程通常会被结束掉，但是如果还在继续运行，则子进程变成ppid为空（没有父进程）的进程。
   
   

### 处理机调度

- SJF即短作业优先调度算法，会导致全去调短作业了，长作业长时间得不到调度。

- RR（时间片轮算法）在时间片增大的时候会退化成FCFS（先来先服务算法）。

- CFS（完全公平调度算法）。

1. [2020.912.2]

   SJF调度算法可能出现饥饿现象。

   正确。SJF即短作业优先调度算法，会导致产生饥饿（全去调短作业了，长作业长时间得不到调度）。

2. 

并行：多个任务同一时刻进行、并发：多个任务看似同一时刻进行、异步：多个任务轮流进行

### 同步互斥

- 自旋锁是自己判断自己是否被占用，被占用的话就等待。

  - ```cpp
    struct flag{
        bool is_use;
    }
    flag lock;
    while(lock.is_use){}
    lock.is_use = false;
    ```

  - 故自旋锁不会因为先来后到而按顺序分配谁先得到运行。

- 类似的，管程也是通过上面这种信号量来管理，设置一个带数值的结构体，判断资源占用情况。

1. [2022.912.1]

   在单核 CPU 中，进程可以通过屏蔽/使能硬件中断中的机器指令来实现同步互斥

   正确。通过资源锁实现一个资源单位时间只能被一方占用。同步方法：1.单核处理器可：禁用中断。2.软件同步上下文实现。3.原子类型指令使得上下文同步。

2. [2022.912.5]

   先来先服务算法（FCFS）可以解决进程间死锁的问题

   错误。FCFS顾名思义只是让先来的进程不至于一直被其他进程抢占资源。死锁可以是通过`死锁预防`（不允许系统进入死锁状态） `死锁避免`（只允许不出现死锁的进程请求资源）`死锁检测和恢复`（死锁以后恢复其资源） `由应用程序处理`（让用户自己去处理死锁的情况）

3. [2022.912.12]

   以下是软件同步算法的伪代码，要求支持线程p[0]和p[1]的临界区访问

   (1) 解释该代码的原理；(2) 完成填空，配合必要的注释

   ```assembly
   variables 
   	wants_to_enter: array of two booleans
   	turn: integer
   wants_to_enter[0] <- false
   wants_to_enter[1] <- false
   turn <- 0 //1
   ```

   线程p[i]的算法伪代码（i取值为0或1）：

   ```cpp
   wants_to_enter[i] <- ①
   while(wants_to_enter[②]){
   	if(turn ③ i){
   		wants_to_enter[i] <- ④
   		while(turn ⑤ i){
   			// busy wait
   		}
           wants_to_enter[i] <- ⑥
   	}
   }
   
   ```

   临界区代码

   ```cpp
   critical_section();
   turn <- ⑦
   wants_to_enter[i] <- ⑧
   // remained section
   ```

   答案:true;1-i;!=;false;!=;true;1-i;false;

   参考Dekkers算法，设置两个flag，flag1设置成true，判断自身能否执行，如果不能执行就等着，直到能执行了就进入临界区，执行完以后释放。以此循环。

   

4. [2021.912.2]

   在用了银行家算法时，系统在不安全状态下会出现死锁

   错误。银行家算法会保证系统一直处于安全状态。即线程申请资源时需要声明最大使用的资源量是多少，系统只会给线程系统自身满足的资源，且使用完成后需要即时归还。此外，系统处于不安全状态的时候也只是真实把资源耗尽了才会死锁。

5. [2020.912.1]

   死锁的充分必要条件是互斥，持有并等待。

   错误。只有互斥（锁）才有死锁出现的可能。而死锁不一定是因为互斥导致的。同时死锁是死占着对方（或多方）要用的锁，使得双方都没法拿另一个锁。

6. [2020.912.3]

   信号量机制可以解决程序死锁问题

   错误。信号量只能声明一个锁，但是循环拿锁的问题没解决。信号量也比较麻烦，总是要记得释放

7. [2020.912.4]

   FIFO算法存在belady现象

   正确。FIFO，CLOCK，改进CLOCK，不恢复计数的LFU会发生belady现象。OPT，LRU，恢复计数的LFU不会。belady现象：后面的进程一直得不到调用。

   FIFO的意思是维护一个队列，队列大小一定，如果队列中存在则命中，**否则缺页，将每次的访问入列**。

   LRU的意思也是维护一个队列，队列大小一定，如果队列中存在则**命中，同时将原先的删除掉，将每次访问入列**，否则缺页。

8. [2016.912期末.20]

   访问频率置换算法（Frequency-based Replacement）的基本思路是，在短周期中使用LFU算法，而在长周期中使用LRU算法

   错误。应该反过来。LFU：Least Frequency Used（最近最不常用页面置换算法）、LRU：Least Recently Used （最近最少使用页面置换算法）

9. [2020.912.7]

   ```cpp
   class semaphore{
       int sem;
       WaitQueue q;
   )
   semaphore::PO {
       [9];
       if ( [10] ) {
       	Add this thread t to q;b1ock(t);
   	}
   )
   semaphore::VO {
       [11];
       if( [12] ) {
       	Remove a thread t from q;wakeup(t);
       }
   }
   
   ```

   sem--;sem<0;sem++;sem<=0。p是申请信号量，v是释放信号量，sem<0则表示进入阻塞态

### 文件系统

1. [2022.912.6]

   在 linux 操作系统中，把外设表示成文件，让应用程序以文件操作的形式来访问外设

   正确。UNIX/Linux万物皆文件。包括各种驱动、系统调用、系统状态等，都模拟成文件了。

2. [2022.912.7]

   在一个硬盘中可以存在多种不同的文件系统

   正确。硬盘是可以分多个区的，每个区可以分别格式化成不同大小、不同格式。

3. [2020.912.5]

   最短寻道时间算法在SSD存储设备中无效

   正确。SSD（固态硬盘）不属于磁表面存储器，SSD是固态电子存储芯片阵列制成的硬盘。固态硬盘不用磁头，寻道时间几乎为0。

4. [2020.912.6]

   延迟写操作可以减少对磁盘的访问次数

   正确。根据时间局部性原理，最近被访问的数据有可能再次被访问，因此当数据更改之后不马上写回磁盘，而是继续放在内存中，以备接下来的请求读取或者修改，是减少磁盘IO的一个有效手段。同样的，提前读也可以减少对磁盘的访问次数

5. [2020.912.7]

   删除一个文件，该文件的所在的当前目录将改变

   正确。目录将会被删除（这里的目录指的是广义的，文件、文件夹、链接等都叫一个目录）

6. [2020.912.9]

   设文件F1的当前引用计数值为1，先建立文件F1的符号链接（软链接）文件F2，在建立文件F1的硬链接F3，然后删除文件F1.此时，文件F2和文件F3的引用计数分别是（ ）

   1；1。软链接是创建一个inode快捷方式，指向一个目录，这个目录存在与否无所谓。它只是个快捷方式、不影响引用目录，更不会影响源文件的计数。硬链接是直接指向同一个文件，使得源文件引用计数+1，每次删除文件时，源文件count-1，count到0的时候删除该文件。

7. [2019.912期末.10]

   设初始情况下，一个一般文件file1的当前引用计数值为1，如果先建立file1的符号链接（软链接）文件file2，再建立file1的硬链接文件file3，然后再建立file3的硬链接文件file4。此时，file3和file4的引用计数值分别是 （---14---）和（---15--- ）。

   3；3。1->2，1=>3=>4，引用计数仅和硬链接相关，且只和源文件计数相等，故此处1/2/3都是链接到源文件，计数为3.

8. [2020.912.10]

   UNIX索引结构存放的位置是（）

   A. 超级块 B.索引节点

   B。索引节点sfs_disk_inode是用来记录索引的，索引结构也在这里。目录也是一种文件，也有inode。

9. 

### IO子系统

1. [2021.912.7]

   操作系统中通信可以使用消息队列、信号、信号量、管道，说明下列操作中最适合使用哪种通信机制，并解释为什么。

   (1) 输入指令关闭一个进程

   (2) linux指令 "cat file | grep exam"

   (3) 第一个进程对一段数据进行写入，另一个进程基于写入的数据对齐进行排序

   

   (1) 信号；信号可以有效地传递给进程告知进程进行什么操作。kill -9 进程pid来关闭。

   (2) 管道；|符号表示管道，使用管道将file文件的内容输出传递给了grep，并筛选exam文字

   (3) 消息队列；因为数据写入是动态（全双工）的，消息队列支持不断将数据传递给消费者。

2. 





## 计算机组成原理

### 基本组成

1. [2021.912.12]

   冯诺依曼计算机最⼤的特点是？

   计算机有**运算器、存储器、控制器、输入设备和输出设备**五大部件组成指令和数据以同等地位存放于存储器内。并可**按地址访问**。
   **指令和数据**均可用二进制表示。指令由操作码和地址码组成。**操作码**表示操作的性质、**地址码**表示操作数在存储器中的位置。
   指令**在存储器中按顺序存放**。通常，指令时顺序执行的。在特殊情况下，可根据运算结果或指定的条件来改变运算顺序。
   机器以**运算器为中心**，输入输出设备和存储器之间的数据传送通过运算器完成。

   - 冯.诺依曼结构的计算机
     “存储程序”计算机，设置内存，存放程序和数据在程序运行之前将程序调入内存，然后执行程序

   - 计算机的功能是执行程序
     程序是依次排列起来的指令序列

   - 计算机执行程序的基本过程
     从程序首地址开始执行第一条指令
     (分步)执行每一条指令，并形成下一条待执行指令地址自动地连续执行指令，直到程序的最后一条指令

- 组合逻辑 时序逻辑
  - 组合逻辑：用于算术、分支选择等
  - 时序逻辑：用于暂存储

### IEEE754

**真值：**所谓真值，其实就是我们数学意义上理解的带有正负号的数字；
**原码：**原码就不用说太多了，就无非是要将一个非二进制数转化为二进制数，并且如果是负数的话记得把最高位写为1.
**反码：**老生常谈，正数的反码是他本身，负数的反码是在其原码的基础上,符号位不变，其余各位取反。
**补码：**正数的补码还是本身，负数的补码是在原码基础上除符号位都取反，然后进1
**移码：**在二进制存储中，补码的符号位取反即是移码，由于浮点数的特殊性，于是引入了移码用来解决浮点数中阶码的问题。

- 浮点数计算

  > 浮点二进制=符号+阶码+尾数
  > 尾数是转换为二进制后的小数点后面的数.
  >
  >
  > - 例如-2017就是-111 1110 0001 = -1.11 1110 0001 * 2^10，阶码为127+10=137，尾数为小数点后面的。
  > 137 = 1000 1001
  > - 结果为 1（符号） 1000 1001（阶码） 11 1110 0001（尾数）
  > - 然后补齐到32位，按小端序 1100=C 0100=4 1111=F 1100=C 0010=2
  > - 故为C4FC2，补齐到4个字节，得到0xC4FC2000
  > 最后转换得到1 100 0100

1. [2022.912.7]

   4字节补码能表示的最大的数为0x____?, IEEE754能表示的最大的数，规格化后表示为0x_____?

   0x7fffffff，0x7fffffff。因为是4个字节，而补码要求有符号，故第4字节只能用一半，为0xff ff ff ff的一半，即0x7f ff ff ff。规格化数：第一位是1的就是规格化数。

2. [2021.912.6]

   IEEE单精度浮点数表示的范围

   A.正数多 B.负数多 C.一样多 D.不确定

   C。因为尾数是原码表示，正负数一样多

3. [2021.912.10]

   short类型变量⾼字节为01H 低字节为FFH 在⼤端表示的机器和⼩端表示的机器中，变量的值分别是多少

   大端：01FF，小端FF01。short类型是2字节的，故其值为01FF。大端是按正常书写顺序写的，小端则是反过来存储（现代化的架构基本都是小端存储）。

4. [2019.期末.10]

   十进制数66.375在IEEE754单精度浮点数标准下表示为：_______。(16进制表示)。

   0x4284C000。先将10进制转换为二进制，则有64\*1+2\*1 . 0.5\*0+0.25\*1+0.125\*1 = 1000010.011。规格化该数，得到1.000010011 * 2^6 ，即阶码为127+6=133（二进制10000101），拼接 符号（0）+阶码（10000101）+尾数（000010011），得到 0100（4） 0010（2） 1000（8） 0100（4） 1100（C），化为大端16进制，4284C，单精度，故补齐到4字节，得到4284C000。

### 指令集

1. [2016.912期中.17]

   一台有完整的层次储存器的MIPS计算机，LW指令访存的最少次数为__。

   0次。当有缓存的时候无需访存，直接从缓存中便可取到

#### 指令系统：RISC和CISC

- RISC（Reduced Instruction Set Computer） **如MIPS**
  通常称为**精简指令**系统的计算机。提供**数目较少、格式与功能简单、运行高效的指令**，追求的是计算机**控制器实现简单，运行高速**，更容易在单块超大规模集成电路的芯片内制做出来。指令并行性好。
- CISC（Complex Instruction Set Computer） **如X86**
  通常称为**复杂指令**系统的计算机，是相对于RISC一词提出来的。其特点是：**指令条数多，格式多样，寻址方式复杂，每条指令的功能强**，优点是汇编程序设计容易些，但计算机**控制器的实现困难多**，很多指令被使用的机会比较少。**指令并行度差**。

1. [2022.912.8]

   X86和MIPS。A. x86指定字长 B. MIPS是RISC指令集 C. x86指令集属于RISC指令集 D. MIPS指令支持间接寻址方式

   B。A.x86支持16位32位64位等，C.x86明显是CISC，D.MIPS是RISC，不支持如此复杂寻址方式

2. [2020.912期末.5]

   li x10,0x12345EEF的汇编指令序列

   lui x10,0x12346; addi x10,x10,0xEEF。li是一个伪指令，等价于 lui x10,前5位;addi x10,x10,后3位。同时当发生进位的时候，将前一位相加后取个位数。即123456+E=12345。


- 并行总线 串行总线 同步总线 异步总线
  - 在cpu时钟频率低的情况下并行快于串行，而现代cpu时钟频率很高，导致并行的多个信号之间相互干扰，从而速度低于串行。
  - 异步总线速度永远低于同步，因为同步是只干一件事，异步是干了就等着

#### 指令执行

1. [2022.912.11]

   一个32位的总线系统，200MHz，2个时钟周期，总线的带宽是
   A.200MB/s.B.400MB/s. C.600MB/s D.800MB/s

   B。带宽=单字节带宽*频率/时钟周期 = 3流水线2b * 200M/s / 2 = 4B * 200M/s /2 = 400MB/s

2. 执行同一条指令，下列用时最短的是

   A.主频2.5GHZ CPI 1 B.主频2.8GHZ CPI 1.1 C.主频3GHZ CPI 1.5 D.主频2GHZ CPI 1.1

   B。时间 = 指令数 * CPI / 频率，故B最小

### 中断

1. [2022.912.1]

   中断处理过程中会记录被中断指令的PC值。

   错误。中断**响应**过程中会保存断点，即中断指令PC值。异常和中断步骤：1.检测：内部中断则设置Cause寄存器，外部则不管。2.响应：保存EPC和程序状态寄存器。3.处理：保存通用寄存器。4.返回：回到中断的地方继续执行

2. [2020.912.13]

   MIPS中断中不是由硬件负责的是（）
   A.开中断 B.保存通用寄存器 C.保存异常原因 D.关中断

   B。保存通用寄存器属于保护现场，由中断服务程序（软件）完成。

3. [2019.912期末.6]

   MIPS响应异常和中断的硬件流程包含 I.保存PC寄存器 II.保存所有通用寄存器 III.恢复PC寄存器 IV.保存异常原因 V.读取异常原因
   A.l，ll，III B.ll，III，IV C.，l，III，IV  D.l，IV，V

   C。产生异常时，CPU干的事：保存断点，关闭中断功能，保存异常原因，进入异常处理入口。

### 数据冲突

1. [2022.912.2]

   调整指令顺序会解决数据冲突

   正确。就是编译器调度的做法，数据冲突是因为前面的指令调用了后面指令的依赖，所以先算后面的指令就行

2. [2021.912.9]

   不可用于解决数据冲突的是 A.旁路 B.阻塞 C.动态预测 D.动态调度/编译器调度

   C。动态预测是解决CPU控制冲突

### 寄存器、流水线

- 流水线 单周期 多周期
  - 单周期则每个周期为所有阶段延迟的总和+PC寄存器锁存延迟，取所有指令中延迟最大的作为周期延迟。每条指令的时间均为一个周期。
  - 多周期则每个周期为输入输出的延迟+所有阶段中延迟最长的（每个阶段都要加PC寄存器锁存延迟）。每条指令时间根据指令类别判断。
    - 指令周期数，j:2,分支类:3,寄存器型:2,Sw指令:4,Lw指令:5
  - 流水线则每个周期同多周期一样。指令延迟均为5个周期。

1. [2022.912.3]

   流水线阶段寄存器对系统软件程序员是否透明

   正确。完全硬件管理，所以对程序员透明

2. [2022.912.12]

   5．关于ALU超前进位的描述正确的是:
   A.加速进位 B.提高精度

   A。

   **![image-20221113213924777](https://raw.githubusercontent.com/serfend/res.image.reference/main/image-20221113213924777.png)**

3. 

#### 流水线

- 指令执行的5个阶段 **IF（取指） ID（译码） EXE（执行） MEM（访存） WB（写回）**

  - 因为流水线效应，故可以同时开始执行多个阶段
    - 后一条指令依赖前一条指令的结果时：
      - 当**使用数据旁路的情况下**在上一阶段的**EXE**阶段即可执行**ID**，在上一阶段的WB阶段执行EXE及后面的指令。
      - 如果没有数据旁路，则需要到上一阶段的**WB**才能执行**ID**以及后面的。
  - 各阶段执行时间 IF(内存延迟) ID(读寄存器延迟) EXE(ALU延迟) MEM(内存延迟) WB(写寄存器延迟) PC(PC输入延迟)
  
  1. [2022.912.13]
  
     一个五级流水的MIPS L1 cache 采用指令缓存和数据缓存分别存放，可在一个时钟周期内完成缓存读写（与寄存器时钟周期同步)现有如下指令已经存入缓存:
  
     ```ass
     lw r1 0(r2); r1 <- mem[r2]
     sub r4 r1 r5; r4 <- r1-r5
     and r6 r1 r7; r6 <- r1 & r7
     or r8 r1 r6 ; r8 <- r1 | r6
     ```
  
     1)在无数据旁路的情况下，有多少指令会产生数据冲突?需要多少个时钟周期完成这些指令?
     2)在有数据旁路的情况下，需要多少个时钟周期完成这些指令﹖需要插入多少个气泡?请说明原因。
  
     
  
     （1）答案: sub、and和or指令会发生数据冲突，需要12个时钟周期。
  
     因为无数据旁路，sub的r1寄存器值需要在lw指令的wb阶段才能拿到，所以要暂停2个周期;同理or指令的r6寄存器也是，要在and指令的wb阶段才能拿到r6寄存器的值。
  
     **![image-20221113213814088](https://raw.githubusercontent.com/serfend/res.image.reference/main/image-20221113213814088.png)**
  
     （2）答案:9个周期;需要插入1个气泡。
  
     有数据旁路的情况下，LW指令在MEM阶段取出来的r1寄存器值可以直接转发给SUB指令的EXE阶段的ALU输入,而AND指令在第5时间周期可以拿到r1寄存器的值了，所以SUB指令需要插入1个气泡，AND指令不用。AND指令在EXE算出来的r6寄存器的值也可以直接转发给OR指令的EXE阶段的ALU输入，所以也不用插入气泡。
  
     **![image-20221113213822695](https://raw.githubusercontent.com/serfend/res.image.reference/main/image-20221113213822695.png)**


1. [2021.912.13]

   ```assembly
   LW R4 0(R5)
   ADD R6 R4 R3
   SUB R8 R7 R5
   ```

   (1)有哪些指令和寄存器存在冲突?
   (2)不加数据旁路的情况下至少需要阻塞几个周期?
   (3)加了数据旁路至少需要阻塞几个周期，并说明每个冲突中旁路数据来源于那个阶段寄存器	

   

   (1) LW与ADD指令的R4寄存器冲突

   (2) 至少需要2个阻塞周期，ADD在EXE和MEM阻塞

   **![image-20221114101410475](https://raw.githubusercontent.com/serfend/res.image.reference/main/image-20221114101410475.png)**	

   (3) 阻塞1个周期，ADD在MEM阻塞

   **![image-20221114101436336](https://raw.githubusercontent.com/serfend/res.image.reference/main/image-20221114101436336.png)**

2. [2019.912期末.8]

   下列关于通过数据转发来解决数据冲突的描述中、正确的是8.(流水线阶段标识: EX为执行阶段、MEM为访存阶段，WB为写回阶段)

   A.只能转发EX/MEM流水线寄存器到ALU的输入
   B.只能转发MEM/WB流水线寄存器到ALU的输入
   C.在EX/MEM流水线寄存器和MEM/WB流水线寄存器对应的寄存器都进行转发的时候、选择MEM/WB流水线寄存器的值
   D.在EX/MEM流水线寄存器和MEM/WB流水线寄存器对应的寄存器都进行转发的时候、选择EX/MEM流水线寄存器的值

   D。EX/MEM、MEM/WB流水寄存器的值都有可能转发到ALU；需要将结果尽快送到需要它的部件，所以选择EX/MEM的值。

   

DRAM（动态存储器Dynamic  Random-Access Memory） SRAM（Static  Random-Access Memory）

1. [2022.912.4]

   静态存储断电后仍然保存数据

   错误。静态存储器（比如内存）具有电易失性，断电后数据消失。

2. 




### 缓存

- 高速缓冲器的映射方式
  - 直接映射
  - 全相连映射
  - 组相连映射

1. [2022.912.5]

   对于32位按字节编址系统，cache行大小为8B，有4行，初始状态为空，先有以下访问顺序：0x100,0x110,0x120,0x130, 0x100,0x110,0x120,0x130。使用直接映射，命中几次？使用全映射，命中几次

   **![image-20221113205522771](https://raw.githubusercontent.com/serfend/res.image.reference/main/image-20221113205522771.png)**

2. [2020.912.8] TLB

   关于TLB的说法正确的是

   A.忘了  **B.**TLB的缺失能在指令cache中找到  **C.**TLB会引发程序错误  **D.**TLB中保存了虚拟地址到物理地址的映射

   D。TLB快表（Translation Lookaside Buffers） B能在**数据**cache找到，指令cache都是指令；C不会引发程序错误，中断处理完程序能继续运行。依托于页表，页表没了它也就没了。

3. [2020.912期末.4] Cache

   增大块大小，可以降低缺失率

   错。缺失率是随块大小先降低随后又升高的（因为块数会变少）。块大小越大，单次查询时间越长，缺失的损失也就越大，于是平均访问时间也是先降低后升高。容量*路数*缺失率=K（常数）

4. [2019.912期末.15]Cache

   某计算机内存系统中，已知Cache访问时间为20ns，主存访问时间为100ns，CPU执行一段时间，有5000次内存系统访问，其中访问主存450次。那么Cache的命中率为_\_\_\_，CPU内存平均访问时间为\_\_\_\_。

   命中率=（5000-450）/5000 = 91%；平均访问时间=(4500\*20 + 500 \* 100) / 5000 = 29ns。正常算就行，挺好记的。

5. 假定不采用Cache和指令预取技术，且机器处于开中断状态，则在下列有关指令执行的叙述中，错误的是

   A.每个指令周期中CPU都至少访问内存一次
   B.每个指令周期一定大于或等于一个CPU时钟周期
   C.空操作指令的指令周期中任何寄存器的内容都不会被改变
   D.当前程序在每条指令执行结束时都可能被外部中断打断

   C。考点: cache、指令周期、时钟周期、nop指令指令周期: 是指计算机从取指到指令执行完毕的时间。时钟周期:是计算机中最基本的、最小的时间单位。在一个时钟周期内，CPU仅完成一个最基本的动作.
   A.每个指令周期都会访存，所以至少会访问一次内存，正确
   B.指令周期包含若干时钟周期，正确
   C.流水线中关于冒险的那章有提及空操作指令nop，若清楚流水线中执行nop时cpu具体做了什么(认真看看黑risc-v版4.7节的内容)，这题是很容易做出来的，比如在解决数据冲突时执行nop就会让pc保持不变、IF/ID段寄存器不变、其余控制信号要置0使之不进行任何写入操作，所以保存了要置0的控制信号的流水段寄存器的内容是会改变的。要真正理解这题需要把流水线搞懂先。

   D.因为处于开中断，正确

6. [2019.期末.2]

   下列不属于缓存缺失的情况是 A.必然缺失  B.容量缺失  C.页面缺失  D.冲突缺失

   C。只要问缺失那么就是容量、必然、冲突。

7. [2020.912.5]

   缓存原理利用了程序的局部性。

   对。局部性原理包括时间局部性与空间局部性。时空局部性是指在最近的未来要用到的信息，很可能是现在正在使用的信息，因为程序中存在循环。空间局部性是指在最近的未来要用到的信息，很可能与现在正在使用的信息在存储空间上是邻近的。

#### 相联方式

1. [2021.912.11]

   32位地址空间，1024个cache块，⼆路组相连，块内8字节，需要多少位的cache标识和索引

   20；9。

   

2. [2021.912.4] 

   Cache 总容量⼀定的话，全相连组织⽅式的命中率不低于组相连⽅式的命中率。

   正确。全相连顾名思义比组织相连连的更多，更容易命中

### 存储

#### raid

raid0 简单存储（1个盘直接存）。
raid1 简单备份（2个盘备份）。
raid2 带海明码校验。
raid3 带奇偶校验码并行传送（只能查错不能纠错，对所有盘传输）。
raid4 等价单个盘版本的raid3。
raid5 分布式的奇偶校验（N+1块盘）（只对一块盘传输）。
raid6 等价于2个冗余盘的raid5（N+2块盘）。raid7 每个盘都有芯片。raid10 高可靠高性能盘。

1. [2022.912.6]

   Raid5为4+1结构，前四个数据块的数据为0x11,0x22,0x33,0x44，现在第五个数据块发生错误，要恢复第五个数据块，则恢复后的数据块数据为0x     ?

   0x44。恢复就是将前面其他块的数据求xor，将数据转换成二进制后异或即可。0x11 ^ 0x22 ^ 0x33 ^ 0x44，而0x22 = 0x11<<2，故0x11 ^ 0x22 = 0x33，而0x33 异或自己等于0，故结果为0x44。

2. RAID5 和 RAID4 比较，检错纠错能力更高。

   错。二者检错能力一致，只是RAID5把校验位分布在每个硬盘上，均衡负载。

#### 层次存储

1. [2022.912.10]

   层次存储系统
   A.增加了主存容量 B.实现了时间局部性 C.实现了空间局部性 D.提高了计算机性能
   D。考点:层次存储系统。高速度，静态存储器速度高；设置较小容量的高遗缓冲存储器。大容量，动态存储器价格适中，速度适中，可作为主存储器。低成本，磁盘存储器价格低廉，作为辅助存储器，暂存CPU访问频率不高的数据和程序，作为虚拟存储器的载体

#### 直接存储访问

DMA（直接访问存储）

- 实现IO和主存之间高速传输
- 数据传输由DMA自行控制
- 数据传输开始前和结束后通过程序中断对DMA进行预处理和后处理
- DMA工作方式：独占总线、周期窃取

1. [2020.912.5]

   DMA不能独占总线周期

   错误。DMA工作方式就是独占总线，并窃取周期

   **![image-20221114080512501](https://raw.githubusercontent.com/serfend/res.image.reference/main/image-20221114080512501.png)**

2. [2016.912期中.27]

   17.下列关于中断/O方式和DMA方式比较的叙述中，错误的是
   A.中断I/O方式请求的是CPU处理时间，DMA方式请求的是总线使用权

   B.中断响应发生在一条指令执行结束后，DMA响应发生在一个总线事务完成后

   C.中断I/0方式下数据传送通过软件完成，DMA方式下数据传送由硬件完成

   D.中断I/O方式适用于所有外部设备，DMA方式仅适用于快速外部设备。

   

   D。解析:中断处理方式:在I/O 设备输入每个数据的过程中，由于无需CPU干预，因而可使CPU与I/O设备并行工作。仅当输完一个数据时，才需CPU花费极短的时间去做些中断处理。因此中断申请使用是CPU处理时间，发生的时间是在一条指令执行结束之后，数据是在软件的控制下完成传送而DMA方式与之不同。DMA方式:数据传输的基本单位是数据块，即在CPU与I/O设备之间，每次传送至少一个数据块:DMA方式每次申请的是总线的使用权，所传送的数据是从设备直接送入内存的或者相反:仅在传送一个可整块数据的传送是在控制器的控制下完成的。多个数据块的开始和结束时，才需CPU干预，答案D的说法不正确，中断方式并不适用于所有设备，比如为了提高数据传送速度，高速外设中普遍采用DMA方式传送数据考点: I/O方式 PPT869



## 计算机网络

### 纠错码/检错码

1. [2021.912.3]

   循环冗余码多项式为$x^2+x+1$时下列哪项是对的。

   1 1 1。循环冗余码，故取多项式系数

#### 海明码

1. [2022.912.1]

   海明纠错码，为了纠正 n 个错，海明纠错码的最短码距是_____.

   2n+1。解析：检测n位错，码距为n+1；纠正n位错，码距为2n+1；

2. [2019.912期末.11]

   使用海明码数据传输，设数据位k=3(D3D2D1)，校验位r=4(P4P3P2P1)，数据D3D2D1=011的编码结果为(按照P1P2D1P3D2D3P4的顺序) ：____________。

   0111100。海明码纠错，且D3D2D1=011，则P1 = D1 ^ D2 = 0，P2 = D1 ^ D3 = 1，P3 = D2 ^ D3 = 1，P4 = 所有求异或 = 0。按题目要求顺序为P1P2D1P3D2D3P4填入，得到答案。

### OSI模型

- OSI七层模型 物理层、链路层、网络层、传输层、会话层、表示层、应用层。

  - 物理层：物理传输介质如光纤、无线、网线等。中继器、集线器
  - 链路层：链路数据信息交换、MAC地址。网桥、二层交换机
  - 网络层：路由交换、IP地址。三层交换机、路由器
  - 传输层：数据包、帧等切分、可靠性保证、端口号。
  - 会话层：建立会话管理、握手。
  - 表示层：数据编码加密等。
  - 应用层：应用程序数据交互。

- 网络协议

  - IPv4协议：分片与重组、IPv4地址

  - ICMP协议： ICMP报文封装在IP分组中

  - ARP协议：ARP协议工作过程

  - RARP协议：RARP与BO0TP的区别

  - RIP协议：内部网关协议、**距离向量**算法、基于UDP

  - OSPF协议：内部网关协议、**链路状态**算法、分层思想、四种类型路由器

  - BGP协议：外部网关协议、**路径向量**算法、基于TCP

  - CIDR协议： CIDR的思想（加掩码以缓解ipv4不够用）、IP地址分配和掩码配置、最长匹配原则

  - IPv6协议：IPv6与IPv4的主要区别（128位对比32位）、IPv6地址、IPv4/IPv6过渡（支持转换）



1. [2022.912.1]

   ISO/OSI模型中的_____层会在处理协议元数据的时候在数据首尾添加信息

   数据链路层。首部是前同步码，可以使接收方和发送方的时钟同步。尾部信息含有CRC校验码，可以用来检验信息在传输来的过程中是否出错。

### 物理层

1. [2020.912.1]

   以下设备只工作在物理层的是(   )。路由器、中继器、交换机、网桥

   中继器。

2. 数据在模拟电路中传播需要的设备是（） A.调制解调器 B.编码解码器

   A。调制解调器是为物理层的。B是IP信号才有的东西

3. 电话网络和TCP网络的性质的比较，回忆版不完整

   电话网采用电路交换，tcp网络没听过？

4. 蜂窝移动⽹络六边形,频率840HZ，每个单元可使用最大频率个数

   280Hz。六边形蜂巢结构几何上，平均利用为3个，故每个单元最大可用840/3=280Hz



### 数据链路层

#### IEEE802系列

1. [2022.912.3]

   IEEE 802.3局域网中使用的 MAC 协议是____.

   CSMA/CD。IEEE 802系列标准定义了若干种LAN,包括对物理层、MAC子层的定义和描述。它的组成如下:

   - 802.1基本介绍和接口原语定义

   - 802.2逻辑链路控制(LLC)子层.
   - 802.3采用CSMA/CD技术的局域网
   - 802,4采用令牌总线（Token Bus)技术的局域网
   - 802.5采用令牌环(Token Ring)技术的局域网

2. [2022.912.6]

   以下哪一个属于使用了时槽周期的MAC协议

   A.非坚持型CSMA B.1-坚持型CSMA C.p-坚持型CSMA D.纯ALOHA

   C。判断时槽是否被占用，如果占用则等待下一个周期，否则以概率P决定是否发数据。如果产生冲突则随机等待一个时间后再发。

3. [2022.912.7]

   链路层成帧的方法不包括

   A.偏移量法 B.物理层编码违例法 C.带位填充首尾字节标记法 D.字符计数法

   A。字符统计法几乎所有链路协议都用，物理层编码违例法、带字符填充首尾字节标记法、带位填充首尾字节标记法 是组帧（将比特流分散成帧、判断每个帧校验和）方法

4. [2022.912.10]

   电路交换和虚电路分组交换共同点
   I.分组有序 II.设备端口带宽预约占用 III.不会产生拥塞
   A.l、II、II B.I、II C.I、II D.l

   B。电路交换和虚电路分组交换都能保证分组有序，因此1正确，二者传输数据前都需要建立连接，因此2正确。电路交换建立的是物理连接，同一个线路只有一个连接使用该线路，不会拥塞，而虚电路分组交换建立的是逻辑链接，同一个结点可能为多条虚电路服务，进而产生拥塞。因此3错误。

5. [2021.912.2]

   CSMA/CD的链路，数据传输率是1Gbps，数据传播速率200000km/s问最小帧长增加50个字节后，最远两节点间距离应该
   A.增加40m B.减少40m C.增加80m D.减少80m

   A。一个站点确定发生冲突的时间最坏情况下是2倍电缆传输时间，所以
   最小帧长 = 总线传播时延\*数据传输率\*2;总线传播时延 = 两节点距离/数据传播速率。

   由公式可知，最小帧长增加，则最远两节点距离也增加，得:50B * 8b/B = 数据传输率 \*2 \* 两节点距离 / 数据传播速率 =>  400 = $10^6$ \* 2 / 2\* $10^5$   * 两节点距离，两节点距离 = 40米。

   同样的题还有[2019.912.1] 以太网中最短帧长1000bit，最远两点相距离100m,数据在光纤中的传播速率为2*10^8m/s,问最大发送速率A.1Gb/s B.2Gb/s C.100Mb/s D.200Mb/s。由最小帧长 = 总线传播时延 * 数据传输率 * 2 可得 1000bit  = 100米 / 2*10^8m/s * 2 * 发送速率 ，得发送速率 = 10^8 = 1Gb/s

6. 

   

### 网络层

1. [2022.912.8]

   哪一个网络设备工作在网络层 A.集线器 B.路由器 C.网桥 D.中继器

   B。物理层：集线器，中继器；数据链路层：网桥；网络层：路由器；

2. [2021.912.5]

   5考虑图5.13(a)中的子网。该子网使用了距离矢量路由算法，下面矢量刚刚到达路由器C:来自B的矢量为(5,0,8,12,6,2);来自D的矢量为( 16,12,6,0,9,10);来自E的矢量(7,6,3,9,0,4)。经测量到B、D和E的延迟分别为6,3和5.请问C的新路由表将会怎样?请给出将使用的输出线路以及期望的延迟。
   注意路由不对称性，到B、D、E使用自身测算的延迟
   这个题图一样，不过数不一样，求C的路由表
   1．如果C使用链路状态路由算法，则C发送的链路状态信息是?
   2．依据上图，每个路由器连接一个子网，每个子网内依次有90，78，4，15，3，40，2(数是编的不过应该差不多)给了一个子网为55.16.22.0/24(也是编的，知道/24就行)求一个合理的子网划分，写出每个子网的范围和对应子网掩码
   3.最后一道大题似乎是和滑动窗口协议相关的（没做完没来得及读题QAQ…写数据结构去了了）

   **![image-20221114142030845](https://raw.githubusercontent.com/serfend/res.image.reference/main/image-20221114142030845.png)**

   1.C发送的链路状态信息是C到每个邻居的延迟

   | 目的地址 | 延迟 |
   | -------- | ---- |
   | B        | 2    |
   | D        | 3    |
   | E        | 1    |

   ⒉数据很明显不对呀，90和78都要7位主机号，8位根本不够分，而且有七个子网跟图也不对应。地址划分也是常规题了，参考下其他题就好，比如2019年的路由器大题
   3.题目不完整，应该是考后退n帧，选择重传那些

3. [2020.912.6]

   HOST1和HOST2的地址掩码配置错误，给出默认的网关，然后给了一个路由表中的表项，路由表配置正确
   (1)给出了四个IP请求，分析查询的MAC地址对应于哪个IP,能否收到ARP响应报文

   (2)路由器可以收到四个IP请求中哪些发送的报文

   (3)距离向量的更新，D收到了来自B和C的信息，D到B和C的距离分别为2和3(具体数字可能反了)，D中的路由表项为。

   回忆版题目不全，没法做，可以根据题目描述找类似考点的题目来训练。



4. [2019.912.9]

   (1)如图，网络1有100台主机，网络2有50台，网络3有20台，请将166.111.4.0/24划分给网络并写出路由器接口ip

   (2)简述AB通信时与AC通信时使用ARP协议的具体情况（ARP在同一局域网间的主机通信操作是做什么，在不同局域网间的主机通信操作是做什么?)

   (3)当A发送报文给C时写出各个段上报文的源IP，目的IP，源MAC，目的MAC(用MAC-A,IP-A,MAC-e0等表示)

   **![image-20221114161632631](https://raw.githubusercontent.com/serfend/res.image.reference/main/image-20221114161632631.png)**

   

   (1)图中共需要分为5个部分的网络

   e0-e6是交换机的路由地址，需要配置一个ip。

   1. 网络1的100台主机 + e0 ＋ 2个全0全1的主机号（全0表示网络本身，全1表示网络广播地址) =103<128 = 2^7，需要7位主机号。
   
   2. 网络2的50台主机+e3+ 2 = 53 < 64 = 2^6，需要6位主机号。
   3. 网络3的20台主机+e6 + 2 = 23< 32 = 2^5，需要5位主机号。
   4. 路由地址e1 + e2 +2 =4 = 2^2，需要2位主机号。

   5. e4 + e5 + 2 =4 = 2^2，需要2位主机号。

      因此，网络划分如下

      1. e0: 166.111.4.0 0000001/25 = 166.111.4.1/25
      网络1的100台主机: 166.111.4.2/25 - 166.111.4.101/25，即166.111.4.0 0000010/25-166.111.4.00110101/25
      2. e3: 166.111.4.10 000001/26 = 166.111.4.129/26
        网络2的50台主机: 166.111.4.130/26 - 166.111.4.179/26，即166.111.4.10 000010/26 -166.111.4.10110011/26
      3. e6: 116.111.4.110 00001/27 = 116.111.4.193/27
        网络3的20台主机:116.111.4.194/27-116.111.4.213/27，即116.111.4.110 00010/27-116.111.4.11010101/27
      4. e1: 116.111.4.111000 01/30 = 116.111.4.225/30; e2:116.111.4.111000 10/30=116.111.4.226/30
      5. e4: 116.111.4.11100101/30=116.111.4.229/30; e5:116.111.4.11100110/30=116.111.4.230/30
      
   
   (2)
   
   1. 当A向B发送数据报时，通过B的IP地址发现B与A处于同一个子网中，这时先在A的ARP告诉缓存中查看有没有B的ip地址到硬件地址的映射。如果有，就可以查出B的硬件地址，再将硬件地址写入MAC帧，然后通过局域网将该帧发往B。如果没有，那么使用目的MAC地址为FF-FF-FF-FF-FF-FF的帧来封装并广播ARP分组，此时处于同一局域网的主机都能接收到ARP请求。主机B收到请求后，向主机A发送ARP响应分组(响应分组是单播，只有A能接收到)，分组包含B的IP到MAC地址的映射关系，主机A收到后将此映射存入高速缓存中，然后按查询到的硬件地址发送MAC帧。
      2. 当A向C发送数据报时，通过C的IP地址发现C与A处于不同的子网中，这时A用ARP得到R1的eo的MAC地址，将包发送给R1，然后R1查询IP后，再使用ARP找到R2的e2端口的MAC地址，将包发送给R2，然后R2查询IP地址，发现e3与C处于同一子网，然后使用ARP得到C的MAC地址，将包发送给C。
      
   
   （3）
      | 网段  | 源IP | 目的IP | 源MAC  | 目的MAC |
      | ----- | ---- | ------ | ------ | ------- |
      | 网络1 | IP-A | IP-C   | MAC-A  | MAC-e0  |
      | R1-R2 | IP-A | IP-C   | MAC-e3 | MAC-e2  |
      | 网络2 | IP-A | IP-C   | MAC-e3 | MAC-C   |
   
   
   
   

#### 网桥

1. [2020.912.4]

   在局域网中，解决多网桥互联的回路问题所采用的方法是（）

   A. 水平分裂算法 B. 生成树网桥

   B。通过最小生成树来解决回路问题。

#### IP地址

1. [2022.912.4]

   166.111.67.8/21 的广播地址是_______.

   166.111.71.255。因为是21位掩码，故掩盖了前21位，即A段、B段的各8位，加上C段的5位。而C段IP为67 = 01000011，前5位为01000，即64。广播地址，故后面全部补1，最终地址为01000111.255 =   64+4+2+1.255 = 71.255。

2. 下列正确的是：下列正确的是 l.同一个域名可以拥有多个IP地址 ll.同一个IP地址可以拥有多个域名

   都正确。一个域名可以通过DNS解析的配置，分发到不同的CDN（IP地址）。一个IP地址更是可以通过设置不同域名解析地址指向，绑定到多个域名上。

3. DNS相关，以下正确的是（）

   A.双十—淘宝购物，不同地方的人得到的IP地址可能不同

   B.DNS存储IP是通过二元组的形式

   D.DNS数据库集中存储

   A。一个域名可以对应多个ip地址，智能DNS服务器会根据请求的线路、地理位置等信息综合考虑，返回对于该请求最快的IP。B，DNS的资源记录是五元组。D，DNS数据库是分布式存储。



### 传输层

1. [2021.912.1]

   传输层服务访问点是 A.lP地址，端号 B.IP地址 C.MAC地址，IP地址，端号 D.MAC地址，IP地址

   A。MAC地址是链路层的。

2. [2020.912.3]

   在选择重传协议中，当前发送方的发送窗口为[1,2,3,4]时，收到了一个接收方的否定确认帧，则可能的情况是哪个帧出现了问题____。

   1,2,3,4都有可能。选择重传策略通常跟否定策略结合起来一起使用，即当接收方检测到错误（例如，帧的校验和错误或者序号不正确），它就发送一个否定确认（NAK., negative acknowledgement ）。NAK 可以触发该帧的重传操作，而不需要等到相应的计时器超时，因此协议性能得以提高。所以1,2,3,4都有可能。接收方在收到一个错误的帧时可发送否定确认帧NAK要求发送方重新发送该帧。因为1、2、3、4都有可能出错，因此对应的四个否定确认帧都有可能出现。

3. [2019.912.4]

   停等协议通信线路利用率最低的是，源和目的之间距离很（近/远），速度（快/慢）

   远；快。停等协议中，利用率＝数据帧传输时延/（数据帧传输时延+2*传播时延+确认帧传输时延）。距离越远，传播时延越长；速度越快，数据帧传输时延和确认帧传输时延越小，利用率越低。

4. [2019.912.5]

   由两端链路构成，给出包大小，数字带宽，传输速率，计算延迟【1.5s 1.6s 2.1s 3.1s】 （两个转发加两个传播）

   回忆版条件不全。

   

5. TCP中，拥塞窗口大小W，最大发送段长MSS，给RTT，求平均算出速率近似是多1少

   0.75W*MSS/RTT。执行拥塞避免算法周期内，发送的段数为：(W/2 + 1) + (W/2 + 2) + (W/2 + 3) + … + W = $2^n-1$

   **![image-20221114152427595](https://raw.githubusercontent.com/serfend/res.image.reference/main/image-20221114152427595.png)**

#### TCP协议

1. [2022.912.5]

   TCP中______与定时器结合释放连接.

   三次握手。建立连接是三次握手，释放连接是三次握手+定时器（4次握手）。通过滑动窗口实现可靠传输，通过可变滑动窗口和慢启动、拥塞避免实现流控制。

2. [2020.912.7]

   TCP使用慢启动算法，初始阈值为400KB，接收方接收窗口大小为600KB,

   **<img src="https://raw.githubusercontent.com/serfend/res.image.reference/main/image-20221114145053332.png" alt="image-20221114145053332" style="zoom: 80%;" />**

   

   1 时刻0时，发出第一个包，序号为0;
   2 时刻1时，每当收到时刻0中一个包的确定，拥塞窗口增加100KB，全部接收后(时刻0只有1个包)，拥塞窗口由100KB->200KB。然后发出序号为1和2的包。
   3 时刻2时，每当收到时刻1中一个包的确定，拥塞窗口增加100KB，全部接收后(时刻2有2个包)，拥塞窗口由200KB->400KB。然后发出序号为3、4、5、6的包。此时拥塞窗口达到阈值，开始拥塞避免算法。
   4 时刻3时，当收到时刻2所有包的确定后，拥塞窗口才会增加一个包的大小(400KB->500KB),然后发出序号为7、8、9、10、11的包。
   5 时刻4时，当收到时刻3所有包的确定后，拥塞窗口才会增加一个包的大小(500KB->600KB),然后发出序号为12、13、14、15、16、17的包。
   6 时刻5发生超时，拥塞窗口直接变为一个包的大小(100KB)，阈值变为上一时刻的一半(300KB)，然后发送超时的包12;

​		**![image-20221114145624310](https://raw.githubusercontent.com/serfend/res.image.reference/main/image-20221114145624310.png)**



​		

#### 应用层

1. [2019.912.7]

   解释以下URL各部分的意义http://info.tsinghua.edu.cn:80/index.jsp

   http：协议。info.tsinghua.edu.cn：DNS域名。80：端口号。index.jsp：路径名。

2. [2019.912.8]

   如域名info.tsinghua. edu.cn对应的ip为166.111.4.98，解释为何会发⽣如下现象：
   ①访问http://info.tsinghua.edu.cn/index.jsp 正常，⽽访问http://166.111.4.98/index.jsp 异常②访问http://166.111.4.98/index.jsp 正常，⽽访问http://info.tsinghua. edu.cn/index.jsp 异常。

   第一种：网站使用虚拟主机方式部署，需要通过Host指定；或可能是禁止了以ip方式访问。

   第二种：域名绑定的ip不正确，或本地DNS解析有问题，或大网的DNS被污染。

   