# Bean LifeCycle - Hooks

* You can add custom code during bean initialization

	* Calling custon business logic methods
	* Setting up handles to resources (db, sockets, file ...)

* You can add custon code during bean destruction

	* Calling custon business logic methods
	* Clean up handles to resources (db, sockets, file ...)


***

> Special Note about init and destroy Method Signatures

When using XML configuration, I want to provide additional details regarding the method signatures of the init-method  and destroy-method .

**Access modifier**
The method can have any access modifier (public, protected, private)

**Return type**
The method can have any return type. However, "void' is most commonly used. If you give a return type just note that you will not be able to capture the return value. As a result, "void" is commonly used.

**Method name**
The method can have any method name.

**Arguments**
The method can not accept any arguments. The method should be no-arg.


