[toc]



# 散列表&Hash table

---

>散列表核心概念是key 和 value，每个key映射一个value，基本的原理是通过hash function/function 来计算key的哈希值，然后用哈希值作为索引将对应值插入内存

## 性能

| 查找   | 插入   | 删除   |          |
| ------ | ------ | ------ | -------- |
| O（1） | O（1） | O（1） | 平均情况 |
| O(n)   | O(n)   | O(n)   | 最坏情况 |

​	

# 题目

---

## 1.两数之和

### 题

> 给定一个整数数组 `nums` 和一个整数目标值 `target`，请你在该数组中找出 **和为目标值** *`target`* 的那 **两个** 整数，并返回它们的数组下标。
>
> 你可以假设每种输入只会对应一个答案。但是，数组中同一个元素在答案里不能重复出现。
>
> 你可以按任意顺序返回答案。
>
>  
>
> **示例 1：**
>
> ```
> 输入：nums = [2,7,11,15], target = 9
> 输出：[0,1]
> 解释：因为 nums[0] + nums[1] == 9 ，返回 [0, 1] 。
> ```
>
> **示例 2：**
>
> ```
> 输入：nums = [3,2,4], target = 6
> 输出：[1,2]
> ```
>
> **示例 3：**
>
> ```
> 输入：nums = [3,3], target = 6
> 输出：[0,1]
> ```

### 分析

`用将nums 用 enumerate拆解，将索引和item分别拆开遍历，再建一个hashtable， 直接判断target-x 是否存在在hashtable 里，然后直接返回就可以了。`

### 代码

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        hashtable=dict()
        for i,num in enumerate(nums):
            if target-num in hashtable:
                return [hashtable[target-num],i]
            hashtable[nums[i]]=i
        return []
```

## 2.环形连表

### 题

> ​	给你一个链表的头节点 `head` ，判断链表中是否有环。
>
> 如果链表中有某个节点，可以通过连续跟踪 `next` 指针再次到达，则链表中存在环。 为了表示给定链表中的环，评测系统内部使用整数 `pos` 来表示链表尾连接到链表中的位置（索引从 0 开始）。**注意：`pos` 不作为参数进行传递** 。仅仅是为了标识链表的实际情况。
>
> *如果链表中存在环* ，则返回 `true` 。 否则，返回 `false` 。
>
>  
>
> **示例 1：**
>
> ![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/07/circularlinkedlist.png)
>
> ```
> 输入：head = [3,2,0,-4], pos = 1
> 输出：true
> 解释：链表中有一个环，其尾部连接到第二个节点。
> ```
>
> **示例 2：**
>
> ![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/07/circularlinkedlist_test2.png)
>
> ```
> 输入：head = [1,2], pos = 0
> 输出：true
> 解释：链表中有一个环，其尾部连接到第一个节点。
> ```
>
> **示例 3：**
>
> ![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/07/circularlinkedlist_test3.png)
>
> ```
> 输入：head = [1], pos = -1
> 输出：false
> 解释：链表中没有环。
> ```

### 分析

`用循环遍历所有head 并用hashtable 存下来，每次遍历后查看是否有重复的head出现，如果有说明cycle，没有说明没有cycle`

### 代码

```python
class Solution:
    def hasCycle(self, head: Optional[ListNode]) -> bool:
        past={}
        while head:
            if head in past:
                return True
            past[head]=1
            head=head.next
        return False
```

## 3.邮箱地址

### 题

> 每个 **有效电子邮件地址** 都由一个 **本地名** 和一个 **域名** 组成，以 `'@'` 符号分隔。除小写字母之外，电子邮件地址还可以含有一个或多个 `'.'` 或 `'+'` 。
>
> - 例如，在 `alice@leetcode.com`中， `alice` 是 **本地名** ，而 `leetcode.com` 是 **域名** 。
>
> 如果在电子邮件地址的 **本地名** 部分中的某些字符之间添加句点（`'.'`），则发往那里的邮件将会转发到本地名中没有点的同一地址。请注意，此规则 **不适用于域名** 。
>
> - 例如，`"alice.z@leetcode.com”` 和 `“alicez@leetcode.com”` 会转发到同一电子邮件地址。
>
> 如果在 **本地名** 中添加加号（`'+'`），则会忽略第一个加号后面的所有内容。这允许过滤某些电子邮件。同样，此规则 **不适用于域名** 。
>
> - 例如 `m.y+name@email.com` 将转发到 `my@email.com`。
>
> 可以同时使用这两个规则。
>
> 给你一个字符串数组 `emails`，我们会向每个 `emails[i]` 发送一封电子邮件。返回实际收到邮件的不同地址数目。
>
>  
>
> **示例 1：**
>
> ```
> 输入：emails = ["test.email+alex@leetcode.com","test.e.mail+bob.cathy@leetcode.com","testemail+david@lee.tcode.com"]
> 输出：2
> 解释：实际收到邮件的是 "testemail@leetcode.com" 和 "testemail@lee.tcode.com"。
> ```
>
> **示例 2：**
>
> ```
> 输入：emails = ["a@leetcode.com","b@leetcode.com","c@leetcode.com"]
> 输出：3
> ```

筛出@前后两个部分，再取出 `.`和`+`的对应内容，拼起来add到hashtable里，返回hashtable的个数就可以了。



### 代码

```python
class Solution:
    def numUniqueEmails(self, emails: List[str]) -> int:
        emailSet = set()
        for email in emails:
            i = email.index('@')
            local = email[:i].split('+',1)[0]
            local=local.replace('.','')
            emailSet.add(local+email[i:])
        return len(emailSet)
```

