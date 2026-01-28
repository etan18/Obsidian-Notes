**VTables**, or *virtual tables*, are arrays of virtual memory. In C++, VTables store pointers to all member functions of a particular class. Storing function pointers this way is what enables C++ to have **polymorphism**.

> [!hot] Polymorphism
> Polymorphism is a principle of object-oriented programming that allows for interfaces to implement functions differently. Some ways to implement polymorphism include
> 		- Creating function definitions with the same name, but accepting different arguments
> 		- Creating function definitions with the same name in different contexts

To execute a function from the VTable, dereference the pointer with an offset to get the address of the function.




