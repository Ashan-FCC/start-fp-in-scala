**A tutorial for Functional programming in Scala**

This book is aimed to be the first place when you starting functional programming in Scala. Feedback and PR are welcome.

* [Setup](#setup)
   * [Install Java 8 JDK](#install-java-8-jdk)
   * [Install sbt](#install-sbt)
   * [Hello world with sbt](#hello-world-with-sbt)
   * [REPL](#repl)
* [Basics in Scala](#basics-in-scala)
   * [val vs var](#val-vs-var)
   * [Expression](#expression)
   * [Function](#function)
   * [Common data structure](#common-data-structure)
* [Practice REST API server with Scala](#practice-rest-api-server-with-scala)

[TOC]


## Setup

### Install Java 8 JDK
Open your favorite terminal, check installed Java version:
```shell
java -version
```
If it's not installed, download [here](http://www.oracle.com/technetwork/java/javase/downloads/index.html).

### Install sbt
For Mac OS users: 
```shell
brew install sbt
```

For Arch Linux users:

```shell
yay -S sbt
```

### Hello world with sbt 
Using sbt new command to create an simple project:
```shell
sbt new sbt/scala-seed.g8
```
Follow the prompt information, Input the project name to finish the setup:
```shell
A minimal Scala project.

name [Scala Seed Project]: scala-walk-through

Template applied in ./scala-walk-through
```

Now we have a basic project, check the directories structure:
```shell
ls -l scala-walk-through
total 8
-rw-r--r--  1 kcsun  staff  282 Jan  3 12:00 build.sbt
drwxr-xr-x  4 kcsun  staff  136 Jan  3 12:00 project
drwxr-xr-x  4 kcsun  staff  136 Jan  3 12:00 src
```
Let me explain the files:

* `build.sbt` - the project configuration file, it includes basic information for the project like project name, group name, scala version, dependencies, etc. 
* `project` - this folder contains the file
  * `build.properties` used to set sbt version
  * `plugins.sbt` used to define all the available plugins for the build
  * Other project settings you want to extract from the `build.sbt` to make the main file clean and tight.
* `src` - this folder maintains all the source code and test code. sbt has the same code structure style with Maven.  

Modify the source code in`src/main/scala/example/Hello.scala` to be:
```scala
lazy val greeting: String = "Hello, Functional Programming!"
```

Run your newest program with sbt command, you can use `sbt run` directly, or get into interactive mode with `sbt`, then execute `run`. You will get following output if you are lucky:

```shell
Hello, Functional Programming!
```

Exit sbt with ctrl + d or simply input `exit`。

### REPL
REPL (Read-Eval-Print Loop) is one of the most useful environments if you want to try a new programming language. There is a few options for Scala:
* sbt console - help us import the dependencies in the project, can be used directly in this way.

* amm - most efficient tool developed by [lihaoyi](https://github.com/lihaoyi), it has user friendly features like syntax highlight, multiple line input, etc. Install with following command:

  ```shell
  sudo curl -L -o /usr/local/bin/amm https://git.io/vdNv2 && sudo chmod +x /usr/local/bin/amm && amm
  ```

### IDE

[IntelliJ IDEA](https://www.jetbrains.com/idea/) - There is a free community version for idea. 

Open the IntelliJ IDEA, 

* go to **File -> New -> Project from existing sources**, choose the root folder of your project and open.
* select **sbt** under `Import project from external model`.
* select **Library sources** and choose the proper JDK version, fow now I use JDK 1.8.
* click **finish**, now after downloading all the dependencies, you should be able to get your project up. 

## Basic Knowledge in Scala

This section includes some basic concepts in Scala, like basic type (String, Int), data type (List, Option, Either), 

Most of code listed in this book can be run directly in REPL tools like amm.

### Basic type

Scala provides **nine** predefined basic or scalar type, they are:

* Boolean: `true`, `false`
* Int: `1`
* String: `"hello"`
* Unit: `()`
* Char: `c`
* Long: `100L`
* Short: `100: Short`
* Float: `31.4f`
* Double: `3.14d`

### Container type

Data type like `List[A]`, `Option[A]`, `Either[A]` etc, can be viewed as a container of basic type, the formal name in math is called [Higher Kinded Type](https://en.m.wikipedia.org/wiki/Kind_(type_theory)). 

**List:**

```
scala> List(1,2,3)
res0: List[Int] = List(1, 2, 3)

scala> 1 :: 2 :: 3 :: Nil
res1: List[Int] = List(1, 2, 3)
```

**Set:**

```
scala> Set(1, 1, 2)
res2: scala.collection.immutable.Set[Int] = Set(1, 2)
```

**Seq:**

```
scala> Seq(1,1,2)
res3: Seq[Int] = List(1, 1, 2)
```

**Map:**

```
scala> Map('a'->1, 'b'->2)
res4: res1: scala.collection.immutable.Map[Char,Int] = Map(a -> 1, b -> 2) 
```

**Stream:**  TODO

### Variable
通过val, 可以将表达式的结果赋值给一个常量，常量值不能改变。
```
scala> val three = 1 + 2
two: Int = 3
```

var定义的值为变量，可被修改。
```
scala> var name = "dasheng"
name: String = dasheng

scala> name = "kaichao"
name: String = kaichao
```

### Expression
Scala中几乎所有的语句都是表达式，就连`if else`、`patter match`也都是表达式。
expressions 总是返回结果，几乎不产生任何side effect；相反，statements 并不返回任何结果，仅仅为了获取side effect而执行。
EOP（expression-oriented programming）是函数式编程语言的共有特点，更多内容请参考[这里](https://alvinalexander.com/scala/best-practice-think-expression-oriented-programming-eop)。
通过EOP，代码变得：
* easy to reason about
* easy to test
* excute in parallel

```
scala> if (true) 1 else 0
res0: Int = 1

scala> "hp" match {
     |   case "hp" => "computer"
     |   case _ => "non-computer"
     | }
res1: String = computer
```

### Conditional Control



### Loop Control



### Function

[Functions vs Methods](http://jim-mcbeath.blogspot.com/2009/05/scala-functions-vs-methods.html)

### Traits



### Class & Objects



### Comment



## ELI5 - Category Theory

### What's Category Theory



### Object and Arrow



### Terminal Object



### Product Type



### Sum Type



### Kleisili Arrow



### Monoid



### Functor



### Monad

## Daily Libraries

### cats

常用的Monad

#### Id

```
import cats.{Id, Monad}
import cats.syntax.functor._ // for map
import cats.syntax.flatMap._ // for flatMap

val a = Monad[Id].pure(3)
// a: cats.Id[Int] = 3
val b = Monad[Id].flatMap(a)(_ + 1)
// b: cats.Id[Int] = 4

for {
  x <- a
  y <- b
} yield x + y
// res6: cats.Id[Int] = 7
```

#### Either

#### Eval

Eval有三个子类型，Now、Later和Always。

```
import cats.Eval

val now = Eval.now(1)
val later = Eval.later(2)
val always = Eval.always(3)
```

通过`value`方法进行取值。

Eval和Scala lazy的比较：

| scala    | cats   | properties         |
| -------- | ------ | ------------------ |
| val      | Now    | eager, memoized    |
| lazy val | Later  | lazy, memoized     |
| def      | Always | lazy, not memoized |

#### Writer

#### State

#### Customized Monad

通过实现flatMap, pure, tailRecM为一个自定义的类型提供Monad。

#### Monad transformer

Cats为很多Monad提供了transformer，以T结尾，如：EitherT是Either和其他Monad组合，OptionT组合Option和其他Monad。

#### Validated

- map, leftMap, bimap
- toEither
- withEither
- ensure

### cats-effect



### fs2



### circe



### http4s



### doobies



### monix



### specs2



### shapeless
Function1:
```scala
val f: A => B = ???
```

Natural Transformation:
```scala
val nat: F ~> G
or 
val nat: F[A] => G[A]
```

## Common Functionality

This section may not necessary.

### File Read / Write



### Common Calculation



### Http Request



## Use Cases

### Scala Web Server

* Setup a empty project with sbt.

  Resource: https://www.scala-sbt.org/1.0/docs/sbt-new-and-Templates.html

* Add http4s library and create a test API with response hello world.

  Resource: https://http4s.org/v0.18/service/

* Add model `Post(Int userId, Int id, String title, String body)` and create API to response a single Get post request as String. 

  Resource: https://docs.scala-lang.org/tour/case-classes.html

* Add circe library and make the previous response as JSON, example:

  ```json
  {
    "userId": 1,
    "postId": 1,
    "title": "sunt aut facere repellat provident occaecati excepturi optio reprehenderit",
    "body": "quia et suscipit\nsuscipit recusandae consequuntur expedita et cum\nreprehenderit molestiae ut ut quas totam\nnostrum rerum est autem sunt rem eveniet architecto"
  }
  ```

  Resource: https://circe.github.io/circe/codecs/custom-codecs.html

* Add library `http4s-blaze-client`, and call the endpoint to get post information `https://jsonplaceholder.typicode.com/posts/1`

  Resource: https://http4s.org/v0.18/client/

* Decode the previous response to `Post` model and return as API response.

  Resource: https://circe.github.io/circe/codecs/custom-codecs.html

### Big Data Process



### Web Crawler



### Machine Learning

TODO



### ScalaJS



## Other Knowledge

### Scala Type System: Parameterized Types and Variances

#### Why variance
Scala中集合是covariance，我们可以使用子类集合替换父类集合。例如，List[Circle]可以用于任意需要一个List[Shape]的地方，因为Circle是Shape的子类。

Contravariance, 当构造代表一些操作的类型时，十分有用。如JsonWriter type class:
```
trait Json
trait JsonWriter[-A] {
  def write(value: A): Json
}

val shape: Shape = ???
val circle: Circle = ???

val shapeWriter: JsonWriter[Shape] = ???
val circleWriter: JsonWriter[Circle] = ???

def format[A](value: A, writer: JsonWriter[A]): Json =
  writer.write(value)
```
JsonWriter[Shape]是JsonWriter[Circle]的子类，也就是所，任何使用shapeWriter的地方可以用circleWriter替换。
那么我们的circle就可以和任意一个writer结合使用。


## References
[1] https://blog.codecentric.de/en/2015/03/scala-type-system-parameterized-types-variances-part-1/