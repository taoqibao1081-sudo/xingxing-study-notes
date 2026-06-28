# 第14-15天：副线A · Python pandas 报表合并（超级学习日）

> 日期：2026-06-27（Day14上篇）+ 2026-06-28（Day15下篇）
> 状态：✅ 完成（12个核心函数 + 单公司/3家/4家三种难度 + 宽表透视 + 财务体检）

---

## 一、掌握的函数清单

| # | 函数/技能 | 财务类比 | 掌握度 |
|:--:|------|---------|:--:|
| 1 | `pd.read_excel()` | 双击打开Excel | ✅ |
| 2 | `df.shape` / `df.head()` | Excel右下角行列数 / 滚动预览 | ✅ |
| 3 | `df.iloc[:, [列号]]` | 按住Ctrl选列 | ✅ |
| 4 | 条件筛选 `str.isdigit() | contains('合计')` | Excel筛选+去空行 | ✅ |
| 5 | `pd.concat([表1,表2])` | 追加查询 | ✅ |
| 6 | `df.groupby('科目').sum()` | 分类汇总 | ✅ |
| 7 | `pd.to_numeric(errors='coerce')` | 文本→数字 | ✅ |
| 8 | `df.to_excel()` | 另存为Excel | ✅ |
| 9 | `for filename in os.listdir(folder)` | 批量处理文件夹 | ✅ |
| 10 | `if/else` 判断 | 条件分支 | ✅ |
| 11 | `df.pivot_table()` | 数据透视表 | ✅ |
| 12 | `df.melt()` | 逆透视 | ✅ |

## 二、学习里程碑

```
阶段1：单公司清洗 → day14_1.py（新星餐饮，平账805万）
阶段2：3家循环   → day14_2.py（for循环，平账1331万）
阶段3：4家混合   → day14_3.py（双栏+扁平，平账3582万）
阶段4：财务体检  → lianxi_2.py（流动比率+资产负债率分析）
```

## 三、排坑经验

1. **合计行无行次号**：不能用dropna(subset=['行次'])，要用科目含"合计|总计"判断
2. **字符串不能求和**：`pd.to_numeric(errors='coerce')` 转换
3. **变量用混**：`df`是原始表，`combined`是清洗后的表，分析要用后者
4. **缩进问题**：`health_check.append()`必须在for循环内
5. **NameError**：变量未定义 → 在前面加 `xxx = []`
6. **UnicodeError**：emoji在gbk终端无法显示 → 用文本替代或设utf-8

## 四、Python/pandas 本质理解

- **Python** = 厨房（操作系统级别的语言）
- **pandas** = 菜刀（专门处理表格的工具包）
- **import** = 从工具箱里拿出菜刀
- **变量** = 给数据贴标签（df=原始表，combined=洗过的表）
- **缩进** = Python的"大括号"，决定代码属于哪个块

## 五、下一步

pandas收官复习（自定时间）→ 副线B：DeepSeek API 辅助科目映射
