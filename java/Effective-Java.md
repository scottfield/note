- Prefer Static factory method to Constructor

  advantages:
    - One advantage of static factory methods is that, unlike
      constructors, they have names.
    - A second advantage of static factory methods is that,
      unlike constructors, they are not required to create a new
      object each time they’re invoked.
    - A third advantage of static factory methods is that, unlike
      constructors, they can return an object of any subtype of
      their return type.
    - A fourth advantage of static factories is that the class of
     the returned object can vary from call to call as a function
     of the input parameters.
    - A fifth advantage of static factories is that the class of the
      returned object need not exist when the class containing
      the method is written.
  
  drawbacks:
    - The main limitation of providing only static factory
      methods is that classes without public or protected
      constructors cannot be subclassed
     - A second shortcoming of static factory methods is that
       they are hard for programmers to find. 

- consider a builder when faced with many constructor parameters

  some alternative method:
  
   - telescoping constructor
   
      drawbacks:
      - hard to read and write when there are many parameters
   - java beans pattern
      
      drawbacks:
      - a JavaBean may be in an inconsistent state partway through its construction
      - cannot make a immutable class

- enforce the singleton property with a private constructor or an enum type
- enforce noninstantiability with a private constructor
- prefer dependency injection to hardwiring resources
- avoid creating unnecessary objects
- eliminate obsolete object references
- avoid finalizers and cleaners

  drawbacks:
  
  - there is no guarantee they’ll be executed promptly

- prefer try-with-resources to try-finally
- obey the general contract when overriding equals

   when should not override equals:
   
   - Each instance of the class is inherently unique.
   - There is no need for the class to provide a “logical
     equality” test.
   - A superclass has already overridden equals, and the superclass behavior is appropriate for this class.
   - The class is private or package-private, and you are certain that its equals method will never be invoked.
   
   the generic contract:
   
   - Reflexive: For any non-null reference value x, x.equals(x) must
     return true.
   - Symmetric: For any non-null reference
     values x and y, x.equals(y) must return true if and only
     if y.equals(x) returns true.
   - Transitive: For any non-null reference values x, y, z,
     if x.equals(y) returns true and y.equals(z) returns true,
     then x.equals(z) must return true.
   - Consistent: For any non-null reference values x and y, multiple
     invocations of x.equals(y) must consistently return true or
     consistently return false, provided no information used
     in equals comparisons is modified
   - For any non-null reference value x, x.equals(null) must return false

- always override hashcode when you override equals
- always override tostring
- override clone judiciously
- consider implementing comparable

   note:
     - there is no way to
       extend an instantiable class with a new value component while
       preserving the compareTo contract, unless you are willing to forgo
       the benefits of object-oriented abstraction
     - When comparing field values in the implementations of
       the compareTo methods, avoid the use of the < and > operators.
       Instead, use the static compare methods in the boxed primitive
       classes or the comparator construction methods in
       the Comparator interface.
- minimize the accessibility of classes and members
