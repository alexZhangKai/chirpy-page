---
title: Golang Learning Log
date: 2023-10-14 22:10:10 +1000
categories: [Golang]
tags: [Golang]
pin: false
math: false
mermaid: false
image:
  path: /wip.jpg
  alt: 'Photo by Antoni Shkraba: https://www.pexels.com/photo/a-businessman-wearing-a-wireless-headset-8191969/'
---

## Compile

``` shell

go build main.go
./main

go run main.go

```

## Variable and Type

``` go
package main

import "fmt"

func main() {

  // variable
  var stationName string
  var nextTrainTime int8
  var isUptownTrain bool
  
  stationName = "Union Square"
  nextTrainTime = 12
  isUptownTrain = false
  
  fmt.Println("Current station:", stationName)
  fmt.Println("Next train:", nextTrainTime, "minutes")
  fmt.Println("Is uptown:", isUptownTrain)
  
  stationName = "Grand Central"
  nextTrainTime = 3
  isUptownTrain = true
  
  fmt.Println("")
  fmt.Println("Current station:", stationName)
  fmt.Println("Next train:", nextTrainTime, "minutes")
  fmt.Println("Is uptown:", isUptownTrain)

  myvar := "my variable"

  var flavorScale float32 = 5.8

  const earthsGravity = 9.80665


  // if statement
  if isHungry := false; isHungry {
    fmt.Println("Eat the cookie") 
  } else {
    fmt.Println("Step away from the cookie...")
  }

  // switch statement
  switch clothingChoice := "sweater"; clothingChoice {
  case "shirt":
    fmt.Println("We have shirts in S and M only.")
  case "polos":
    fmt.Println("We have polos in M, L, and XL.")
  case "sweater":
    fmt.Println("We have sweaters in S, M, L, and XL.")
  case "jackets":
    fmt.Println("We have jackets in all sizes.")
  default:
    fmt.Println("Sorry, we don't carry that")
  }

  // random
  rand.Seed(time.Now().UnixNano())
  amountLeft := rand.Intn(10000)

  // pointer and reference
  lyrics := "Moments so dear" 
  pointerForStr := &lyrics

  *pointerForStr = "Journeys to plan" 

  fmt.Println(lyrics) // Prints: Journeys to plan
}

// function example
func multiplier(x, y int32) (int32, int32, int32) {
  return x * y, x, y
}

// defer statement
// avoid logging at each return
func calculateTaxes(revenue, deductions, credits float64) float64 {
  defer fmt.Println("Taxes Calculated!")
  taxRate := .06143
  fmt.Println("Calculating Taxes")

  if deductions == 0 || credits == 0 {
    return revenue * taxRate
  }
  

  taxValue := (revenue - (deductions * credits)) * taxRate
  if taxValue >= 0 {
    return taxValue
  } else {
    return 0
  }
}
```