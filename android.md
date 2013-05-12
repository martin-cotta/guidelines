## Android Code Style Guidelines

Current [Java coding conventions][1], plus:

* **Don't Ignore Exceptions**, alternatives (in order of preference) are:
    - Throw the exception up to the caller of your method  
    - Throw a new exception that's appropriate to your level of abstraction  
    - Handle the error gracefully and substitute an appropriate value in the catch {} block  
    - Catch the Exception and throw a new RuntimeException. only do it if you are positive that if this error occurs, the appropriate thing to do is crash  
    - Last resort: if you are confident that actually ignoring the exception is appropriate then you may ignore it, but you must also comment why with a good reason
    
* **Don't Catch Generic Exception**, alternatives to catching generic Exception:
    - Catch each exception separately as separate catch blocks after a single try
    - Refactor your code to have more fine-grained error handling, with multiple try blocks
    - Rethrow the exception
* **Don't Use Finalizers**  
In most cases, you can do what you need from a finalizer with good exception handling.

* **Fully Qualify Imports**  
Do this: `import foo.Bar;` instead of this: `import foo.*;`

* **Use Javadoc Standard Comments**  
Every class and nontrivial public method you write must contain a Javadoc comment with at least one sentence describing what the class or method does.

* **Write Short Methods**  
If a method exceeds 40 lines or so, think about whether it can be broken up without harming the structure of the program.

* **Define Fields in Standard Places**  
fields should be defined either at the top of the file, or immediately before the methods that use them.

* **Limit Variable Scope**  
The scope of local variables should be kept to a minimum. By doing so, you increase the readability and maintainability of your code and reduce the likelihood of error.  
Local variables should be declared at the point they are first used. Nearly every local variable declaration should contain an initializer. If you don't yet have enough information to initialize a variable sensibly, you should postpone the declaration until you do.

* **Order Import Statements** ([android.importorder][2])
    - Android imports
    - Imports from third parties (com, junit, net, org)
    - java and javax
    
* **Use Spaces for Indentation**  
    * Use 4 space indents for blocks. Never use tabs.  
    * 8 space indents for line wraps, including function calls and assignments.
    
* **Field Naming Conventions**
    - Non-public, non-static field names start with m.
    - Static field names start with s.
    - Other fields start with a lower case letter.
    - Public static final fields (constants) are ALL_CAPS_WITH_UNDERSCORES.
    
* **Use Standard Brace Style**  
Braces do not go on their own line; they go on the same line as the code before them.

* **Limit Line Length**  
Each line of text in your code should be at most 100 characters long.

* **Use Standard Java Annotations**  
Annotations should precede other modifiers for the same language element. Simple marker annotations (e.g. @Override) can be listed on the same line with the language element. If there are multiple annotations, or parameterized annotations, they should each be listed one-per-line in alphabetical order.

* **Treat Acronyms as Words**  
Treat acronyms and abbreviations as words in naming variables, methods, and classes.

* **Use TODO Comments**  
Use TODO comments for code that is temporary, a short-term solution, or good-enough but not perfect.
TODOs should include the string TODO in all caps, followed by a colon: 
`// TODO: Remove this code after the UrlTable2 has been checked in`

* **Log Sparingly**  
While logging is necessary it has a significantly negative impact on performance and quickly loses its usefulness if it's not kept reasonably terse.

* **Be Consistent**  
The point of having style guidelines is to have a common vocabulary of coding, so people can concentrate on what you're saying, rather than on how you're saying it. We present global style rules here so people know the vocabulary. But local style is also important. If code you add to a a file looks drastically different from the existing code around it, it throws readers out of their rhythm when they go to read it.

[Android Code Style Guidelines for Contributors](http://source.android.com/source/code-style.html)

[1]: http://www.oracle.com/technetwork/java/codeconv-138413.html "Code Conventions for the Java Programming Language"
[2]: https://github.com/android/platform_development/blob/master/ide/eclipse/android.importorder "platform_development / ide / eclipse / android.importorder"
