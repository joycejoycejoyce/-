# Data Structure & Algorithm 

## 做题的Structure 
1. 仔细读题目，找出input, output 
虽然听起来像废话可是绝对不是！
在这一个step 之中，理解一个题目的input output 是什么，由此可以推出是否之中需要相应的类型变动。
如果你用的是Java 这样的严谨编程语言的话，这一步有助于你想想最后要将数据类型如何变化。
如果我们用的是JavaScript 这样的弱语言的话，这一步有可能会告诉我们为什么最后的结果出了问题。
2. 用例子找出题目之中的逻辑关系
我们把数字带进去，试图发现其中的逻辑关联。
比如说我们做了一道recursion 题目，我们说: 
input = 2时， output =2;
input ＝3 时， output ＝ 3； 
input＝4， output = 5; 
input =5, output = 8;
那么当我们观察结果时，我们会说， “哦， 似乎input(n)=input(n-1) + input(n-2)”
“看上去有点像recursion”
然后我们来看它是否有recursion 的其他特性，比如说base case. 是有的。所以我们说这题可以用recursion 来解。
3. 这里我们确定了解题方法，找出大概步骤 draft 
我们用comment 写出我们大概的一步步步骤
 1. 写出base case 
 2. 定义一个函数 function 
 3. 调用这个函数
4. implementation 添加细节
这时就添加具体的代码
5. optimizationn 想想改进方法
在确保你的整体思路正确之后，想想是否有什么方法可以增进performance. 减少 time complexity / space complexity.

## Recursion 递归 
其实recursion 的概念我查了好几次我都没看到有什么非常好的解释。 
最形象的一个解释是我在人家的博客上看到的。当我坐在电影院我想知道自己坐在第几排。
我知道  我的排数 =Alexia 排数＋1 ；
于是我问坐在我前面的Alexia， “嘿，你在哪一排？”
 Alexia 的排数 ＝ Sophie +1；
 Alexia 知道他的排数是坐在前面的Sophie, "嘿，你在哪一排？"
 ... 
 直到有一个人说： “我是第1？2？3？排”；

从这个例子我们观察到了几个现象
1. 我们能得到答案的前提是一定要有一个人直到自己在第几排。 
2. 这个询问的动作是一样的 
3. 询问背后的逻辑推导相同


### Instances 
1. Fibonacci Number 
2. Climb Stairs 
一个比Fibonacci Number 更难一点的题目就是Climb Stairs. 也算是一道大家必会的算法题。
我觉得其实学算法的精髓就在于学到一个解决问题的方法。而不是去背题。所以最关键的是学会好的思路并能够自己以后运用这样的思维。
那我们就首先来看看在思维上我们要怎么解决这道题目吧
1. 仔细读题目，找出input, output 
input: number 
output: number 
2. 用例子找出题目之中的逻辑关系

首先，我们来看看这里是否存在某种规律。
比如说在这题中，我们说: 
input = 2时， output =2;
input ＝3 时， output ＝ 3； 
input＝4， output = 5; 
input =5, output = 8;
那么当我们观察结果时，我们会说， “哦， 似乎input(n)=input(n-1) + input(n-2)”
“看上去有点像recursion， 向the previous row ask row number”
然后我们来看它是否有recursion 的其他特性，比如说base case. (anyone know their row number?) 是有的。

   stair = 1; way = 1;

   stair = 2; way = 2;


所以我们说这题可以用recursion 来解。
3. 这里我们确定了解题方法，找出大概步骤 draft 
   1. 在function中添加base case 
   2. 返回前两个台阶的结果 
4. implementation 添加细节
```  
function stepStairs(s){
  // base case 
  if (s<=2){
      let ways = s;
      return ways; 
  }
  // return the previous two options 
  return stepStairs(s-1) + stepStairs(s-2);
}
 
``` 

5. optimizationn 想想改进方法
前面的写法已经可以实现结果了。可是如果我们画图就会发现
``` 

stairs(1) => 1 way 
stairs (2) => 2 ways 
stairs (3) => stairs(2) = 2 ways 
           => stairs(1) = 1 way
           = 3 ways 
stairs(4) => stairs(3) => stairs(2) = 2 ways
                       => stairs(1) = 1 way
                       = 3 ways  
          => stairs(2) = 2 ways
          = 5 ways  
stairs(5) => stairs(4) => stairs(3) => stairs(2)=2 ways 
                                    => stairs(1) = 1 way
                                    = 3 ways
                       => stairs(2) = 2 ways 
                       = 5 ways 
          => stairs(3) => stairs(2) = 2ways 
                       => stairs(1) = 1 way 
                        = 3 ways 
          = 8 ways  

``` 


在我们不断向上循环的过程中， 前面的function 在不断被重算。那么去加快calculation 的方法是否可以
是将前面计算的结果记录下来呢？

| stairs        | ways          | 
| ------------- |:-------------:| 
| 0             | 0             | 
| 1             | 1             | 
| 2             | 2             | 
| 3             | 3             |

那么我们的树就会变成 
``` 
stairs(5) => stairs(4) => stairs(3) table(3) ? no => stairs(2)=2 ways 
                                                  => stairs(1) = 1 way
                                                  = 3 ways
                       => stairs(2) table(2) ? yes = 2 ways 
                       = 5 ways 
          => stairs(3) => table(3) ? yes = 3 ways 
          = 8 ways 


``` 
那么这里面的stairs(3) 就可以直接取table中的value而不用重新计算了。