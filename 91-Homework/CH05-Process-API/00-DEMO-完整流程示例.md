# DEMO · 完整流程示例（seed 10）

> 这是一份**已完成的示范**，用来展示三个步骤各自该写什么。
> 轮到你自己做时，请照着 [Q1](Q1-随机进程树.md) 里的空白表格写。

## 题目

```sh
cd ~/ostep-homework/cpu-api
./fork.py -s 10        # 只看动作，不看答案
```

得到的动作序列：

```text
初始: a

1. a forks b
2. a forks c
3. c EXITS
4. a forks d
5. a forks e
```

---

## Step 1 · Prediction

（这一步本该自己手写。下面是先写下的预测）

| # | 动作 | 我预测的树 |
|---|---|---|
| 1 | `a forks b` | `a → b` |
| 2 | `a forks c` | `a → (b, c)` |
| 3 | `c EXITS` | `a → b` |
| 4 | `a forks d` | `a → (b, d)` |
| 5 | `a forks e` | `a → (b, d, e)` |

---

## Step 2 · Result

```sh
./fork.py -s 10 -c
```

```text
Action: a forks b               a
                                └── b

Action: a forks c               a
                                ├── b
                                └── c

Action: c EXITS                 a
                                └── b

Action: a forks d               a
                                ├── b
                                └── d

Action: a forks e               a
                                ├── b
                                ├── d
                                └── e
```

**预测与结果完全一致 ✅**

---

## Step 3 · Explanation

### 为什么 `c EXITS` 之后树从 `(b, c)` 变回 `b`？

因为 `c` 是**叶子进程**，没有子进程需要安顿。退出时只需把它从父进程 `a` 的孩子列表里摘掉，树的其余部分完全不受影响。

### 为什么最后是 `b, d, e`，而不是 `b, c, e`？

打印顺序反映的是**创建顺序**：

| 进程 | 创建次序 | 结局 |
|---|---|---|
| `b` | 第 1 个创建 | 存活 |
| `c` | 第 2 个创建 | 第 3 步退出 |
| `d` | 第 3 个创建（第 4 步） | 存活 |
| `e` | 第 4 个创建（第 5 步） | 存活 |

`c` 退出后在兄弟列表里"腾出的位置"**不会被复用** —— `d` 排在 `b` 后面，只是因为它是在 `c` 退出之后才被创建的。

> ⚠️ 容易掉进去的坑：**不要按字母序去推树的排列**，只跟创建先后有关。

### 延伸：如果退出的是 `b` 呢？

`b` 有子进程时退出，行为取决于选项（详见 [README](README.md#已实测的行为易错点)）：

- 默认：子进程被提升到**根**下
- `-R`：子进程挂到**就近**的父进程下
- `-L`：直接**禁止**退出，报 `failed: has children`
