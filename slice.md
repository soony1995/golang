### 배열의 값을 변경하는 방법 

```
func main() {
	a := []RecordListResult{
		{
			Id:                 1,			
		},
		{
			Id:                 3,
		},
	}

  for _,v := range a{
    v.Id = 11111
    fmt.Println(v.Id)
  // {11111}
  // {11111}  
  }
  fmt.Println(a)
  // [{1} {3}]

  위의 예시 처럼 value를 이용해 값을 할당한다고 해서 a의 Id 값이 바뀌지 않는 것을 확인 할 수 있다.
  왜냐면 for문 자체는 값을 복사해서 넘겨주기 때문이다.

  a의 값 자체를 변경 하고 싶다면,

  for i := range a {
    a[i].Id = 11111
	 	fmt.Println(a[i])
	 }
  fmt.Println(a)
  // [{11111} {11111}]
  처럼 인덱스를 이용해 접근해 값을 변경하게 된다면 정상적으로 바뀌는 것을 알 수 있다.
}
```
