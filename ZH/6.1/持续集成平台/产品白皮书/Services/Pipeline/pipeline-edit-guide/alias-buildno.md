# 为流水线开启自定义构建号

## 为什么要自定义构建号

默认的流水线构建号是由 1 自增的数字组成，为了增加可辨识度，我们允许您对流水线的构建号做出别名设置，开启后将在页面展示上优先显示您的自定义构建号格式。

## 开启方法

进入流水线基础设置页，设置对应的构建号规则即可，比如：

```text
${{DATE:"yyMMdd"}}.${{BUILD_NO_OF_DAY}}
```

![png](../../../assets/service_pipeline_edit_build_no.png)

## 规则说明

### 可用格式

| KEY | Example |
| :--- | :--- |
| YEAR | 2020 |
| DAY\_OF\_MONTH | 28 |
| DAY\_OF\_YEAR | 285 |
| HOUR\_OF\_DAY | 23 |
| MINUTE | 55 |
| MONTH\_OF\_YEAR | 3 |
| BUILD\_NO\_OF\_DAY | 从 1 自增，每天重置 |
| DATE:"yyMMdd hh:MM" | 20201028 10:08 |
| SECOND | 59 |

{% hint style="info" %}
* 新增的字段对应变量：${BK\_CI\_BUILD\_NUM\_ALIAS}
* 该字符长度最长 256 字符
* 该字符所能生成的真实字符串长度最长 256 字符
* 配置自定义构建号处需强提醒：超出长度限制的部分会被截断
* 构建号超长不影响流水线的构建
{% endhint %}

### 允许的字符

* 规则允许的字符改为：^\[\w-{}\(\) +?.:$"\]{1,256}$，自定义内部版本号规则只能由\[大写和小写字母，数字，空格，-，\_，。，：，{，}，（，），“，+，？，$\]字符组成，并且长度为在 1-256 之间 
* 格式化时间的规则在 db 请配置成：DATE:"\(.+?\)"，\(.+?\)指的是通用规则，支持用户配置由大小写字母、空格、:、-等字符组成的规则，如：yyyy-MM-dd HH:mm:ss 3、用户配置规则，通过$引用具体的规则 xx

## 效果展示

![png](../../../assets/service_pipeline_edit_build_no_1.png)

![png](../../../assets/service_pipeline_edit_build_no_2.png)

