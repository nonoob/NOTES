```scala
// v1:String="is this"
def v1: String = {
  val g = () => { return "is this" }
  g()                               
  "not this"
}
// v2:String="is this"
def v2: String = {         
  def g(): String = { return "not this" }
  g()
  "is this"
}
//cannot compile,complains "return outside method definition"
val v3: String = {         
  def g(): String = { return "error here" }
  g()
  "oops!"
}

//function types
def m1(x:Int)=x+3    //method
val funFromMethod = m1 _    //method value
var funFromLambda = new Function1[Int, Int] {def apply(x: Int): Int = x + 1} //anonymous function, can be also written as (x:Int)=>x+1
```

[Tips](http://stackoverflow.com/questions/6951895/what-does-and-mean-in-scala/6952195#6952195):
`=>` has several meanings in Scala, all related to its mathematical meaning as implication.

* In a value, it introduces a function literal, or *lambda*.  e.g. the bit inside the curly braces in `List(1,2,3).map { (x: Int) => x * 2 }` 

* In a type, with symbols on both sides of the arrow (e.g. `A => T`, `(A,B) => T`, `(A,B,C) => T`, etc.) it's sugar for `Function<n>[A[,B,...],T]`, that is, a function that takes parameters of type `A[,B...]`, and returns a value of type `T`.  
 * Empty parens on the left hand side (e.g. `() => T`) indicate that the function takes no parameters (also sometimes called a "thunk");

 * Empty parens on the right hand side denote that it returns `()`&mdash;the sole value of type `Unit`, whose name can also be written `()`&mdash;confused yet? :)  

      A function that returns Unit is also known as a *procedure*, normally a method that's called only for its side effect.


* In the type declaration for a method or function parameter, with no symbol on the left hand side (e.g. `def f(param: => T)`) it's a "by-name parameter", meaning that is evaluated every time it's used within the body of the function, and not before.  Ordinary "by-value" parameters are evaluated before entry into the function/method.

* In a `case` clause, they separate the pattern (and optional guard) from the result expression, e.g. `case x => y`.