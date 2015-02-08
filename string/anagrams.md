**时间**:2015.2.8

**问题描述**:从输入的字符串数组中找到所有成组的anagram单词(anagram,字谜,形如"cinema"和"iceman",单词中所有字母和数量都相同,只是排列顺序不同)

example. input:{"dog", "god", "cinema", "iceman", "eat"} output:["dog", "god", "cinema", "iceman"]

**code**:
```java  
public class Anagrams {
    public static List<String> anagrams(String[] strs){
        List<String> result = new LinkedList<String>();
        Map<String,List> table = new HashMap<String, List>();
        for(String s : strs){
            char[] array = s.toCharArray();
            Arrays.sort(array);
            List list = table.get(new String(array));
            if(list == null){
                list = new LinkedList();
                list.add(s);
                table.put(new String(array), list);
            }else{
                list.add(s);
            }
        }
        for(String key : table.keySet()){
            List list = table.get(key);
            if(list.size() != 1){
                result.addAll(list);
            }
        }
        return result;
    }

    public static void main(String[] args){
        System.out.println(anagrams(new String[]{"",""}));
    }
}

```
**思路**:
1. 判断是否两个字符串是否满足要求,在于所有组成的字母和出现次数都相同.实现时先将字符数字按字母序排序,由有序数组构造的**新字符串**可以判断是否满足要求.(如"cinema"和"iceman"排序后都是"aceimn".)
2. 然后将排序后的字符串作为hashtable的key,list作为value,用于保存所有和key成对的字符串
