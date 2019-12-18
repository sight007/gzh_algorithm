## 38、字符串的排列

#### 题目：

输入一个字符串，打印出该字符串中字符的所有排列。



#### 解题（递归）：

- 把字符串分为两部分，第一部分为第i字节，第二部分为剩余的字符
- 把字符串的第i字母与其他字节一次交换，形成`str.length`种字符串。
- 把上面每一种字符串的第二部分也按照之前的操作。



为什么要采用递归？因为是求解同样子问题，先固定一个字节，算剩余字符的组合。剩余字符的组合怎么算？剩余字符再固定一个字符，求剩下的组合。。。直到index到最后一个位置了。



```java
	ArrayList<String> res = new ArrayList<String>();
    
    public ArrayList<String> Permutation(String str) {
       
        if(str == null || str.length()==0) return null;
       
        Permutation(str.toCharArray(), 0, res);
       
        return res;
    }
    
    //递归
    public void Permutation(char[] strs, int index, ArrayList<String> res) {
        if(index==strs.length-1 && !res.contains(String.valueOf(strs))){
            res.add(String.valueOf(strs));
        }else{
            for(int i=index; i<strs.length; i++){
                
                //第一部分（交换）
                char temp = strs[i];
                strs[i] = strs[index];
                strs[index] = temp;
                
                Permutation(strs, index+1, res);
                
                //还原上面的交换，为了下一次循环继续用原数据
                strs[index] = strs[i];
                strs[i] = temp;
            }
        }
    }
```

