## Data Structure

### struct
- Collection of properties that are related together.

type person struct {
	firstName string
	lastName  string
}

- Embedding Struct

    type contactInfo struct{
        email string
        zipCode int
    }

    type person struct {
        firstName string
        lastName  string
        contact   contactInfo
    }

    Put comma at the end.

- Pass by value
- struct with pointer

### Pointer

- &variable: memory address of the variable this variable is pointing to.
- *pointer: value this memory address is pointing at.
    
    func (pointerToPerson *person) updateName(newFirstName string) {
	(*pointerToPerson).firstName = newFirstName
    }

    *person: This is a type description - it means we're working with a pointer to a pointer.
    (*pointerToPerson): This is an operator - it means we want to manipulate the value to the pointer is referencing.

- Turn address into value: *address
- Turn value into address: &value

Options:
    jimPointer := &jim
    jimPointer.updateName(newFileName)
    Type of *person

    or 

    jim.updateName(newFileName)
    Type of person

    func (pointerToPerson *person) updateName()

Go is pass by value, but using pointer we can use pass by reference

https:play.golang.org


