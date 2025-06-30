# 结构体排序
题目链接：[牛客 BGN22 小苯送礼物](https://www.nowcoder.com/practice/466e02d2177845589ab5fa5decc2857f?tpId=385&tags=&title=&difficulty=0&judgeStatus=0&rp=0&sourceUrl=%2Fexam%2Foj%3Fpage%3D1%26tab%3D%25E7%25AE%2597%25E6%25B3%2595%25E7%25AF%2587%26topicId%3D385)
## 第一版，超时了
```python

from functools import cmp_to_key

class struct:
    def __init__(self,id,dianzan,shoucang):
        self.id = id
        self.dianzan = dianzan
        self.shoucang = shoucang
        self.support = dianzan + shoucang * 2

def cmp(a,b):
    if a.support!=b.support:
        return a.support - b.support
    elif a.shoucang!=b.shoucang:
        return a.shoucang - b.shoucang
    else:
        return a.id - b.id

key_func = cmp_to_key(cmp)

struct_list = []
n,k = map(int,input().split())
for i in range(n):
    dianzan,shoucang = map(int,input().split())
    struct_list.append(struct(i+1,dianzan,shoucang))

struct_list.sort(key=key_func,reverse=True)

# for item in struct_list:
#     print(item.id,item.dianzan,item.shoucang,item.support)

res = []
for i in range(k):
    res.append(struct_list[i].id)

res.sort()
for i in res:
    print(i,end=" ")
```
## 第二版：优化了（更推荐使用）
```python

class Struct:
    def __init__(self, id, dianzan, shoucang):
        self.id = id
        self.dianzan = dianzan
        self.shoucang = shoucang
        self.support = dianzan + shoucang * 2

struct_list = []
n, k = map(int, input().split())
for i in range(n):
    dianzan, shoucang = map(int, input().split())
    struct_list.append(Struct(i + 1, dianzan, shoucang))

# 使用元组排序，先按 support 降序，再按 shoucang 降序，最后按 id 升序

# 重要！！！重要！！！！
struct_list.sort(key=lambda x: (-x.support, -x.shoucang, x.id))

# 提取前 k 个元素的 id
res = [item.id for item in struct_list[:k]]

# 对结果进行排序并打印
res.sort()
print(" ".join(map(str, res)))
```

# 字典排序？
```python
word_list = input().split(" ")
word_count = {}
for word in word_list:
    if word not in word_count:
        word_count[word] = 1
    else:
        word_count[word] += 1

# 把字典转为列表才可以排序
# 按值降序排序，值相同的情况下按键的逆序排序
sorted_word_count = sorted(word_count.items(), key=lambda x: (-x[1], x[0]), reverse=False)

# 打印排序后的结果
for key,value in sorted_word_count:
    if value>=3:
        print(key)
    else:
        break
```
---
开发中......