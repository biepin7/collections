# go 刷题用到的技巧

[toc]

## about hash/map

格式:

```go
map[kepType]valueType
```

1. key 是唯一的，多次赋值取最后一次赋值
2. map是无序的



## 奇怪的函数的模板

### gcd

```
func gcd(x, y int) int {
    for y != 0 {
    	x, y = y, x%y
    }
    return x
}
```

### Fibonacci

```
func fib(n int) int {
    x, y := 0, 1
    for i := 0; i < n; i++ {
    	x, y = y, x+y
}
return x
}
```


### bool to int
```
func btoi(b bool) int {
    if b {
    	return 1
    }
    return 0
}
```

### min int

```
func min(a, b int) int {
	if a < b {
		return a
	}
	return b
}

```

### 前缀测试

```
func HasPrefix(s, prefix string) bool {
    return len(s) >= len(prefix) && s[:len(prefix)] == prefix
}
```

后缀测试

```
func HasSuffix(s, suffix string) bool {
	return len(s) >= len(suffix) && s[len(s)-len(suffix):] ==suffix
}
```

### 字串包含

```
func Contains(s, substr string) bool {
    for i := 0; i < len(s); i++ {
        if HasPrefix(s[i:], substr) {
        	return true
        }
    }
return false
}
```

