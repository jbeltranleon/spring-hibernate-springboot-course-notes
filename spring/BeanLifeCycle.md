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

---

> For "prototype" scoped beans, Spring does not call the destroy method.  Gasp!  


In contrast to the other scopes, Spring does not manage the complete lifecycle of a prototype bean: the container instantiates, configures, and otherwise assembles a prototype object, and hands it to the client, with no further record of that prototype instance.

Thus, although initialization lifecycle callback methods are called on all objects regardless of scope, in the case of prototypes, configured destruction lifecycle callbacks are not called. The client code must clean up prototype-scoped objects and release expensive resources that the prototype bean(s) are holding. 


