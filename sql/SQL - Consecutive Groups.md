#GapsAndIslands #ConsecutiveGroups
#SQL #Leetcode/Hard 

Simple groups
### 180. Consecutive Numbers

https://leetcode.com/problems/consecutive-numbers/description/

  

```sql

SELECT

distinct l1.num as "ConsecutiveNums"

  

FROM

Logs l1,

Logs l2,

logs l3

  

WHERE

l1.id = l2.id-1

and

l2.id = l3.id-1

and

(l1.num = l2.num) and (l2.num = l3.num)

  

ORDER BY

  

l1.Id, l2.Id, l3.Id

```

- alternate solution using window functions LAG and LEAD
- personally I find this more readable

```sql

WITH lagged AS (

  

SELECT

lag(num) OVER(ORDER BY id) as last_num,

num,

lead(num) OVER(ORDER BY id) as next_num

FROM Logs

  

)

  

SELECT DISTINCT num as ConsecutiveNums

FROM lagged

WHERE last_num = num AND next_num = num

```
