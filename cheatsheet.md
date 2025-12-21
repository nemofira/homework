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
# 常用操作
x & 1        # 判断奇偶
x & (x-1)    # 去掉最后一个1（判断2的幂）
x & -x       # 得到最后一个1的位置
1 << n       # 2^n
x ^ x = 0    # 相同数异或为0
x ^ 0 = x    # 任何数异或0为自己

# 统计二进制中1的个数
def count_ones(n):
    count = 0
    while n:
        n &= n-1
        count += 1
    return count
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

      动态规划：
       # 1D DP（斐波那契）
            def fib(n):
                if n <= 1: return n
                dp = [0] * (n+1)
                dp[1] = 1
                for i in range(2, n+1):
                    dp[i] = dp[i-1] + dp[i-2]
                return dp[n]

            # 空间优化版
            def fib_optimized(n):
                if n <= 1: return n
                prev2, prev1 = 0, 1
                for i in range(2, n+1):
                    curr = prev1 + prev2
                    prev2, prev1 = prev1, curr
                return curr

            # 0-1背包（最大价值）
            def knapsack_01(weights, values, capacity):
                n = len(weights)
                dp = [0] * (capacity+1)
    
                for i in range(n):
                    for w in range(capacity, weights[i]-1, -1):  # 逆序！
                        dp[w] = max(dp[w], dp[w-weights[i]] + values[i])
                return dp[capacity]

            # 完全背包（物品无限）
            def knapsack_unbounded(weights, values, capacity):
                dp = [0] * (capacity+1)
    
                for w in range(1, capacity+1):
                    for i in range(len(weights)):
                        if weights[i] <= w:
                            dp[w] = max(dp[w], dp[w-weights[i]] + values[i])
                return dp[capacity]

            # 最长公共子序列
             def longest_common_subsequence(text1, text2):
                m, n = len(text1), len(text2)
                dp = [[0]*(n+1) for _ in range(m+1)]
    
                for i in range(1, m+1):
                    for j in range(1, n+1):
                        if text1[i-1] == text2[j-1]:
                            dp[i][j] = dp[i-1][j-1] + 1
                        else:
                            dp[i][j] = max(dp[i-1][j], dp[i][j-1])
    
                # 重构LCS
                i, j = m, n
                lcs = []
                while i > 0 and j > 0:
                    if text1[i-1] == text2[j-1]:
                        lcs.append(text1[i-1])
                        i -= 1; j -= 1
                    elif dp[i-1][j] > dp[i][j-1]:
                        i -= 1
                    else:
                        j -= 1
                return dp[m][n], ''.join(reversed(lcs))

      # dijkstra算法
            import heapq

            def dijkstra(graph, start):
                # graph: {node: [(neighbor, weight), ...]}
                distances = {node: float('inf') for node in graph}
                distances[start] = 0
                pq = [(0, start)]  # (距离, 节点)
    
                while pq:
                    curr_dist, curr_node = heapq.heappop(pq)
                    if curr_dist > distances[curr_node]:
                        continue
        
                    for neighbor, weight in graph[curr_node]:
                        distance = curr_dist + weight
                        if distance < distances[neighbor]:
                            distances[neighbor] = distance
                            heapq.heappush(pq, (distance, neighbor))
                return distances
      
```
