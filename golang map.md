```go
package main  
  
import "fmt"  
  
func main() {  
// Create a map where the value is a slice of strings  
myMap := make(map[string][]string)  
  
// Create some slices  
slice1 := []string{"apple", "banana"}  
slice2 := []string{"orange", "grape"}  
  
// Set the slices as values in the map  
myMap["fruits1"] = slice1  
myMap["fruits2"] = slice2  
  
// Print the map  
fmt.Println(myMap)  
// Output: map[fruits1:[apple banana] fruits2:[orange grape]]  
  
// Access a slice from the map  
retrievedSlice := myMap["fruits1"]  
fmt.Println(retrievedSlice)  
// Output: [apple banana]  
  
// Modify the slice (this will not affect the original slice in the map)  
**retrievedSlice = append(retrievedSlice, "cherry")**  
fmt.Println(retrievedSlice)  
// Output: [apple banana cherry]  
fmt.Println(myMap["fruits1"])  
// Output: [apple banana]  
  
// To update the slice in the map, you need to reassign it  
myMap["fruits1"] = retrievedSlice  
fmt.Println(myMap["fruits1"])  
// Output: [apple banana cherry]  
}

```

slice 의 특징으로, 동적으로 추가할 때는 append 함수를 사용해야 하는데,
append는 받은 slice 자체를 변경한 것이 아닌, 변경된 slice를 return한다.

