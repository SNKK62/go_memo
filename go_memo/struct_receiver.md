# struct/receiver

## struct
```go
type Task struct {
    Title    string
    Estimate int
}

task1 := Task{
    Title:    "Learn Golang",
    Estimate: 3,
}
task1.Title = "Learning Go"
fmt.Printf("%[1]T %+[1]v %v \n", task1, task1.Title)

var task2 Task = task1
task2.Title = "new"  #task1.Title == "Learning Go"

task1p := &Task{
    Title:    "Learn concurrency",
    Estimate: 2,
}
(*task1p).Title = "Changed"
task1p.Title = "Changed"
```
- %+v で展開
- 代入するとcopyされる
- dereferenceは省略可能

## receiver
```go
func (task Task) extendEstimate() {
    task.Estimate += 10
}
func (taskp *Task) extendEstimatePointer() {
    taskp.Estimate += 10
}
```
- value receiver は変更されない
- pointer receiver は変更される
