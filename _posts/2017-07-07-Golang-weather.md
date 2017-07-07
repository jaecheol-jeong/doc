---
layout: post
title: Golang OpenWeatherMap API 사용하기
---
## Golang OpenWeatherMap API 사용하기

[openweathermap](https://openweathermap.org/)

API 사용이 무료다.. 분당 60회까지만...

[가격표 - price](https://openweathermap.org/price)


```go
package main

import (
	"bufio"
	"encoding/json"
	"fmt"
	"io/ioutil"
	"net/http"
	"os"
)

// Weather is struct type
type Weather struct {
	Coord struct {
		Lon float32 `json:"lon"`
		Lat float32 `json:"lat"`
	} `json:"coord"`
	Weather []struct {
		No          int    `json:"id"`
		Main        string `json:"main"`
		Description string `json:"description"`
		Icon        string `json:"icon"`
	} `json:"weather"`
	Main struct {
		Temp      float32 `json:"temp"`
		Pressure  float32 `json:"pressure"`
		Humidity  int     `json:"humidity"`
		TempMin   float32 `json:"temp_min"`
		TempMax   float32 `json:"temp_max"`
		SeaLevel  float32 `json:"sea_level"`
		GrndLevel float32 `json:"srnd_level"`
	} `json:"main"`
	Wind struct {
		Speed float32 `json:"speed"`
		Deg   float32 `json:"deg"`
	} `json:"wind"`
	Clouds struct {
		All int `json:"all"`
	} `json:"clouds"`
	Dt  float32 `json:"dt"`
	Sys struct {
		Message float32 `json:"message"`
		Country string  `json:"country"`
		Sunrise float32 `json:"sunrise"`
		Sunset  float32 `json:"sunset"`
	} `json:"sys"`
	No   int    `json:"id"`
	Name string `json:"name"`
	Cod  int    `json:"cod"`
}

func main() {

	resp, err := http.Get("http://api.openweathermap.org/data/2.5/weather?q=Seoul,KR(지역)&APPID=(apikey)&units=metric")

	if err != nil {
		panic(err)
	}

	data, err := ioutil.ReadAll(resp.Body)
	if err != nil {
		panic(err)
	}

	println(string(data))

	var szData = []byte(data)
	var weather Weather
	err = json.Unmarshal(szData, &weather)
	if err != nil {
		panic(err)
	}

	fmt.Printf("최고 기온: %.2f °C\n", weather.Main.TempMax)
	fmt.Printf("최저 기온: %.2f °C\n", weather.Main.TempMin)
	fmt.Printf("현재기온: %.2f °C\n", weather.Main.Temp)

	reader := bufio.NewReader(os.Stdin)
	text, _ := reader.ReadString('\n')
	fmt.Println(text)
}

```

> 1. 회원 가입후 key를 발급받을 수 있다.
> 2. 발급받은 key를 APPID= 에 넣으면 된다.
> 3. q= 다음에 지역코드를 넣으면 되는데, Seoul,KR 또는 Busan,KR 이런식으로 넣거나 
api.openweathermap.org/data/2.5/weather?id=2172797
이렇게 (도시ID) 또는  api.openweathermap.org/data/2.5/weather?lat=35&lon=139
(위,경도)를 넣어도 된다.

> TAG : #golang #weather #openweathermap
