# 正規表達式 Regular Expressions(RegExp)
## 1.基本介紹
<table>
  <thead>
    <th>符號</th>
    <th style="width:100px">說明</th>
    <th>簡單範例</th>
  </thead>
  <tbody>
    <tr><td>\</td><td>跳脫字元</td><td>/A\*/可比對A*，其中*為特殊字元，需跳脫其原本意思。</td></tr>
    <tr><td>^</td><td>比對起始位置</td><td>/^ABC/可比對字串開頭是否為ABC</td></tr>
    <tr><td>$</td><td>比對結束位置</td><td>/ABC$/可比對字串結尾是否為ABC</td></tr>
    <tr><td>*</td><td>比對前一個字元'零'次或更多次</td><td>/bo*/可比對Good booook中的booo，亦可比對Good bk中的 b</td></tr>
    <tr><td>+</td><td>比對前一個字元'一'次或更多次</td><td>/a+/可比對candy中的a，和caaandy中的aaa</td></tr>
    <tr><td>?</td><td>比對前一個字元'零'次或'一'次</td><td>/e?le?/可比對angel中的el</td></tr>
    <tr><td>.</td><td>比對任何一個字元（但換列符號不算）</td><td>/.n/可比對nay, an apple is on the tree中的an和on</td></tr>
    <tr><td>(x)</td><td>比對x並將符合的部分存入一個變數</td><td><code>"https://www.google.com".replace(/(^https?:\/\/)(.*)/,'$2')</code>比對開始時是否包含http，s可出現零次或一次，接著:，然後用跳脫字元\ /\ /搜尋//，將結果存進變數$1，(.*)搜尋任意字元零次或更多次，將結果存進變數$2，最後把結果replace為$2，會得到www.google.com</td></tr>
    <tr><td>{n}</td><td>比對前一個字元n次，n為一個正整數</td><td>/a{3}/可比對aa aaa aaaa其中的aaa</td></tr>
    <tr><td>{n,}</td><td>比對前一個字元'至少'n次，n 為一個正整數</td><td>/a{3,}/g可比對aa aaa aaaa其中的aaa和aaaa</</td></tr>
    <tr><td>{n,m}</td><td>比對前一個字元至少n次，至多m次，m、n均為正整數</td><td>/a{3,4}/g可比對aa aaa aaaa其中的aaa和aaaa</td></tr>
    <tr><td>[xyz]</td><td>比對中括弧內的任一個字元</td><td>/[ecm]/g可比對welcome中的e和c和m和e</td></tr>
    <tr><td>[^xyz]</td><td>比對不在中括弧內出現的任一個字元</td><td>/[^ecm]/g可比對welcome中的w和l和o可見出其與[xyz]功能相反</td></tr>
    <tr><td>\b</td><td>比對英文字的邊界，例如空格</td><td>/\bn\w/可以比對noonday中的no、/\wy\b/可比對possibly yesterday中的ly</td></tr>
    <tr><td>\B</td><td>比對非「英文字的邊界」</td><td>/\w\Bn/可以比對noonday中的on、/y\B\w/可以比對possibly yesterday中的ye</td></tr>
    <tr><td>\d</td><td>比對任一個數字，等同於[0-9]</td><td></td></tr>
    <tr><td>\D</td><td>比對任一個非數字，等同於 [^0-9]</td><td></td></tr>
    <tr><td>\n</td><td>比對換列</td><td></td></tr>
    <tr><td>\r</td><td>比對carriage return</td><td></td></tr>
    <tr><td>\s</td><td>比對任一個空白字元</td><td></td></tr>
    <tr><td>\S</td><td>比對任一個'非'空白字元</td><td></td></tr>
    <tr><td>\w</td><td>比對數字英文字母或底線( _ )等同於[A-Za-z0-9_ ]</td><td>/\w/可比對 . A _ !9 中的A和 _ 和9</td></tr>
    <tr><td>\W</td><td>比對非「數字英文字母或底線」，等同於[^A-Za-z0-9_ ]</td><td>/\W/可比對 .A _ !9 中的 . 和 !</td></tr>
    <tr><td></td><td></td><td></td></tr>
  </tbody>
</table>

## 2.Flag
* g 全域搜尋
* i 不區分大小寫
* m 多行搜尋
* u 將patten視為unicode
* y 又叫 [sticky search](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp/sticky "sticky search")

## 3.貪婪模式(greddy)&非貪婪模式(un-greddy)
貪婪模式：
```
"abcXabcXabcX".match(/.+X/) = ["abcXabcXabcX"]
```
非貪婪模式(加上問號)：
```
"abcXabcXabcX".match(/.+?X/) = ["abcX"]
```

## 4.Group
利用括號( )來代表group：

範例1：
```
"https://google.com".replace(/(^https?:\/\/)(.*)/,'$2') = google.com
```
> 解說：其中有2個括號第1個括號代表$1、第2個代表$2...依此類推，最後將整個字串替代為$2

範例2：

```
"aaabbbbcccccdd".replace(/(.)\1+/g,'$1') = "abcd"
```
> 解說：括號後方\1代表匹配到的第一個群組，後面的+代表匹配到的那個字重複1次至多次，最後用$1來覆蓋掉($1為匹配到的那個單一字母)

範例3：
```
/(\w).*\1/.test("asdsz") = true
```
> 解說：此為測試字串中是否有重複之字母，(\w)代表匹配到一個單一字母，並存入變數群組1，然後緊接著任意字元重複0次至多次，然後再接著群組1匹配到的字(\1)，會匹配到sds，所以 `return true`
## 4-1. ( ? : )
沿用範例1
```
"https://google.com".replace(/(?:^https?:\/\/)(.*)/,'$1') = google.com
```
> (? :)的作用在於將匹配到的內容去除，所以$1 已變成第二個括弧匹配到的內容
## 4-2. ( ? ! )和( ? = )
( ? ! )為反向向前匹配如：
```
/a(?!foo)/.test("afoo") = false
```
> a的後面不能為foo

( ? = )為正向向前匹配如：
```
/a(?=foo)/.test("afoobar") = true
```
> a的後面要為foo

注意：
```
/a(?=foo)bar/.test("afoobar") = false
```
> 匹配a後面為foo後，會再匹配a的後面是否為bar，a的後面不可能同時為foo又是bar所以永遠都會 `return false`
## 4-3.( ? < ! )和( ? < = )
( ? < ! )為反向向後匹配如：
```
/(?<!foo)bar/.test("foobar") = false
```
> foo後面不能為bar，所以 `return false`

( ? < = )為正向向後匹配如：
```
/(?<=foo)bar/.test("asdfoobarasd") = true
```

> foo後面為bar即 `return true` 再往後的asd就不會再匹配
