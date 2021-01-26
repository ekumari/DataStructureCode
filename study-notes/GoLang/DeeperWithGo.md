## Variables

GO is static type

Type
bool        true/false
string      ""
int         0  -10000 
float64     10.000001 0.00009

### Definition

	//var card string = "Ace of Spades"
	card := "Ace of Spades"
	card = "Five of Diamonds"

### Function


func newDeck() string { // return type string
	return "Five of Diamonds"
}

### Slices 
- Data Structure
  - Array: fixed length
  - Slice: An array that can grow or shrink

- Every element in a slice must be of same type
- cards := [] string
- cards := []string{"Ace of Sheperds", newDeck()}
    for i, card := range cards {
		fmt.Println(i, card)
	}

Add new element at the end of the slice.
    - cards = append(cards, "Six of Sphades") // Doesnt modify the existing cards rather it returns the new slice with append data and reassigned to cards

### OO Aproach Vs Go Approach

- Go is not object oriented programming langauage, means no classes

Basic Go Types

- string, int, float, array and map
- type deck[] string // array of string
- function with 'deck' as a receiver

Code Flow

- main.go > deck.go > deck_test.go

### Receiver Functions

    func (d deck) print(): Any variable of type 'deck' now get access to the "print" method

Slice is zero-index. 

fruits = apple, banana, grape, orange

fruits[0:2] = apple , banana 

fruits[startIndexIncluding: upToNotIncluding]

### Type Converstion

- []byte("Hi there!")
  type    value

  deck -> []string -> string -> []byte

  []byte: string of character

## Testing with Go
    - Writing go code, no framework
    - To make a test, create a new file ending in _test.go