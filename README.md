## Why you should avoid package objects under `test/`

If there is a package object defined with the same name in both `test/` and `main/`, you DON'T get an error during compile time, but a confusing `java.lang.NoSuchMethodError` during the test run.

```
sbt:package-object-in-test> test
[info] Compiling 2 Scala sources to /dev/shm/package-object-in-test/target/scala-2.13/classes ...
[info] Compiling 2 Scala sources to /dev/shm/package-object-in-test/target/scala-2.13/test-classes ...
[info] HelloSpec:
[info] The Hello object
[info] example.HelloSpec *** ABORTED ***
[info]   java.lang.NoSuchMethodError: example.package$.hello()Ljava/lang/String;
[info]   at example.Hello$.<clinit>(Hello.scala:4)
[info]   at example.HelloSpec.$anonfun$new$1(HelloSpec.scala:8)
[info]   at org.scalatest.OutcomeOf.outcomeOf(OutcomeOf.scala:85)
[info]   at org.scalatest.OutcomeOf.outcomeOf$(OutcomeOf.scala:83)
[info]   at org.scalatest.OutcomeOf$.outcomeOf(OutcomeOf.scala:104)
[info]   at org.scalatest.Transformer.apply(Transformer.scala:22)
[info]   at org.scalatest.Transformer.apply(Transformer.scala:20)
[info]   at org.scalatest.flatspec.AnyFlatSpecLike$$anon$5.apply(AnyFlatSpecLike.scala:1683)
[info]   at org.scalatest.TestSuite.withFixture(TestSuite.scala:196)
[info]   at org.scalatest.TestSuite.withFixture$(TestSuite.scala:195)
[info]   ...
[error] stack trace is suppressed; run last Test / executeTests for the full output
[error] (Test / executeTests) java.lang.NoSuchMethodError: example.package$.hello()Ljava/lang/String;
[error] Total time: 3 s, completed May 7, 2020 6:42:42 PM
```
