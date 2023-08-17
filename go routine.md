### shared variables in go routine 

### go routine in for loop 
```
1)
var wg sync.WaitGroup
for i := 0; i < 3; i++ {
    wg.Add(1)
    go func() {
        defer wg.Done()
        fmt.Println(i)
    }()
}
wg.Wait()
fmt.Println("Done")

결과: 
3
3
3
Done

2)
var wg sync.WaitGroup
	for i := 0; i < 5; i++ {
		wg.Add(1)		
		go func(i int) {
			defer wg.Done()
			fmt.Println(i)
		}(i)
	}
	wg.Wait()
	fmt.Println("Done")

결과:
0
4
1
2
3
Done

```
1번의 경우
> 우리가 지정한 for loop 속 goroutine 이 실제로 실행되기 전에 loop 을 다 돈 상태에서 원소 값을 참조하면서 임시 value 값 (마지막 원소의 복제본)만 반복해서 얻어오게 되는 것이다.

2번의 경우, 
> 각 goroutine 마다 독립적인 i를 얻을 수 있다. 

-> 왜 이렇게 되는 지에 대한 확실한 답변을 찾아야 할 듯 하다.