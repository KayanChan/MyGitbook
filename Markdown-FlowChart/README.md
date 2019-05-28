# Markdown-流程图

@2019-05-27 14:19

@(工具类笔记)[markdown语法|流程图]



### 定义元素

语法：`tag=>type: content:>url`，将流程图代码包含在`···flow`和`···`之间

* tag： 流程图中的标签（元素）名称，一般为流程的英文缩写和数字的组合
* type：标签类型，共6种：
  * 开始 `start`
  * 结束 `end`
  * 操作 `operation`
  * 子程序操作说明 `subroutine` 
  * 条件 `condition`
  * 输入密码 `inputoutput`

* content：流程图文本框中的描述内容
* url：一个连接，与框框中的文本相绑定



### 指向流程(连接元素)

语法：`tag1->tag2`

- 使用 -> 来连接两个元素
- 对于`condition`类型，有`yes`和`no`两个分支，`e.g.`cond(yes)`和`cond(no)`
- 每个元素可以制定分支走向，默认向下，也可以用`right`指向右边，`e.g.`cond2(yes,right)`



### 示例

```flow
st=>start: A获取授权，向B申请授权

e1=>end: A申请授权成功，获取B的数据

e2=>end: A申请授权失败

op1=>operation: B同意授权

op2=>operation: A得到令牌(短期里可复用)

op3=>operation: B拒绝授权

cond=>condition: B是否同意授权A获得授权

input=>inputoutput: A可输入令牌

st->cond
cond(yes)->op1->op2->input->e1
cond(no)->op3->e2
```



