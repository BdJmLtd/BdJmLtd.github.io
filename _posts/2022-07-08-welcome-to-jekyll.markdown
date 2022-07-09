---
layout: post
title:  "Welcome to Jekyll!"
date:   2022-07-08 10:00:00 +0800
categories: jekyll
---

## 文字和图片

### 文字

You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. You can rebuild the site in many different ways, but the most common way is to run `jekyll serve`, which launches a web server and auto-regenerates your site when a file is updated.

Jekyll requires blog post files to be named according to the following format:

`YEAR-MONTH-DAY-title.MARKUP`

Where `YEAR` is a four-digit number, `MONTH` and `DAY` are both two-digit numbers, and `MARKUP` is the file extension representing the format used in the file. After that, include the necessary front matter. Take a look at the source for this post to get an idea about how it works.

Jekyll also offers powerful support for code snippets:

{% highlight ruby %}
def print_hi(name)
puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
{% endhighlight %}

Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].

### 图片

{:refdef: style="text-align: center;"}
![修改成图片的描述信息](/assets/image/spring-summer-autumn-winter.jpg)
{: refdef}

### 表格

| 名字  | User Name   | Email                | Role      |
|-----|-------------|----------------------|-----------|
| 杰瑞鼠 | Jerry Mouse | jerry@example.com    | Author    |
| 汤姆猫 | Tom Cat     | tom@example.com      | Committer |
| 张三  | Zhang San   | zhangsan@example.com | Author    |
| 李四  | Li Si       | lisi@example.com     | Committer |

### 超链接

请点击[我](https://www.baidu.com/)，跳转到百度。

## 代码和数学公式

### 代码

```java
public class Main {
    public static void main(String[] args) {
        // TODO: 打印当前的版本信息
        String str = "501548.722";
        BigDecimal surface = new BigDecimal("31.6");
        BigDecimal depth = new BigDecimal("1.32");
        BigDecimal elevation = new BigDecimal("30.28");
        boolean flag = MathUtils.checkSum(elevation, depth, surface);
        System.out.println(flag);
    }
}
```

### 数学公式

<p>
示例一，在文字当中，写一个数学公式：
\( a^{2} + b^{2} = c^{2} \)
。
</p>

<p>
示例二，写一个单独占一行的数学公式：
</p>

<p>
    \[\begin{aligned}
    h_{i} - P_{0} - E_{i} = R_{Di} \: {q_{Di}}^{e}
    \end{aligned}\]
</p>

<p>
示例三，一个比较复杂的数学公式：
</p>

<p>
  \[\begin{split}\begin{aligned}
  q_{Di} =
  \left\{
  \begin{array}{l l}
  D_{i}                                                            &amp; p_{i} \ge P_{f}     \\
  D_{i} \left( \frac{p_{i} - P_{0}}{P_{f} - P_{0}} \right) ^{\frac{1}{e}} \; &amp; P_{0} &lt; p_i &lt; P_{f} \\
  0                                                                &amp; p_{i} \le P_{0}
  \end{array}
  \right.
  \end{aligned}\end{split}\]
</p>

<p>
示例四，多个公式以“等号”对齐。
</p>

<p>
    也就是说，压力差（\(\Delta p\)） = 流体密度（\( \rho \)） X 重力加速度（\(g\)） X 距离 （\(h\)）
</p>
<p>
    \[\begin{align}
    \Delta p &= \rho g h \\
    Pa &= \frac{kg}{m^{3}} \times \frac{m}{s^{2}} \times m \\
    \frac{N}{m^{2}} &= ( kg \times \frac{m}{s^{2}}) \times \frac{1}{m^{2}} \\
    \frac{N}{m^{2}} &= (m a) \times \frac{1}{m^{2}} \\
    \frac{N}{m^{2}} &= F \times \frac{1}{m^{2}} \\
    \frac{N}{m^{2}} &= N \times \frac{1}{m^{2}} \\
    \end{align}\]
</p>

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
