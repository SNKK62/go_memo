# Unit Test
```go
func Add(x, y int) int {
    return x + y
}
func Divide(x, y int) float32 {
    if y == 0 {
        return 0
    }
    return float32(x) / float32(y)
}

```
- `:GoTests` でカーソル上の関数のテストが自動生成
- `:GoTestsAll` で全ての関数のテストが自動生成
- `go test -v .` でテストの結果を詳細表示
- `:GoCoverageToggle` でテストの網羅性をcheckできる
