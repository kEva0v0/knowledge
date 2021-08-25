# Flutter Null Safety 与 包体积

> 内容源自 [Dart and the performance benefits of sound types](https://medium.com/dartlang/dart-and-the-performance-benefits-of-sound-types-6ceedd5b6cdc)

# Dart 1

> In Dart 1, however, static types weren’t sound and were effectively ignored during compilation. 

Dart 1使用的是不完全类型，即在编译时无法确定它的offset，这会导致它无法确认field的offset，因此将花大量的操作去获取正确的内容，或抛出异常。

>The access to age might be to a field at a different offset, to a getter that triggered further executable code, or to a non-existent field (triggering a catchable runtime error).

具体如何操作的还有待研究

# Dart 2

> With Dart 2, we introduced soundness, which enabled us to safely compile code based upon type information and reduced our reliance on profiling for performance.

Dart2使用的是完全类型（即编译期就确定的类型），这样就可以很轻松滴获取offset，进而获取正确的field, 但这部分依然需要进行null check

当然只要你不把变量声明为dynamic类型

# Dart 2.12

> With sound null safety, the type system is richer, and our compiler can leverage that. The compiler can safely rely upon the (now) non-nullable type 

Dart2.12去掉了编译期的null check（当然仅针对非空变量做），进一步减少了instruct code数量