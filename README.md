# go-masscan

go-masscan is a golang library to run masscan scans, parse scan results.


## Installation


```sh
go get github.com/dean2021/go-masscan
```
to install the package

```go
import "github.com/dean2021/go-masscan"
```

## Example

```go
package main

import (
	"github.com/dean2021/go-masscan"
	"fmt"
)

func main() {

	m := masscan.New()

	// masscan可执行文件路径,默认不需要设置
	//m.SetSystemPath("/usr/local/masscan/bin/masscan")

	// 扫描端口范围
	m.SetPorts("0-65535")

	// 扫描IP范围
	m.SetRanges("0.0.0.0/8")

	// 扫描速率
	m.SetRate("2000")

	// 隔离扫描名单
	m.SetExclude("127.0.0.1")

	// 开始扫描
	err := m.Run()
	if err != nil {
		fmt.Println("scanner failed:", err)
		return
	}

	// 解析扫描结果
	results, err := m.Parse()
	if err != nil {
		fmt.Println("Parse scanner result:", err)
		return
	}

	for _, result := range results {
		fmt.Println(result)
	}

}

```