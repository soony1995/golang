### worker pool 
>Concurrency limiting goroutine pool. Limits the concurrency of task execution, not the number of tasks queued. Never blocks submitting tasks, no matter how many tasks are queued.


```
type Site struct {
	URL string
}

type Result struct {
	Status int
}

func crawl(wId int, jobs <-chan Site, results chan <- Result){
	for site := range jobs{
		log.Printf("worker ID: %d\n",wId)
		resp,err:=http.Get(site.URL)
		if err !=nil{
			log.Println(err.Error())
		}
		results <- Result{Status: resp.StatusCode}
	}
}

func main() {
	fmt.Println("work pools in go.")

	jobs := make(chan Site,3)
	results := make(chan Result, 3)

	for w := 1; w<=3; w++{  // 3명의 worker가 Jobs 채널에 데이터가 송신되기를 기다리고 있음.
		go crawl(w,jobs,results)
	}

	urls := []string{
		"https://naver.com",
		"https://daum.net",
		"https://google.com",
		"https://example.com",
	}

	for _,url := range urls{
		jobs <- Site{URL: url}
	}

    // jobs에 데이터가 들어오는 동시에 처리함.
	close(jobs)
	for a := 1 ; a <=4 ; a++{
		result:= <-results
		log.Println(result)
	}
}
```