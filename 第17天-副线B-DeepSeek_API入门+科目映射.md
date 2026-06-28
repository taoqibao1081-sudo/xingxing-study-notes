# 第17天：副线B · DeepSeek API 入门 + 科目映射实战

> 日期：2026-06-28
> 状态：完成

---

## 一、Hello World

### API调用五零件

| 零件 | 代码 | 财务类比 |
|------|------|---------|
| API Key | `DEEPSEEK_API_KEY` | 银行U盾 |
| 地址 | `base_url="https://api.deepseek.com"` | 网点地址 |
| 模型 | `model="deepseek-chat"` | VIP还是普通窗口 |
| 消息 | `messages=[{"role":"user","content":"..."}]` | 你要办什么业务 |
| 响应 | `response.choices[0].message.content` | 柜员回单 |

### 角色（role）说明

| role | 作用 | 举例 |
|------|------|------|
| `system` | 设定AI的角色和输出规则 | "你是会计准则专家，只回复科目名" |
| `user` | 你问的问题 | "将短期投资映射为企业准则科目" |
| `assistant` | AI的回复（多轮对话时传入历史） | 上一条AI回复 |

---

## 二、科目映射实战

### 流程
```
Excel(34个科目) → pandas读取 → for循环 → DeepSeek API → 写回Excel
```

### 关键代码
```python
client = OpenAI(api_key=DEEPSEEK_API_KEY, base_url=DEEPSEEK_BASE_URL)

response = client.chat.completions.create(
    model="deepseek-chat",
    messages=[
        {"role": "system", "content": "只返回映射后的科目名称，不要解释"},
        {"role": "user", "content": f"将「{name}」映射为企业准则科目"},
    ],
)
result = response.choices[0].message.content.strip()
```

### 核心映射结果（小企业→企业）

| 小企业科目 | 企业科目 | 变化 |
|-----------|---------|:--:|
| 短期投资 | 交易性金融资产 | 改名 |
| 长期债券投资 | 债权投资 | 改名 |
| 应付利润 | 应付股利 | 改名 |
| 主营业务收入 | 营业收入 | 简化 |
| 主营业务成本 | 营业成本 | 简化 |
| 主营业务税金及附加 | 税金及附加 | 简化 |
| 应收票据 | 应收票据 | 同名 |
| 固定资产原价 | 固定资产 | 微调 |
| ... | ... | ... |

### 验证
- 34个科目 / 34个映射完成 / 0个错误

---

## 三、排坑日志

| 坑 | 原因 | 解决 |
|----|------|------|
| VSCode用系统Python找不到openai | 库装在虚拟环境 | 用.bat指定解释器路径 |
| 写字符串进float64列报错 | pandas空列默认数字类型 | `dtype={'列名': str}` |
| 路径反斜杠转义 | `\U`被当Unicode | 加`r`前缀 |

---

## 四、文件清单

```
DeepSeek API/
├── deepseek_config.py      # API Key配置
├── hello_deepseek.py        # Hello World
├── 科目映射待办.xlsx         # 练习数据
├── 科目映射_AI.py            # 测试版（前5个）
├── 科目映射_全量.py          # 全量版（34个）
├── 科目映射结果_测试.xlsx     # 测试输出
├── 科目映射结果_全量.xlsx     # 全量输出
├── 运行映射.bat              # 测试版快捷启动
└── 运行全量映射.bat          # 全量版快捷启动
```

---

## 五、下一步

模块5：合并抵消（PQ实战）
