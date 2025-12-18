# cheatsheet

作为一个纯废物，我竟也能在这分享考试时要带的cheetsheet吗？

```python
列表推导式： （ [x] * n for _ in range(n)）
字典推导式：  {key:value for key,value in zip(keys,values)}
集合推导式：{x for x in iterable}
切片：list[-1]:最后一个元素
      list[::-1]:反转
      list[1:5:2]:步长为2
      list[:m]:索引为m前的元素
      list[m:]:索引从m开始到结束的元素
排序：x.sort() #从小到大排序
     x.sort(reverse=True) #从大到小排序
     y=sorted(x) #y是x按从小到大排序得来的
     y=sorted(x,reverse=True) #与上相反
     y=sorted(x,key= ) #按  进行排序
          y=sorted(x,key=abs) #按绝对值
          y=sorted(x,key=len) #按长度
          y=sorted(x,key=lambda x:x[i]) #按元组的第i+1个元素排序
          y=sorted(x,key=lambda x:x['key']) #按字典值排序
    
```
