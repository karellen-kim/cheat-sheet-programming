# Scala Cheat Sheet

## Json
#### [circe](https://circe.github.io/circe/)
```scala
import io.circe._, io.circe.generic.auto._, io.circe.parser._, io.circe.syntax._

val encodeJson = foo.asJson.noSpaces
val decodedJson = decode[Foo](json)
```

## shapeless
#### Generic
```scala
import shapeless.Generic

val fromGen = Generic[From] // ("name", "address")
val toGen = Generic[To] // ("name", 20, "address")

val fromDatas = fromGen.to(from)
val to = toGen.from(fromDatas.head :: 20 :: fromDatas.tail.tail)
```
#### Coproducts
```scala
type ISB = Int :+: String :+: Boolean :+: CNil

val isb = Coproduct[ISB]("foo")
isb.select[Int] // None
isb.select[String] // Some(foo)
```
#### Coproducts match 
```scala
type ISB = Int :+: String :+: Boolean :+: CNil

val isb1 = Coproduct[ISB]("foo")
isb1.reverse = "oof"
val isb2 = Coproduct[ISB](true)
isb2.reverse = false


implicit class ISBSyntax[A](a: A) {
  def reverse(implicit helper: ReverseISB[A]): A = helper.reverse(a)
}

implicit val stringReverse = new ReverseISB[String] {
  override def reverse(a: String): A = a.reverse
}
implicit val intReverse = new ReverseISB[Int] {
  override def reverse(a: Int): A = a * -1
}
implicit val booleanReverse = new ReverseISB[Boolean] {
  override def reverse(a: Boolean): A = !a
}
implicit val deriveCNil = new ReverseISB[CNil] {
  override def reverse(a: CNil) = throw new Exception("Can't reach hear!")
}
implicit def deriveCCons[H, T <: Coproduct](implicit H: Lazy[ReverseISB[H]], T: Lazy[ReverseISB[T]]) =
  new ReverseISB[H :+: T] {
    override def reverse(a: H :+: T): A = a match {
      case Inl(l) => H.value.reverse(l)
      case Inr(t) => T.value.reverse(t)
    }
  }
```
#### Get case class field names
```scala
import shapeless._, record._, ops.record._

case class Foo(bar: String, baz: Boolean)
val labl = LabelledGeneric[Foo]
val keys = Keys[labl.Repr].apply

println(keys.toList.map(_.name))
```
#### Get case class field names and values
```scala
object keysToString extends Poly1 {
  implicit def keyToName[A, B] = at[(Symbol with A, B)] { case (k, v) => (k.name, v) }
}
case class Foo(bar: String, baz: Boolean)
val valuesWithLabel = LabelledGeneric[Foo].to(Foo("bar", true)).fields.map(keysToString)

print(valuesWithLabel)
```

## Akka
#### RabbitMQ : dead letter subscribe
```scala
class DeadLetterMonitorActor() extends Actor {
  def receive = {
    case DeadLetter(message, snd, rcp) =>
      val origin = if (snd eq context.system.deadLetters) "without sender" else s"from $snd"
    case _ => println("DeadLetterMonitorActor : got an unexpected message")
  }
}

val deadLetterMonitorActor = actorSystem.actorOf(Props(classOf[DeadLetterMonitorActor]), "deadlettermonitoractor")
actorSystem.eventStream.subscribe(deadLetterMonitorActor, classOf[DeadLetter])
```
