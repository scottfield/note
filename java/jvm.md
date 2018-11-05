###Data Types
####integral types
- byte(8 bit signed integers default value is zero),value range [-128,127]
- short(16 bit signed integers default value is zero),value range [-32768,32767]
- int(32 bit signed integers default value is zero),value range [-2147483648,2147483647]
- long(64 bit signed integers default value is zero),value range [-9223372036854775808,9223372036854775807]
- char(16 bit unsigned integers representing unicode code point encoded with UTF-16 default value is'\u0000'),value range[0,65535]
####float-point types
- float(32 bit elements of the float value set default value is positive zero)
- double(64 bit elements of the float value set default value is positive zero)
####boolean type
- boolean (true or false default value is false),no opcode dedicated for boolean type, the compiler will map it to int type
####returnAddress type
- values are are pointers to the opcodes of Java Virtual Machine instructions.
####reference type
- class types(values are class instances)
- array types(values are array consists of a component type with a single dimension)
- interface types (values are class instances or arrays that implement interfaces)

###run time data area
####pc register
#### jvm stack
####native method stack
####heap
####method area(logically part of heap but not necessary)
It stores per-class structures such as the run-time constant pool,
field and method data, and the code for methods and constructors, including
the special methods used in class and instance initialization and interface
initialization.
- Run-Time Constant Pool(values ranging from numeric literals known at compile-time to method and field references that must be resolved at run-time)
####frame
- local variables
- operand stack
- a reference to the runtime constant pool of the class of the current method

####opcode
opcode mnemonic by a letter: i for an int operation, l for long, s for short,
b for byte, c for char, f for float, d for double, and a for reference.