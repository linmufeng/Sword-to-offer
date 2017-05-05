# 前言
这是一个新的部分，主要是刷剑指offer上的编程题，记录自己的解法，如果看到比较赞的解法，也会放出来，共同学习。

# 题目描述

一只青蛙一次可以跳上1级台阶，也可以跳上2级……它也可以跳上n级。求该青蛙跳上一个n级的台阶总共有多少种跳法。

# 自己的解法

## 思路
f(n) 代表的是n个台阶有一次1,2,...n阶的 跳法数。

1. n = 1时
只有1种跳法，f(1) = 1
2. n = 2时
会有两个跳得方式，一次1阶或者2阶，这回归到了问题（1） ，f(2) = f(2-1) + f(2-2) 
3. n = 3时
会有三种跳得方式，1阶、2阶、3阶，
    那么就是第一次跳出1阶后面剩下：
    f(3-1);第一次跳出2阶，剩下f(3-2)；第一次3阶，那么剩下f(3-3)
    因此结论是f(3) = f(3-1)+f(3-2)+f(3-3)
4. n = n时
会有n中跳的方式，1阶、2阶...n阶，得出结论：
f(n) = f(n-1)+f(n-2)+...+f(n-(n-1)) + f(n-n) => f(0) + f(1) + f(2) + f(3) + ... + f(n-1)

## 代码

```
public class JumpFloorIISolv {
    
    /**
     * 一只青蛙一次可以跳上1级台阶，也可以跳上2级……它也可以跳上n级。
     * 求该青蛙跳上一个n级的台阶总共有多少种跳法。
     * @param target
     * @return
     */
    public int JumpFloorII(int target) {
        // 1. 声明阶数数组
        int jft[] = new int[target + 1]; //第i项表示，青蛙跳到当前台阶有多少中跳法
        
        // 2. 特殊情况处理
        if (target < 0){
            return 0;
        }else if (target == 0){
            return 1;
        }else if (target == 1){
            return 1;
        }else if (target == 2){
            return 2;
        }
        
        // 3. 计算阶数
        
        // 3.1 前几个阶数
        jft[0] = 1;
        jft[1] = 1;
        jft[2] = 2; 
        // 3.2 后面的阶数
        for(int i = 3; i <= target; ++i){
            // 阶数的计算类似斐波拉契数列
            for(int j = 0; j < i; ++j){
                jft[i] += jft[j];
            }
        }
        
        return jft[target];
    }
    
}
```

# 别人的解法

## 思路
每个台阶都有跳与不跳两种情况（除了最后一个台阶），最后一个台阶必须跳。所以共用2^(n-1)种情况。

## 解法

```
return  1<<--number;
```

向大佬低头，在下服了。。。

# 参考资料
1. [变态跳台阶](https://www.nowcoder.com/profile/286927/codeBookDetail?submissionId=1522855)


# 广告时间
我的个人微信公众号，喜欢的小伙伴可以添加一下，不定期分享有趣的文章
![这里写图片描述](http://img.blog.csdn.net/20170505223017483?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXE0NzA4Njk4NTI=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
