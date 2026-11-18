# PsychoPy Sentence Rating


## 1. 安装 PsychoPy

[官方安装页](https://psychopy.org/download.html)


## 2. 条件表制作
示例 16 trials 条件表，点击[此处](https://github.com/zqzhao-sudo/Psychopy_SentenceRating_Practice/releases/download/v1.0/psychopy_demo_conditions.csv)下载，请放在你的实验项目根目录（与 `.psyexp` 文件同级）下。

[官方 Flow 与条件表说明](https://devdocs.psychopy.org/builder/flow.html)

**注意，表头一定要涵盖 trial_id、sentence 和 context，不然接下来无法实现前后导航。如若命名并非 trial_id，可以自行替换第4部分预制代码中的 trial_id 部分！！**

## 3. 可以自定义的一些参数

### 3.1 整个实验的设置

| 页签 | 参数 | 设置与用途 |
| --- | --- | --- |
| Basic | Experiment info | 保留 `participant` 和 `session`，便于区分试跑 |
| Screen | Full-screen window / Window size (pixels) | 在run模式里可以调整被试看到的参数 |
| Screen | Color / Color space | 用于调整背景颜色 |
| Data | Data filename | 保留默认命名，通常包含参与者编号和时间。可以根据需要自己改一下。 |
| Data | 保存选项 | 选择需要保留哪些数据|

[官方坐标单位说明](https://psychopy.org/general/units.html)


### 3.2 loop里的参数

| Loop 参数 | 填写 | 作用 |
| --- | --- | --- |
| Name | `demo_16trails` | 沿用示例文件的拼写。注意改名勿忘更新预制代码 |
| Conditions | `psychopy_demo_conditions.csv` | 选择csv文件，会自动识别parameters。 |
| Loop type | `sequential` | 按表格顺序跑，也可以设置随机等。 |
| nReps | `1` | 重复次数，这里是每行一次，如若写16就是每行16次了 |
| Selected rows | 留空 | 选择读几行，留空就是读完整张条件表 |
| Is trials | 勾选 | 每次循环按一次试次处理 |

### 3.3 不同routine的参数

几个组件的 Start 均选择 **time (s)** 并填 `0`，Stop 留空。Routine 自身的结束时间也留空，让参与者自行决定何时给分。字体可先用电脑已安装的中文字体。示例是 `FangSong_GB2312`，也可安装并统一使用 `Noto Sans SC`。

添加字体的话，在finder里按cmd+shift+g，输入`~/.psychopy3`，找到font文件夹并添加

[仿宋字体](https://github.com/zqzhao-sudo/Psychopy_SentenceRating_Practice/releases/download/v1.0/FangSong_GB2312.ttf)


[Noto Sans SC](https://github.com/zqzhao-sudo/Psychopy_SentenceRating_Practice/releases/download/v1.0/Noto_Sans_SC.truetype)


#### 3.3.1 textbox组件
| 组件 | 页签与参数 | 填写 | 作用 |
| --- | --- | --- | --- |
| Textbox `context_textbox` | Basic → Text / 更新频率 | **set every repeat** | 每题根据变量换语境。|
| | Layout → Units / Position / Size | `from exp settings` / `(0, 0.2)` / `(1.1, 0.25)` | 把语境框放在上方，宽度控制一行能放多少字。 |
| | Layout → Anchor / Alignment | `center` / `center-left` | 框以坐标为中心，段落左对齐。|
| | Appearance → Text color | 根据需求填写 | 改变字体颜色 |
| | Data → Read only / Store rating / Store rating time / Store history | 自行按需要选择 | 选择需要保存的数据，如RT或者Rating |

#### 3.3.2 text组件
| 组件 | 页签与参数 | 填写 | 原因 |
| --- | --- | --- | --- |
| Text `sentence_text` | Basic → Text / 更新频率 | **set every repeat** | 每题替换目标句，评分提示放在下一段 |
| | Layout → Units / Position / Wrap width | `from exp settings` / `(0, 0)` / `1.1` | 目标句居中并限制宽度。若材料会占多行，预览时检查与语境和量表的间距 |
| | Appearance → Text color | 根据需求填写 | 改变字体颜色 |
| | Data → Read only / Store rating / Store rating time / Store history | 自行按需要选择 | 选择需要保存的数据，如RT或者Rating |


#### 3.3.3 slider组件
| 组件 | 页签与参数 | 填写 | 原因 |
| --- | --- | --- | --- |
| Slider `sentence_rating` | Basic → Styles / Ticks / Granularity | `scrollbar` / `(1, 2, 3, 4, 5, 6, 7)` / `1` | 数值范围为 1–7，响应吸附到整分 |
| | Basic → Labels / Starting value | `('1分', '', '', '', '', '', '7分')` / 留空 | 为每个分数赋值，此处我们只需要首位 |
| | Basic → Force end of Routine | 勾选/关闭 | 释放鼠标确认评分后，自动进入下一题。在上一题下一题功能时需要关闭。 |
| | Layout → Units / Position / Size | `from exp settings` / `(0, -0.2)` / `(1.0, 0.05)` | 量表位于目标句下方，宽大于高，因此水平显示 |
| | Appearance / Formatting | Label color `根据需求填写`、Marker color `根据需求填写`、Line color `根据需求填写`、Style tweaks 留空，标签字高 `0.05` | 调整slider的颜色，根据需要填写 |
| | Data → Read only / Store rating / Store rating time / Store history | 自行按需要选择 | 选择需要保存的数据，如RT或者Rating |

在 `sentence_text` 的 Text 字段粘贴这一行。开头的 `$` 告诉 Builder 执行表达式，`\n\n` 在目标句和提示之间换行。也可以用俩text框

```text
$sentence + '\n\n请判断上面的句子是否通顺自然。'
```


[官方 Textbox 参数](https://psychopy.org/builder/components/TextboxComponent.html) 

[官方 Text 参数](https://psychopy.org/builder/components/TextComponent.html) 

[官方 Slider 参数](https://psychopy.org/builder/components/SliderComponent.html)

### 3.4 换行组件的参数

在 `sentence_trial` 中找到并添加 **Code** component，代码类型选py，命名 `linebreak_code`，在 **Begin Routine** 粘贴以下代码，其余页签留空。

```python
context_textbox._lineBreaking = 'uax14'
context_textbox._layout()
```
注意：如若context_textbox的命名规则不一致，需要更改才可以生效。

```python
这里是你需要换行的component的名字._lineBreaking = 'uax14'
这里是你需要换行的component的名字._layout()"
```

### 3.5 button组件的参数【可选】
与前文类似，在`button_text`里填写你想呈现的文字，如`上一题`
勾选`Run once per click`
在layout调整位置；在Appearance中修改颜色；在Formatting中修改字体；在Data选择要保存什么数据。

注意1：似乎该组件只能识别Noto Sans SC字体？

注意2: 如若出现换行问题需要在换行组件中添加该组件的换行参数，操作同上。

```python
这里是你需要换行的component的名字._lineBreaking = 'uax14'
这里是你需要换行的component的名字._layout()"
```


## 4.前进与返回键的预制代码

### 4.1 Button的预制代码
首先，取消 `sentence_rating` 的 **Force end of Routine**。

添加两个 **Button** 组件。Start 都是 `0`，Stop 留空，Text 保持 **constant**。按钮的回调只登记点击，实际翻页由下面的 Code 处理。 

| 页签 / 参数 | 上一题 | 下一题 |
| --- | --- | --- |
| Basic → Callback function | `nav['action'] = 'prev'` | `nav['action'] = 'next'` | 


### 4.2 预制代码
**！！一定要保证loop用的condition file和预制代码中的一致！！**

**食用指南：**
新增 Code，命名 `nav_code`，放在评分 Routine 的最底部，在 Slider 和两个 Button 之后。组件从上到下执行，`nav_code` 需要读到本轮的条件、已初始化的组件和本帧登记的点击。把下面三段分别放进同一个 Code 组件对应的页签。

#### Begin Experiment

```python
import csv
import os as nav_os
from pathlib import Path

''' False：方式 1；True：方式 2。 '''
NAV_DYNAMIC_SAVE = False

with open('这里填写你的condition表格名称.csv', ##需要填写的部分
          'r', newline='', encoding='utf-8-sig') as nav_file:
    nav_reader = csv.DictReader(nav_file)
    nav_headers = nav_reader.fieldnames
    nav_rows = list(nav_reader)

if not nav_headers or not nav_rows:
    raise ValueError('条件表没有表头或没有材料。')
if any(not h.strip() for h in nav_headers):
    raise ValueError('条件表存在空列名。')
if len(nav_headers) != len(set(nav_headers)):
    raise ValueError('条件表存在重复列名。')
if not {'trial_id', 'context', 'sentence'}.issubset(nav_headers):
    raise ValueError('条件表必须包含 trial_id、context、sentence。')
if 'sentence_rating' in nav_headers:
    raise ValueError('条件表已有 sentence_rating 列，请先改名。')
if any(None in row or any(v is None for v in row.values())
       for row in nav_rows):
    raise ValueError('条件表某行的列数与表头不一致。')
nav_ids = [row['trial_id'] for row in nav_rows]
if any(not item_id.strip() for item_id in nav_ids):
    raise ValueError('trial_id 不能为空。')
if any(item_id != item_id.strip() for item_id in nav_ids):
    raise ValueError('trial_id 前后不能带空格。')
if len(nav_ids) != len(set(nav_ids)):
    raise ValueError('每行材料需要唯一的 trial_id。')

nav_by_id = {row['trial_id']: row for row in nav_rows}
nav_ratings = {item_id: None for item_id in nav_ids}
nav_order = [] 
nav = {'loop_i': -1, 'page_i': -1, 'action': None, 'done': False}

nav_base = str(thisExp.dataFileName)
nav_final_path = Path(nav_base + '_final_ratings.csv')
nav_progress_path = Path(nav_base + '_progress_ratings.csv')
nav_final_path.parent.mkdir(parents=True, exist_ok=True)


def nav_write_csv(destination):
    """导出原条件表全部字段，加一列最新评分。"""
    temporary = destination.with_name(destination.name + '.tmp')
    with open(temporary, 'w', newline='', encoding='utf-8-sig') as f:
        writer = csv.DictWriter(
            f, fieldnames=nav_headers + ['sentence_rating']
        )
        writer.writeheader()
        for row in nav_rows:
            output_row = dict(row)
            score = nav_ratings[row['trial_id']]
            output_row['sentence_rating'] = '' if score is None else score
            writer.writerow(output_row)
        f.flush()
        nav_os.fsync(f.fileno())
    nav_os.replace(temporary, destination)


def nav_show_page():
    """显示 page_i 指向的题目及其已有评分。"""
    item_id = nav_order[nav['page_i']]
    row = nav_by_id[item_id]
    这里填写context文本框的名字.setText(row['context']) ## 需要填写的部分
    这里填写句子文本的名字.setText( ## 需要填写的部分
        row['sentence'] + '\n\n'
        + '请根据语境，判断引号“”内的句子是否通顺自然。'
    )
    这里填写评分slider的名字.reset() ## 需要填写的部分
    old_score = nav_ratings[item_id]
    if old_score is not None:
        这里填写评分slider的名字.rating = old_score ## 需要填写的部分
        这里填写评分slider的名字.markerPos = old_score ## 需要填写的部分

    这里填写下一题button的名字.setText( ## 需要填写的部分
        '提交' if nav['page_i'] == len(nav_rows) - 1 else '下一题'
    )


def nav_capture_rating():
    """更新屏幕上这道题的答案，不盲目更新 loop 当前题。"""
    score = 这里填写评分slider的名字.getRating() ## 需要填写的部分
    if score is None:
        return
    if score not in (1, 2, 3, 4, 5, 6, 7):
        raise ValueError('评分应为 1—7 的整数，请检查 Slider。')
    item_id = nav_order[nav['page_i']]
    score = int(score)
    if nav_ratings[item_id] != score:
        nav_ratings[item_id] = score
        if NAV_DYNAMIC_SAVE:
            nav_write_csv(nav_progress_path)
```


#### Begin Routine

```python
if int(填写loop名称.nTotal) != len(nav_rows): 
    raise ValueError('本示例要求 nReps=1、Selected rows 留空、使用整份条件表。') ## 需要填写的部分
if int(填写loop名称.thisN) != len(nav_order):
    raise ValueError('循环进度与已呈现顺序不一致，请检查是否有额外跳转代码。') ## 需要填写的部分

nav_new_id = str(trial_id)
if nav_new_id not in nav_by_id:
    raise ValueError('循环中的 trial_id 与本次读取的条件表不一致。')
if nav_new_id in nav_order:
    raise ValueError('本示例不允许同一 trial_id 重复呈现为新题。')

nav_order.append(nav_new_id)
nav['loop_i'] = len(nav_order) - 1
nav['page_i'] = nav['loop_i']
nav['action'] = None
nav_show_page()

if NAV_DYNAMIC_SAVE and len(nav_order) == 1:
    nav_write_csv(nav_progress_path)
```

#### Each Frame

```python
nav_capture_rating()

nav_action = nav['action']
nav['action'] = None 

if nav_action == 'prev':
    if nav['page_i'] > 0:
        nav['page_i'] -= 1
        nav_show_page()

elif nav_action == 'next':
    nav_page_id = nav_order[nav['page_i']]
    if nav_ratings[nav_page_id] is not None:
        if nav['page_i'] < nav['loop_i']:
            nav['page_i'] += 1
            nav_show_page()
        else:
            if nav['loop_i'] == len(nav_rows) - 1:
                if not all(score is not None
                           for score in nav_ratings.values()):
                    raise ValueError('还有未完成的题目，不能提交。')
                nav_write_csv(nav_final_path)
                nav['done'] = True
            continueRoutine = False
```


### 4.3 大概逻辑

- Builder 的 Loop 决定何时引入新题。`nav_order` 记录实际出现的 ID，`nav['page_i']` 指向屏幕当前题。看到 T03 时点“上一题”，屏幕切回 T02，Loop 仍停在第三次。此时把 T02 从 2 分改为 5 分，会更新 T02 那一行。
- 第一题点击“上一题”维持在原页。当前题还没评分时，“下一题”维持在原页。回看时点“下一题”先回到已呈现过的题目。回到最新一题后再次点“下一题”，`continueRoutine = False` 才推进 Builder Loop。
- `*_final_ratings.csv` 随本次运行的数据文件名前缀保存。每行保留原条件表的全部字段，最右边增加 `sentence_rating`，行顺序跟原表一致。UTF-8 BOM 便于用 Excel 打开中文。代码先写临时文件，再替换目标 CSV。
- 想在提前退出时保留已经选过的分数，把 `NAV_DYNAMIC_SAVE` 改为 `True`。第一次进入评分页时会建立 `*_progress_ratings.csv`，新增或修改评分时会更新它，未答题留空。退出后可查看进度表，本模板每次启动都从第一题开始。


## 5. 修改slider中的marker至想要的款式 

**食用指南：**
在routine中，把以下预制代码贴到 `linebreak_code → Begin Routine` 的换行代码之后。

```python
这里是你slider的名字.marker.选择一个下面的参数填入 = 示例
```

| 参数 | 作用 | 示例 |
|---|---|---|
| `size` | 大小（宽、高） | `(0.12, 0.03)`|
| `fillColor` | 填充颜色 | `'red'` |
| `lineColor` | 边框颜色 | `'white'` |
| `opacity` | 透明度 | `0.8` |
| `vertices` | 形状 | `'rectangle'` |
| `ori` | 旋转角度 | `45` |
| `contrast` | 对比度 | `0.8` |

**示例: 0为宽，1为高**
```python
sentence_rating.marker.size = (
    sentence_rating.size[0] * 0.25, ##slider长度的百分之25
    sentence_rating.size[1]  ##与整体slider高度一直
)
```


## 6. Radio【评分】版本

### Slider的设置
| 页签 | 字段 | Radio 设置与原因 |
| --- | --- | --- |
| Basic | Styles | `radio`，按类别呈现选项 |
| Basic | Labels | `('1分', '2分', '3分', '4分', '5分', '6分', '7分')`，标签唯一，按从低到高排列 |


### 6.1 为什么要转换

| 同一个 4 分响应 | Scrollbar | Radio |
| --- | --- | --- |
| `getRating()` 返回值 | 数字 `4` 或 `4.0` | Labels 中的字符串 `'4分'` |
| 程序保存的评分 | 整数 `4` | 整数 `4` |
| 回看时传给 `.rating` 的值 | 数字 `4` | 第四个选项的位置索引 `3` |

Radio 按类别工作。直接对 `'4分'` 调用 `int()` 会报错。将整数 `4` 直接赋给 Radio 的 `.rating` 会选中索引 4，也就是第五个选项。用标签查分数，恢复时再用分数反查标签位置，就能把显示、保存和回看对应起来。CSV 本身没有字段类型，此处的“整数”指 Python 保存前的值，以及 CSV 中写出的 `4`。 

### 6.2 Radio的预制代码

#### 第一步
先完成4中的预制代码

随后在`nav_code`中`begin experiment`里找到 `NAV_DYNAMIC_SAVE = False` 附近添加下面两项，放在函数定义之前：

```python
NAV_RADIO_LABELS = ('1分', '2分', '3分', '4分', '5分', '6分', '7分')
NAV_LABEL_TO_SCORE = {
    label: position + 1
    for position, label in enumerate(NAV_RADIO_LABELS)
}
```

若 Labels 为 `('1', '2', ..., '7')`，应完整写出这 7 项，并同步修改 `NAV_RADIO_LABELS`。两处必须完全一致。本教程默认使用带“分”的标签，不混用两种写法。

#### 2. 完整替换 nav_capture_rating()

在`nav_code`中`begin experiment`里，找到原有 `def nav_capture_rating():`。将这个函数整个替换成下面内容，不要同时保留两个同名定义：

```python
def nav_capture_rating():
    """radio 标签转换为整数分数，再保存当前屏幕题目的答案。"""
    raw_rating = 这里填写评分slider的名字.getRating() ## 需要填写的部分
    if raw_rating is None:
        return

    if raw_rating not in NAV_LABEL_TO_SCORE:
        raise ValueError(
            f'radio 返回了未配置的标签：{raw_rating!r}，请核对 Labels。'
        )
    score = NAV_LABEL_TO_SCORE[raw_rating]
    item_id = nav_order[nav['page_i']]

    if nav_ratings[item_id] != score:
        nav_ratings[item_id] = score
        if NAV_DYNAMIC_SAVE:
            nav_write_csv(nav_progress_path)
```

#### 3. 完整替换 nav_show_page()

同样在 `Begin Experiment` 中，将原 `nav_show_page()` 整个替换为下面函数：

```python
def nav_show_page():
    """显示当前题目，并把整数旧分数恢复为 radio 选项。"""
    item_id = nav_order[nav['page_i']]
    row = nav_by_id[item_id]
    这里填写context文本框的名字.setText(row['context'])## 需要填写的部分
    这里填写句子文本的名字.setText(## 需要填写的部分
        row['sentence'] + '\n\n'
        + '请根据语境，判断引号“”内的句子是否通顺自然。'
    )

    这里填写评分slider的名字.reset()
    old_score = nav_ratings[item_id]
    if old_score is not None:
        old_position = old_score - 1
        这里填写评分slider的名字.rating = old_position ## 需要填写的部分
        这里填写评分slider的名字.markerPos = old_position ## 需要填写的部分

    这里填写下一题button的名字.setText( ## 需要填写的部分
        '提交' if nav['page_i'] == len(nav_rows) - 1 else '下一题'
    )
```
