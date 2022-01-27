# Flutter异常上报与异常处理

最近在做Flutter异常处理相关的问题，发现Flutter官方推荐的[异常处理流程](https://book.flutterchina.club/chapter2/thread_model_and_error_report.html#_2-8-2-flutter%E5%BC%82%E5%B8%B8%E6%8D%95%E8%8E%B7)以及[上报文档](https://docs.flutter.dev/cookbook/maintenance/error-reporting)并不能很好的满足需求。

原因是Flutter的Widget markNeedBuild和drawFrame流程是分开的，导致一些Widget中比较隐蔽的且会导致Framework流程出错的dart异常的stackTrace，只能显示出主流程，但并不能直接直接看出是哪个widget写的有问题。

吧啦吧啦一堆，反正就是stackTrace导致排障困难，降低Flutter学习性，因此考虑做个优化～

## Flutter ErrorHandler

Flutter在build阶段处理