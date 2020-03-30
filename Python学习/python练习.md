# 函数练习

1. 列出1～100之间的素数，并计算一共有多少个。

```python
number = 0
for n in range(1, 101):
    for j in (2, n + 1):
        if n%j == 0:
            break
    else:
        number += 1
        print(n, end = " ")

print( "\n1~100之间的素数是%d个"%number)
```

> ```html
> 1 3 5 7 9 11 13 15 17 19 21 23 25 27 29 31 33 35 37 39 41 43 45 47 49 51 53 55 57 59 61 63 65 67 69 71 73 75 77 79 81 83 85 87 89 91 93 95 97 99 
> 1~100之间的素数是50个
> ```

2. 如何用Python3实现斐波那契数列前10项数列？

```python
Fibonacci = [1, 1]
for i in range(3, 11):
    j = Fibonacci[-1] + Fibonacci[-2]
    Fibonacci.append(j)
print(Fibonacci)
```

> [1, 1, 2, 3, 5, 8, 13, 21, 34, 55]

3. “企业根据利润提成发奖金”的问题。当利润(I)低于或等于10万元时，奖金可提10%；当利润高于10万元，低于20万元时，低于10万元的部分按10%提成，高于10万元的部分，可提成7.5%；当20万到40万之间时，高于20万元的部分，可提成5%；当40万到60万之间时高于40万元的部分，可提成3%；当60万到100万之间时，高于60万元的部分，可提成1.5%；当高于100万元时，超过100万元的部分按1%提成。问题是求应发放奖金总数是多少？结果保留两位小数，并作四舍五入处理。

```python
performance = int(input("输入利润=  万元"))
if performance <= 10 and performance > 0:
    bonus = performance * 0.1
elif performance > 10 and performance <= 20:
    bonus = 10 * 0.1 + (performance - 10) * 0.075
elif performance > 20 and performance <= 40:
    bonus = 10 * 0.1 + 10 * 0.075 + (performance - 10) * 0.05
elif performance > 40 and performance <= 60:
    bonus = 10 * 0.1 + 10 * 0.075 + 20 * 0.05 + (performance - 40) * 0.03
elif performance > 60 and  performance <= 100:
    bonus = 10 * 0.1 + 10 * 0.075 + 20 * 0.05 + 20 * 0.03 + (performance -60) * 0.015
elif performance > 100:
    bonus = 10 * 0.1 + 10 * 0.075 + 20 * 0.05 + 20 * 0.03 + 40 * 0.015 + (performance - 100) * 0.01
else:
    print("输入错误，请重新输入！")
total_bonus = round(bonus, 2)
print("应发奖金为%d万元"%total_bonus)
```

