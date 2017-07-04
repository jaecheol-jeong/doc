
## Golang Read Excel File

![golang-excel](/images/golang-excel.png "excel read")

<pre>
package main

import (
	"fmt"

	"github.com/tealeg/xlsx"
)

func main() {
	excelFileName := "c:\\test.xlsx"
	xlFile, err := xlsx.OpenFile(excelFileName)
	if err != nil {
		panic(err)
	}
	for _, sheet := range xlFile.Sheets {
		for _, row := range sheet.Rows {
			for _, cell := range row.Cells {
				text, _ := cell.String()
				fmt.Printf("%10s", text)
			}
			fmt.Printf("\n")
		}
	}
}
</pre>

> 1. import github.com/tealeg/xlsx
> 2. ~~
