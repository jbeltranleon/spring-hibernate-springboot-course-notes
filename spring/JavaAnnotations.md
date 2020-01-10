# Java Annotations

* Special labels/markers added to Java classes
* Provide meta-data about the class
* Process at compile time or run-time for special processing  


## Some important annotations

### @PostConstruct

* FAQ: I'm getting null for the fortunes.

*Question*

When I create an array of fortunes using this

String[] data= {a,b,c,d,e};

The array is always null. Why?

*Answer*

The root cause is this is a Spring Bean Lifecycle issue.

When Spring creates the beans it follows this general process

1. Construct an instance of class
2. Inject dependencies
3. Set properties etc (**@Value**)

In your case, when you initialized the array using this code

    ```// create an array of strings
    private String[] data = { a, b, c, d, e };```

The Spring Bean lifecycle was at step #1 above. It created an instance ... but during the assigment of the string array, the properties/fields for a, b, c, d, e haven't been set yet using @Value. That doesn't happen later until step #3.  So that's why you had null with the field assignment.

When you made mods to your code and moved the assignment into the getFortune() method, then by the time this method is invoked all steps 1-3 are already complete and it works as desired.

---

For this use case, the recommended solution is to use the **@PostConstruct** annotation. This is called at the end of the bean lifecycle process. So all of steps 1-3 are already completed and then you can safely perform assignments. This is the best use case for making any custom assignments in your code.

Here's the updated code for your service. Make note of this section:

```
    private String[] data;
    
    @PostConstruct
    public void setupMyData() {
        
        data = new String[5];
        
        data[0] = a;
        data[1] = b;
        data[2] = c;
        data[3] = d;
        data[4] = e;
        
    }
```

### Scope

```
	@Component
	@Scope("prototype")
	public class TennisCoach implements Coach {
		...
	}		
```

### PreDestroy

Used to use a method before the bean is destroy

---

> Special Note about @PostConstruct and @PreDestroy Method Signatures

I want to provide additional details regarding the method signatures of @PostContruct and @PreDestroy methods.

Access modifier

The method can have any access modifier (public, protected, private)

* Return type
The method can have any return type. However, "void' is most commonly used. If you give a return type just note that you will not be able to capture the return value. As a result, "void" is commonly used.

* Method name
The method can have any method name.

* Arguments
The method can not accept any arguments. The method should be no-arg.


