# 第16天：副线A · pandas 收官复习

> 日期：2026-06-28
> 状态：完成

---

## 一、知识地图回顾

12个核心函数，分为四阶段流水线：

| 阶段 | 函数 | 财务场景 |
|------|------|---------|
| 读取与探查 | `read_excel` `shape` `head` | 打开文件看一眼 |
| 清洗与选列 | `iloc` 条件筛选 `to_numeric` | 切行列、去干扰、转数字 |
| 合并与汇总 | `concat` `groupby` `for` `if` | 多表摞一起、分类汇总 |
| 变形与输出 | `melt` `pivot_table` `to_excel` | 换个角度看、存出去 |

**三步法：读进来 → 洗干净 → 算出来 → 存出去**

---

## 二、综合实战：3家管理费用合并

### 场景
3家公司提交管理费用明细，格式各不相同：
- 新星餐饮：双栏格式（6列，左右各3项）
- 创亿科技：扁平格式，前2行表头说明
- 恒通物流：扁平格式，前3行干扰+尾部制表人

### 最终成果
- 科目汇总表（7个科目，合计820,000）
- 科目×公司透视表（交叉对比三家费用构成）

### 验证
- 透视表三家和 = 汇总表合计 = 820,000（平账通过）

---

## 三、关键升级：从手工到自动

### 自动判断双栏 vs 扁平
```python
if df.shape[1] >= 5:
    # 列数>=5 → 双栏 → 左右切分拼接
else:
    # 列数<=3 → 扁平 → 直接取
```

### 自动找数据起点
```python
# 找第一列是数字的行（行次1,2,3...）
first_col = df.iloc[:, 0].astype(str)
is_number = first_col.str.match(r'^\d+$')
first_data_row = is_number[is_number].index[0]
header_row = first_data_row - 1  # 列名行在数字行上面
```

### 统一清洗流程
```python
df = df[~df['科目'].astype(str).str.contains('合计|总计')]  # 去合计
df['金额'] = pd.to_numeric(df['金额'], errors='coerce')     # 文本→数字
df = df.dropna(subset=['金额'])                              # 去空行
```

---

## 四、排坑日志

| 坑 | 原因 | 解决 |
|----|------|------|
| 路径反斜杠被转义 | `\U` 被当成Unicode编码 | 前面加 `r` 或改用 `/` |
| iloc切3列给2个列名 | 双栏有行次列 | `iloc[:, 1:3]` 跳过行次 |
| 找不到"科目"行 | 数据里没"科目"两字，只有费用名 | 改用 `第一列是数字` 定位 |
| 公司名加错位置 | 放在循环外 | 在 `append` 之前加 |
| pivot_table引用了未定义变量 | 放在concat之前 | 先合并再透视 |

---

## 五、副线A结业

### 掌握的函数（12个）

| # | 函数 | 掌握度 |
|:--:|------|:--:|
| 1 | `pd.read_excel()` | OK |
| 2 | `df.shape` / `df.head()` | OK |
| 3 | `df.iloc[:, [列号]]` | OK |
| 4 | 条件筛选 `str.contains()` | OK |
| 5 | `pd.concat([表1,表2])` | OK |
| 6 | `df.groupby('科目').sum()` | OK |
| 7 | `pd.to_numeric(errors='coerce')` | OK |
| 8 | `df.to_excel()` | OK |
| 9 | `for filename in os.listdir(folder)` | OK |
| 10 | `if/else` 判断 | OK |
| 11 | `df.pivot_table()` | OK |
| 12 | `df.melt()` | OK |

### 三层境界达成
- 调用层（找模板改参数）：OK
- 理解层（看懂逻辑能排错）：OK
- 编写层（独立写代码）：起步中

### 能独立完成的事
- 读入多个Excel → 自动判断格式 → 清洗 → 合并 → 汇总 → 透视 → 输出

---

## 六、下一步

副线B：DeepSeek API 辅助科目映射
