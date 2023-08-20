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

<!-- test file -->

package main

import (
	"testing"
)

func TestAdd(t *testing.T) {
	type args struct {
		x int
		y int
	}
	tests := []struct {
		name string
		args args
		want int
	}{
        // TODO
	}
	for _, tt := range tests {
		t.Run(tt.name, func(t *testing.T) {
			if got := Add(tt.args.x, tt.args.y); got != tt.want {
				t.Errorf("Add() = %v, want %v", got, tt.want)
			}
		})
	}
}
```
- `:GoTests` でカーソル上の関数のテストが自動生成
- `:GoTestsAll` で全ての関数のテストが自動生成
- `go test -v .` でテストの結果を詳細表示
- `:GoCoverageToggle` でテストの網羅性をcheckできる
