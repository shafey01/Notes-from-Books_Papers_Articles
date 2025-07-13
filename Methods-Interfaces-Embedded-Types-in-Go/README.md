Tags: [[Articles]], [[GO]], [[Bill Kennedy]]

**Methods**  
Go has both functions and methods. In Go, a method is a function that is declared with a [receiver](http://golang.org/ref/spec#Method_declarations). A receiver is a value or a pointer of a [named](http://golang.org/ref/spec#Types) or [struct](http://golang.org/ref/spec#Struct_types) type. All the methods for a given type belong to the type’s method set.
```
type User struct {  
    Name string  
    Email string  
}  
  
func (u User) Notify() error

// Value of type User can be used to call the method  
// with a value receiver.  
bill := User{"Bill", "bill@email.com"}  
bill.Notify()  
  
// Pointer of type User can also be used to call a method  
// with a value receiver.  
jill := &User{"Jill", "jill@email.com"}  
jill.Notify()
```
In the case where we are using a pointer, Go [adjusts](http://golang.org/ref/spec#Calls) and dereferences the pointer so the call can be made.

---

**Interfaces**  
[Interfaces](http://golang.org/doc/effective_go.html#interfaces) in Go are special and provide an incredible amount of flexibility and abstraction for our programs. They are a way of specifying that values and pointers of a particular type can behave in a specific way. From a language perspective, an interface is a type that specifies a [method set](http://golang.org/ref/spec#Method_sets) and all the methods for an [interface type](http://golang.org/ref/spec#Interface_types) are considered to be the interface.

- It is a [convention](http://golang.org/doc/effective_go.html#interface-names) in Go to name interfaces with an -er suffix when the interface contains only one method.
- Go does not require us to explicitly state that our types implement an interface.

Here are the rules in the spec for how the compiler determines if the value or pointer for our type [implements](http://golang.org/ref/spec#Method_sets) the interface:  

- _The method set of the corresponding pointer type *T is the set of all methods with receiver *T or T_

This rule is stating that if the interface variable we are using to call a particular interface method contains a pointer, then methods with receivers based on both values and pointers will satisfy the interface. This rule does not apply for our example because we are passing a value to the SendNotification function.  

- _The method set of any other type T consists of all methods with receiver type T._

This rule is stating that if the interface variable we are using to call a particular interface method contains a value, then only methods with receivers based on values will satisfy the interface. This rule does not apply for our example because the receiver for the Notify method accepts a pointer.  
  
Since those are the only two rules in the spec for interface compliance, I have derived this rule that applies to our example:  

- _The method set of the corresponding type T **does not** consists of any methods with receiver type *T._
---
**Embedded Types**  
[Struct types](http://golang.org/ref/spec#Struct_types) have the ability to contain anonymous or embedded fields. This is also called embedding a type. When we embed a type into a struct, the name of the type acts as the field name for what is then an embedded field.

_"When we [embed](http://golang.org/doc/effective_go.html#embedding) a type, the methods of that type become methods of the outer type, but when they are invoked, the receiver of the method is the inner type, not the outer one." - Effective Go_

These are the rules for inner type [method set promotion](http://golang.org/ref/spec#Method_sets) in Go:  
  
_Given a struct type S and a type named T, promoted methods are included in the method set of the struct as follows:_  

- _If S contains an anonymous field T, the method sets of S and *S both include promoted methods with receiver T._

This rule is stating that when we embed a type, methods for the embedded type with receivers that use a value are promoted and available for calling by values and pointers of the outer type.  

- _The method set of *S also includes promoted methods with receiver *T._

This rule is stating that when we embed a type, methods for the embedded type with receivers that use a pointer are promoted and available for calling by pointers of the outer type.  

- _If S contains an anonymous field *T, the method sets of S and *S both include promoted methods with receiver T or *T._

This rule is stating that when we embed a pointer of the type, methods for the embedded type with receivers that use both values and pointers are promoted and available for calling by values and pointers of the outer type.  
  
Since those are the only three rules in the spec for method promotion, I have derived this rule for one other case:  

- _If S contains an anonymous field T, the method set of S **does not** include promoted methods with receiver *T._

This rule is stating that when we embed a type, methods for the embedded type with receivers that use a pointer are not promoted for calling by values of the outer type. This is consistent with the rules for interface compliance that we stated above.

---
- Would the compiler throw an error because we now had two implementations of the interface?

No, because when we use an embedded type, the unqualified type’s name acts as the field name. This has the effect of fields and methods of the embedded type having a unique name as an inner type of the struct. So we can have an inner and outer implementation of the same interface with each implementation being unique and accessible.  

- If the compiler accepted the type declaration, how does the compiler determine which implementation to use for interface calls?

If the outer type contains an implementation that satisfies the interface, it will be used. Otherwise, thanks to method promotion, any inner type that implements the interface can be used through the outer type.


