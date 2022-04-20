# Rxjava

## 基本概念

### 观察者与被观察者（Observable & Observer）

### Map FlatMap

### subscribeOn observerOn

### subscribe(Observer observer)

### timeout

## 一些FAQ

### 背压

一般可以：

- 过滤（抛弃）
- 缓存

### Rxjava的使用是否会导致内存泄漏？

比较经典的场景是在Observer中持有了其他生命周期对象导致的内存泄漏，比如：
```kotlin
class SamplePresenter{
    private var view : SampleView? = null

    // register impl
    fun initView(view: SampleView){
        this.view = view
    }

    fun subscribe(){
        ..subscrible(object: Observer<String>{
            override fun onNext(str: String){
                //持有了view对象
                view.doSomeThing(str)
            }
        })
    }
}
```
一般认为增加RxLifeCycle组件或者使用Compositedisposable就可以避免这个问题，
但实际上并不能根本解决。

原因在于上述方法是通过以下两个途径达到解绑操作的：

- 上游通知下游不再发送消息（onComplete）
- 下游通知上游不再接收消息（dispose）

并没有解决掉rxjava的comsumer中持有外部对象的引用问题
所以这里应该在subsucribe前增加

```kotlin
.onTerminateDetach()
```
