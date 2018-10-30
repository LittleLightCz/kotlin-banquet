# kotlin-banquet
My personal set of extension functions that I like to use, which are missing in Kotlin or in my favourite libraries.

Making this a standalone library would be too much :relaxed:, so please take a seat and copy-paste whatever you need.

## Coroutines
```kotlin
object UI : CoroutineScope {
    override val coroutineContext = Dispatchers.JavaFx
}

object IO : CoroutineScope {
    override val coroutineContext = Dispatchers.IO
}

operator fun CoroutineScope.invoke(block: suspend CoroutineScope.() -> Unit) = launch(block = block)

suspend fun <T> offload(block: suspend CoroutineScope.() -> T) = withContext(Dispatchers.IO, block = block)
```

## Kotlin stdlib
```kotlin
public inline fun <T> Collection<T>.randomOrNull(): T? {
    return takeIf { it.isNotEmpty() }?.random()
}
```

## TornadoFX
```kotlin
inline operator fun BooleanProperty.invoke(block: () -> Unit) {
    set(true)
    try {
        block()
    } finally {
        set(false)
    }
}
```
