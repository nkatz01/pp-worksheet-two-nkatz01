# Programming Paradigms - Worksheet Two

Guess what?!?  
We will be continuing with some exercises from the <https://www.scala-exercises.org> site.

1. Got to the site.
2. Login with your nice new shiny `GitHub` account.
3. Follow the [`Scala Tutorial`][tut] path (click on the `Start` button) - just in case you had forgotten.

For this week you should complete the following exercises:

+ `Tail Recursion`,
def factorial(n: Int): Int = {
  @tailrec
  def iter(x: Int, result: Int): Int =
    if (x == 
0
) result
    else iter(x - 
1
, result * x)

  iter(n, 
1
)
}

factorial(3) shouldBe 6
factorial(4) shouldBe 24

+ `Structuring Information`,

case class Note(name: String, duration: String, octave: Int)
val c3 = Note("C", "Quarter", 3)
c3.name shouldBe "C"
c3.duration shouldBe 
"Quarter"

c3.octave shouldBe 
3

EQUALS

case class Note(name: String, duration: String, octave: Int)
val c3 = Note("C", "Quarter", 3)
val otherC3 = Note("C", "Quarter", 3)
val f3 = Note("F", "Quarter", 3)
(c3 == otherC3) shouldBe 
true

(c3 == f3) shouldBe 
false

sealed trait Duration
case object Whole extends Duration
case object Half extends Duration
case object Quarter extends Duration

def fractionOfWhole(duration: Duration): Double =
  duration match {
    case Whole => 1.0
    case Half => 
0.5

    case Quarter => 
0.25

  }

fractionOfWhole(Half) shouldBe 0.5
fractionOfWhole(Quarter) shouldBe 0.25

+ `Higher Order Functions`, 

def sum(f: Int => Int, a: Int, b: Int): Int = {
  def loop(x: Int, acc: Int): Int =
    if (x > b) acc
    else loop(x + 
1
, acc + f(x))
  loop(a, 
0
)
}
sum(x => x, 1, 10) shouldBe 55


+ `Standard Library`.

val cond: (Int, Int) => Boolean = 
(x,y) => (x<y)

def insert(x: Int, xs: List[Int]): List[Int] =
  xs match {
    case List() => x :: 
List()

    case y :: ys =>
      if (cond(x, y)) x :: y :: ys
      else y :: insert(x, ys)
  }
insert(2, 1 :: 3 :: Nil) shouldBe (1 :: 2 :: 3 :: Nil)
insert(1, 2 :: 3 :: Nil) shouldBe (1 :: 2 :: 3 :: Nil)
insert(3, 1 :: 2 :: Nil) shouldBe (1 :: 2 :: 3 :: Nil)

Common Operations on Options
Transform an optional value with map:

Some(1).map(x => x + 1) shouldBe Some(2)
None.map((x: Int) => x + 1) shouldBe None
Option(2)
.map(x => x + 1) shouldBe 
Option(3)
Filter values with filter:

Some(1).filter(x => x % 2 == 0) shouldBe None
Some(2).filter(x => x % 2 == 0) shouldBe Some(2)
Option(4)
.filter(x => x % 2 == 0) shouldBe 
Option(4)
Use flatMap to transform a successful value into an optional value:

Some(1).flatMap(x => Some(x + 1)) shouldBe Some(2)
None.flatMap((x: Int) => Some(x + 1)) shouldBe None
Option(1)
.flatMap(x => Some(x + 1)) shouldBe 
Option(2)

def triple(x: Int): Int = 3 * x

def tripleEither(x: Either[String, Int]): Either[String, Int] =
  x.right.map(triple)

tripleEither(Right(1)) shouldBe 
Right(3)

tripleEither(Left("not a number")) shouldBe 
Left("not a number")


[tut]: https://www.scala-exercises.org/scala_tutorial/terms_and_types
