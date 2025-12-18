# cheatsheet

作为一个纯废物，我竟也能在这分享考试时要带的cheatsheet吗？

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
删除元素：
      a.remove(i) #删除元素i
      b=a.pop() #删除最后一个元素
      b=a.pop(i) #删除索引i
      a[i:j]=[] #删除索引从i到j-1
      del a[i] #删除索引i
常用算法模板：
      二分查找：
            def binary_search(arr, target):
                """
                二分查找（迭代版本）
    
                参数:
                    arr: 有序列表（升序）
                    target: 要查找的目标值
    
                返回:
                    如果找到，返回目标值的索引
                    如果未找到，返回 -1
                """
                left, right = 0, len(arr) - 1
    
                while left <= right:
                    mid = left + (right - left) // 2  # 防止整数溢出
        
                    if arr[mid] == target:
                        return mid
                    elif arr[mid] < target:
                        left = mid + 1  # 目标在右半部分
                    else:
                        right = mid - 1  # 目标在左半部分
    
                return -1  # 未找到


      回溯算法：
            # 排列/组合/子集问题通用模板
            def backtrack_template(nums):
                result = []
                n = len(nums)
    
                def backtrack(start, path):
                    result.append(path.copy())  # 记录所有子集
        
                    for i in range(start, n):
                        # 去重（如果数组有重复元素）
                        if i > start and nums[i] == nums[i-1]:
                            continue
                
                        path.append(nums[i])
                        backtrack(i+1, path)    # i+1表示不重复选择
                        # backtrack(i, path)     # i表示可重复选择
                        path.pop()
    
                # 如果需要排序
                nums.sort()
                backtrack(0, [])
                return result


      
```
