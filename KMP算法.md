# KMP算法

## 模式匹配

串的模式匹配指，在目标串中查找与模式串相等的一个子串并确定该子串位置的操作。

若要**删除或替换**已知字符串中的指定子串，则首先要执行模式匹配操作，在已知串中查找是否有匹配的子串，获得子串位置，再进行查找或替换等操作

首先要了解BF算法，即暴力(Brute Force)算法，是普通的模式匹配算法

**BF算法的思想**就是将**目标串target**的第一个字符与**模式串pattern**的**第一个字符进行匹配**，若相等，则继续比较target的第二个字符和pattern的第二个字符；若不相等，则比较S的第二个字符和T的第一个字符，依次比较下去，直到得出最后的匹配结果。BF算法是一种蛮力算法。

![image-20210502151337852](https://gitee.com/qhzeng/markdown/raw/master/image/image-20210502151337852.png)

Brute-Force 是一种带回溯的模式匹配算法，它将目标串中所有长度为 m 的子串依 次与模式串匹配，如果一次匹配失败，则模式串再与目标串的下一个子串匹配。不存在一个和模式串pattern相等的子串，则模式匹配失败，函数返回-1。

Brute-Force 算法最好情况下的时间复杂度是 O(m)，最坏情况下的时间复杂度是 O(m×n)。

## BF算法实现：

```java
public class BF 
{
    private static int count=0;                            //记载比较次数

    //返回模式串pattern在目标串target中从begin开始的首次匹配位置，匹配失败时返回-1
    public static int indexOf(String target, String pattern, int begin)
    {
        if (pattern!=null && pattern.length()>0 && target.length()>=pattern.length())
        {                                                  //当目标串比模式串长时进行比较
            int i=begin, j=0;                              //i、j分别为目标串和模式串当前字符的下标
            count=0;   
            while (i<target.length())
            {
                if (target.charAt(i)==pattern.charAt(j))   //若当前两字符相等，则继续比较后续字符
                {
                    i++;
                    j++;
                }
                else                                       //否则i、j回溯，进行下一次匹配
                {
                    i=i-j+1;                               //目标串下标i退回到下一个待匹配子串首字符
                    j=0;                                   //模式串下标j退回到0
                }
                count++;
                if (j==pattern.length())                   //一次匹配结束，匹配成功
                {
                    System.out.println("BF.count="+BF.count);
                    return i-j;                            //返回匹配的子串序号
                }
            }
        }
        System.out.println("BF.count="+BF.count);
        return -1;                                         //匹配失败时返回-1
    }
    //返回模式串pattern在目标串target中从0开始的首次匹配位置，匹配失败时返回-1
    public static int indexOf(String target, String pattern)
    {
        return BF.indexOf(target, pattern, 0);
    }
    
    public static void main(String args[]) 
    {
        String target="ababdabcd", pattern="abc";        //图3.10，BF用例
//        String target="aabaaa", pattern="aab";           //图3.13(a)，匹配成功，最好情况
//        String target="aaaaa", pattern="aab";            //图3.13(b)，最坏情况，匹配不成功
//        String target="aaaab", pattern="aab";            //最坏情况，匹配成功
        

        System.out.println("BF.indexOf(\""+target+"\"，\""+pattern+"\")="+BF.indexOf(target,pattern));
    }
}
```



例题：get="aaabaaab"、 pattern="aaaa"， 画出采用 Brute-Force 算法的模式匹配过程，给出比较结果、子串匹配次数和字符比较次数。

------------------------------

<img src="https://gitee.com/qhzeng/markdown/raw/master/image/image-20210502152804459.png" alt="image-20210502152804459" style="zoom:50%;" />

----------------------

<img src="https://gitee.com/qhzeng/markdown/raw/master/image/image-20210502152846239.png" alt="image-20210502152846239" style="zoom:50%;" />

-----------------------------

<img src="https://gitee.com/qhzeng/markdown/raw/master/image/image-20210502152924536.png" alt="image-20210502152924536" style="zoom:50%;" />

------------------------------------

<img src="https://gitee.com/qhzeng/markdown/raw/master/image/image-20210502153001419.png" alt="image-20210502153001419" style="zoom:50%;" />

---------------------------------

<img src="https://gitee.com/qhzeng/markdown/raw/master/image/image-20210502153050257.png" alt="image-20210502153050257" style="zoom:50%;" />

--------------



比较结果：匹配不成功，函数返回-1

子串匹配次数：5次

字符比较次数：4+3+2+1+4=14次



## KMP算法

KMP算法是一种改进的字符串匹配算法，由D.E.Knuth，J.H.Morris和V.R.Pratt提出的，因此人们称它为克努特—莫里斯—普拉特操作（简称KMP算法）。

KMP算法的核心是利用匹配失败后的信息，尽量减少模式串与主串的匹配次数以达到快速匹配的目的。具体实现就是通过一个next()数组实现。（仅仅后移模式串，比较指针不回溯）

<img src="https://gitee.com/qhzeng/markdown/raw/master/image/image-20210503115939575.png" alt="image-20210503115939575" style="zoom:67%;" />

<img src="https://gitee.com/qhzeng/markdown/raw/master/image/image-20210503120009666.png" alt="image-20210503120009666" style="zoom:67%;" />



<img src="https://gitee.com/qhzeng/markdown/raw/master/image/image-20210503115954089.png" alt="image-20210503115954089" style="zoom:67%;" />

KMP函数可按如下方法设计：
假设现在目标串target匹配到 i 位置，模式串pattern匹配到 j 位置



如果j = -1，或者当前字符匹配成功（即t[i] == P[j]），都令i++，j++，继续匹配下一个字符；

如果j != -1，且当前字符匹配失败（即t[i] != P[j]），则令 `i 不变，j = next[j]`。此举意味着失配时，模式串P相对于文本串t向右移动了j - next [j] 位。

换言之，当匹配失败时，

**模式串向右移动的位数为：失配字符所在位置 - 失配字符对应的next 值，即移动的实际位数为：j - next[j]，且此值大于等于1。**

`失配时，模式串向右移动的位数为：失配字符所在位置 - 失配字符对应的next 值`

## next 数组各值的含义：

代表**当前字符之前的字符串**中，有多大长度的相同前缀后缀。例如如果next [j] = k，代表j 之前的字符串中有**最大长度为*k* 的相同前缀后缀**。

| 模式串index |  0   | 1    | 2    | 3    | 4    | 5    | 6    | 7    | 8    | 9    | 10   | 11   | 12   | 13   | 14   |
| :---------- | :--: | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| 模式串      |  a   | b    | d    | a    | b    | c    | a    | b    | b    | a    | b    | c    | a    | b    | c    |
| next数组    |  -1  | 0    | 0    | 0    | 1    | 2    | 0    | 0    | 2    | 0    | 1    | 2    | 0    | 1    | 2    |
|             |      |      |      |      |      |      |      |      |      |      |      |      |      |      |      |

## 求next数组 

<img src="https://gitee.com/qhzeng/markdown/raw/master/image/image-20210504131803467.png" style="zoom:50%;" />



模式串"abcabdabcabcaa"的next数组

| j                                    | 0    | 1    | 2    | 3    | 4    | 5    | 6    | 7    | 8    | 9    | 10   | 11   | 12   | 13   |
| ------------------------------------ | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| 模式串                               | a    | b    | c    | a    | b    | d    | a    | b    | c    | a    | b    | c    | a    | a    |
| "p0…pj-1"中最长相同的前后缀子串长度k | -1   | 0    | 0    | 0    | 1    | 2    | 0    | 1    | 2    | 3    | 4    | 5    | 3    | 4    |

第一次匹配

<img src="https://gitee.com/qhzeng/markdown/raw/master/image/image-20210504140201655.png" style="zoom: 67%;" />

<img src="https://gitee.com/qhzeng/markdown/raw/master/image/20210504142843.png" style="zoom: 67%;" />

第二次匹配，k回到-1，j向前了一位

<img src="https://gitee.com/qhzeng/markdown/raw/master/image/20210504142936.png" style="zoom:67%;" />



<img src="https://gitee.com/qhzeng/markdown/raw/master/image/20210504143047.png" style="zoom:67%;" />





<img src="https://gitee.com/qhzeng/markdown/raw/master/image/20210504143324.png" style="zoom:67%;" />

`j++，k++，next[j]=k=next[4]=1`

```java
private static int[] getNextk(String pattern)          //返回模式串pattern的next数组
{
    int j=0, k=-1;                                   //初始位置的时候，k=-1
    int[] next=new int[pattern.length()];			//声明一个next数组，指定数组长度为串的长度'
    next[0]=-1;                                      
    while (j<pattern.length()-1)                    //一层循环：当索引j的值小于模式串的长度
        if (k==-1 || pattern.charAt(j)==pattern.charAt(k))    //二层循环，k=-1或者模式串j位置的值等于k位置的值
        {
            j++;
            k++;
            next[j]=k;                                 //有待改进
        }
        else k=next[k];
    return next;
}
```







## 改进next数组 

<img src="https://gitee.com/qhzeng/markdown/raw/master/image/20210504143728.png" style="zoom:67%;" />

当p[j] != t[i] 时，下次匹配必然是p[ next [j]] 跟t[i]匹配，如果p[j] = p[ next[j] ]，必然导致后一步匹配失败，所以不能允许p[j] = p[ next[j ]]。如果出现了，则需要再次递归，即

`令next[j] = next[ next[j] ]`



若$P_j≠P_k$:  next[j] = next[j]    改进next数组的值等于原来next数组的值

若$P_j=P_k$:  next[j] = next[ next[j] ]    改进next数组的值等于next[ k ]



**模式串"abcabc"改进的next数组**

| j                                    | 0    | 1    | 2    | 3    | 4    | 5    |
| ------------------------------------ | ---- | ---- | ---- | ---- | ---- | ---- |
| 模式串                               | a    | b    | c    | a    | b    | c    |
| "p0…pj-1"中最长相同的前后缀子串长度k | -1   | 0    | 0    | 0    | 1    | 2    |
| pk与pj比较                           |      | ≠    | ≠    | =    | =    | =    |
| 改进的next[j]                        | -1   | 0    | 0    | -1   | 0    | 0    |

**模式串"abcabdabcabcaa"改进的next数组**

| **j**             | **0**  | **1** | **2** | **3**  | **4** | **5** | **6**  | **7** | **8** | **9**  | **10** | **11** | **12** | **13** |
| ----------------- | ------ | ----- | ----- | ------ | ----- | ----- | ------ | ----- | ----- | ------ | ------ | ------ | ------ | ------ |
| **模式串**        | **a**  | **b** | **c** | **a**  | **b** | **d** | **a**  | **b** | **c** | **a**  | **b**  | **c**  | **a**  | **a**  |
| **串长k**         | **-1** | **0** | **0** | **0**  | **1** | **2** | **0**  | **1** | **2** | **3**  | **4**  | **5**  | **3**  | **4**  |
| **比较**          |        | **≠** | **≠** | **=**  | **=** | **≠** | **=**  | **=** | **=** | **=**  | **=**  | **≠**  | **=**  | **≠**  |
| **改进的next[j]** | **-1** | **0** | **0** | **-1** | **0** | **2** | **-1** | **0** | **0** | **-1** | **0**  | **5**  | **-1** | **4**  |





## 例题：

已知 target="aaabaaab"、pattern="aaaa"，分别画出使用未改进 next 数组和改进 next

数组的 KMP 模式匹配算法过程，给出比较结果、子串匹配次数和字符比较次数。

`令next[j] = next[ next[j] ]`

`失配时，模式串向右移动的位数为：失配字符所在位置 - 失配字符对应的next 值`

| j             | 0    | 1    | 2    | 3    |
| ------------- | ---- | ---- | ---- | ---- |
| 模式串        | a    | a    | a    | a    |
| 串长k         | -1   | 0    | 1    | 2    |
| 比较          |      | =    | =    | =    |
| 改进的next[j] | -1   | -1   | -1   | -1   |

### 未改进next数组：

<img src="https://gitee.com/qhzeng/markdown/raw/master/image/20210504174247.png" style="zoom: 67%;" />



<img src="https://gitee.com/qhzeng/markdown/raw/master/image/image-20210504175440900.png" alt="image-20210504175440900" style="zoom:67%;" />

<img src="https://gitee.com/qhzeng/markdown/raw/master/image/image-20210504175558815.png" alt="image-20210504175558815" style="zoom:67%;" />

<img src="https://gitee.com/qhzeng/markdown/raw/master/image//image-20210504174831416.png" alt="image-20210504174831416" style="zoom:67%;" />

<img src="https://gitee.com/qhzeng/markdown/raw/master/image/image-20210504175118529.png" alt="image-20210504175118529" style="zoom:67%;" />

给出比较结果：匹配失败，返回-1

子串匹配次数：5

字符比较次数：4+1+1+4=10



### 改进next数组

<img src="https://gitee.com/qhzeng/markdown/raw/master/image/image-20210504203405016.png" alt="image-20210504203405016" style="zoom: 80%;" />



<img src="https://gitee.com/qhzeng/markdown/raw/master/image/image-20210504203500088.png" alt="image-20210504203500088" style="zoom:80%;" />

给出比较结果：匹配失败，返回-1

子串匹配次数：2

字符比较次数：4+4=8

