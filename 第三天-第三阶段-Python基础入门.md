# 第三阶段 · Python 基础入门

> 日期：2026-07-19  
> 目标：财务人学 Python 的「最小必要栈」——能看懂、能改、能向 AI 提需求

---

## 📋 财务人学 Python 的正确定位

**不需要当程序员，但要做到：**

| 层次 | 说明 | 目标 |
|------|------|------|
| L1 能用 AI 写代码 | 「帮我用 Python 读 Excel 算合计」→ AI 给代码 → 跑通 | ✅ |
| L2 能看懂代码 | AI 给的代码能读懂每行在干啥 | ✅ |
| L3 能改小地方 | 字段名变了、路径变了能自己改 | ✅ |
| L4 能从头写 | 从零开始写完整脚本 | ❌ 不需要 |
| L5 架构设计 | 选框架、性能优化 | ❌ 完全不需要 |

**类比：就像学 Excel，会 =SUM()、透视表、VLOOKUP 就够用了，不需要会 VBA。**

---

## ✅ 今日掌握的 7 个知识点

### 1. 变量 = 贴标签的盒子

```python
company_name = "易联花西安科技有限公司"   # 文字（字符串），用引号
cash = 1250000                           # 数字（整数），不用引号
```

- `=` 不是"等于"，是"装进去" → 箭头的感觉
- 变量名可以中文、英文、拼音，Python 不关心叫什么

### 2. f-string 格式化输出

```python
print(f"现金余额：{cash:,}元")    # 输出：现金余额：1,250,000元
```

- `f"..."` = 模板字符串
- `{}` = 挖坑填变量
- `:,` = 千分位逗号

### 3. 列表 = 一串数据的大盒子

```python
companies = ["西安", "北京", "泰安", "青岛"]
print(companies[0])    # 第1个：西安（下标从0开始！）
print(len(companies))  # 个数：4
```

- `[]` 方括号包起来
- 下标从 `0` 开始，口诀：想拿第 N 个就写 `[N-1]`

### 4. for 循环 = 挨个处理

```python
for name in companies:
    print(name)          # 直接拿内容

for i in range(len(companies)):
    print(companies[i])  # 用下标拿
```

- `range(4)` = 生成 0, 1, 2, 3
- `range(len(列表))` = 生成所有有效下标
- 缩进的才属于循环体

### 5. if 判断 = 条件筛选

```python
if cash > 1000000:
    print("大额")
```

- `if` 后面**必须加冒号**
- 缩进的代码是"条件成立时才执行"的

### 6. 字典 = 编码查名称（像 VLOOKUP）

```python
科目表 = {"1001": "库存现金", "1002": "银行存款"}
print(科目表["1002"])           # 输出：银行存款
科目表["2202"] = "应付账款"     # 追加

for 编码, 名称 in 科目表.items():
    print(f"{编码} → {名称}")
```

- `{}` 花括号
- `"键": "值"` 每对用冒号，对之间用逗号
- `.items()` = 同时拿键和值

### 7. sum() 求和

```python
total = sum(cash_list)   # 对整个列表求和
```

---

## ⚠️ 今天踩过的 3 个坑

| 错误 | 正解 |
|------|------|
| `sum(cash_list[i])` — 给单个数字求和 | `sum(cash_list)` — 给整个列表求和 |
| `if cash > startswith(...)` — 数字没有 startswith | `if cash > 1000000` — 直接比大小 |
| `if(编码.startswith("1"))` — 多余的花括号 | `if 编码.startswith("1"):` — 注意冒号 |

---

## 🎯 综合题：子公司现金盘点表（从零写出，全对）

```python
company_names = ["西安", "北京", "泰安", "青岛"]
cash_list = [1250000, 890000, 456000, 2380000]

for i in range(len(company_names)):
    print(f"{company_names[i]} ： {cash_list[i]:,}元")

total = sum(cash_list)
print(f"现金合计：{total:,}元")

for i in range(len(company_names)):
    if cash_list[i] > 1000000:
        print(f"{company_names[i]} ： {cash_list[i]:,}元 【大额】")
```

---

## 🔜 待学

- 函数（打包重复代码）
- openpyxl 读写 Excel
- pandas 再过一遍

---

*笔记整理：老财 🤝 幸幸*
