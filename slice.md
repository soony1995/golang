```
func main() {
	a := []RecordListResult{
		{
			Id:                 1,
			Filename:           "test",
			FileExist:          true,
			Transcoding:        true,
			TranscodedFilePath: "test",
			DirPath:            "test",
			CreatedAt:          time.Now(),
		},
		{
			Id:                 3,
			Filename:           "test",
			FileExist:          true,
			Transcoding:        true,
			TranscodedFilePath: "test",
			DirPath:            "test",
			CreatedAt:          time.Now(),
		},
	}

  for _,v := range a{
    v.Id = 11111
    fmt.Println(v.Id)
  // {11111 test true true test test 2023-08-14 09:31:58.326524152 +0000 UTC m=+0.000117601}
  // {11111 test true true test test 2023-08-14 09:31:58.326541652 +0000 UTC m=+0.000134501}  
  }
  fmt.Println(a)
  // [{1 test true true test test 2023-08-14 09:31:58.326524152 +0000 UTC m=+0.000117601} {3 test true true test test 2023-08-14 09:31:58.326541652 +0000 UTC m=+0.000134501}]

  위의 예시 처럼 value를 이용해 값을 할당한다고 해서 a의 Id 값이 바뀌지 않는 것을 확인 할 수 있다.
  왜냐면 for문 자체는 값을 복사해서 넘겨주기 때문이다.

  a의 값 자체를 변경 하고 싶다면,

  for i := range a {
    a[i].Id = 11111
	 	fmt.Println(a[i])
	 }
  fmt.Println(a)
  // [{11111 test true true test test 2023-08-14 09:34:19.955732526 +0000 UTC m=+0.000117201} {11111 test true true test test 2023-08-14 09:34:19.955749625 +0000 UTC m=+0.000133600}]
  처럼 인덱스를 이용해 접근해 값을 변경하게 된다면 정상적으로 바뀌는 것을 알 수 있다.
}
```