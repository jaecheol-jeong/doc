## golang Console Caledar

`#go` , `#golang`, `#calendar`

#소스
```go
package main

import (
	"fmt"
	"time"
)

type Cal struct {
	Year         int
	Month        int
	LastDay      int
	BeginWeekday int
}

func main() {
	fmt.Printf("Calendar\n")
	var y, m, d = time.Now().Date()
	fmt.Printf("today : %d-%d-%d\n", y, m, d)

	var cal Cal
	cal.Year = y
	cal.Month = int(m)
	cal.LastDay = lastDay(y, int(m))
	_, cal.BeginWeekday = firstWeek(y, int(m))

	showHeader()

	showCalendar(cal)
}

func showCalendar(c Cal) {
	k := c.BeginWeekday + 1
	n := 1

	for j := 0; j < c.BeginWeekday; j++ {
		fmt.Printf("%5s", "   ")
	}

	for i := k; i <= 7; i++ {
		if n > c.LastDay {
			break
		}

		fmt.Printf("%-5d", n)
		if i == 7 {
			fmt.Printf("\n")
			i = 0
		}

		n++
	}
}

func showHeader() {
	fmt.Printf("%-5s%-5s%-5s%-5s%-5s%-5s%-5s", "SUN", "MON", "TUE", "WEB", "THU", "FRI", "SAT")
	fmt.Printf("\n")
	fmt.Printf("%-5s", "---")
	fmt.Printf("%-5s", "---")
	fmt.Printf("%-5s", "---")
	fmt.Printf("%-5s", "---")
	fmt.Printf("%-5s", "---")
	fmt.Printf("%-5s", "---")
	fmt.Printf("%-5s", "---")
	fmt.Printf("\n")
}

func firstWeek(year int, month int) (string, int) {
	m := time.Month(month)
	w := time.Date(year, m, 1, 0, 0, 0, 0, time.Local).Weekday()

	weekday := int(w)

	switch w {
	case 0:
		return "일", weekday
	case 1:
		return "월", weekday
	case 2:
		return "화", weekday
	case 3:
		return "수", weekday
	case 4:
		return "목", weekday
	case 5:
		return "금", weekday
	case 6:
		return "토", weekday
	case 7:
		return "일", weekday
	}

	return "", 0
}

func lastDay(year int, month int) int {
	if month == 12 {
		month = 1
		year++
	} else {
		month++
	}

	m := time.Month(month)
	_, _, _d := time.Date(year, m, 0, 1, 0, 0, 0, time.Local).Date()

	return _d
}
```

결과

![](https://jaecheol-jeong.github.io/doc/images/calendar.png "calendar")
