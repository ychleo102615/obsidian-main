[doc](https://www.lua.org/pil/9.1.html)
create接收一個function參數
```
co = coroutine.create(function ()
        print("hi")
    end)
    
print(co)   --> thread: 0x8071d98
```

一個coroutine有三種狀態：suspended, running, dead
剛建立完的coroutine是suspended的
```
print(coroutine.status(co))   --> suspended
```

呼叫resume開始或是繼續這個coroutine
```
coroutine.resume(co)   --> hi

```

範例程式呼叫完立刻結束
```
print(coroutine.status(co))   --> dead
```

呼叫yeild可以跳出coroutine
```
co = coroutine.create(function ()
        for i = 1, 10 do
            print("co", i)
            coroutine.yield()
        end
    end)
         
coroutine.resume(co)    --> co   1
coroutine.resume(co)    --> co   2
coroutine.resume(co)    --> co   3
...
coroutine.resume(co)    --> co   10
coroutine.resume(co)    -- prints nothing

print(coroutine.resume(co))
--> false   cannot resume dead coroutine

```