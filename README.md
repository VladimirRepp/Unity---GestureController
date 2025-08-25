# Unity---GestureController
Gesture Controller for touchscreen 

Универсальный GestureController, поддерживающий:
- Tap <br/>
- Double Tap <br/>
- Long Press <br/>
- Swipe (все варианты) <br/>
- Drag <br/>
- SwipeEnd <br/>
- Pinch <br/>
- Rotate <br/>

Примеры использования:
``` cs
private void Start()
{
    var swipe = SwipeInput.Instance;

    swipe.OnTap += () => Debug.Log("Tap");
    swipe.OnDoubleTap += () => Debug.Log("Double Tap!");
    swipe.OnLongPress += () => Debug.Log("Long Press!");
    swipe.OnSwipeLeft += () => Debug.Log("Swipe Left");
    swipe.OnPinch += scale => Debug.Log($"Pinch: {scale}");
    swipe.OnRotate += angle => Debug.Log($"Rotate: {angle}");
}
```

``` cs
private void Start()
{
    var swipe = SwipeInput.Instance;

    // Обычные свайпы
    swipe.OnSwipeLeft += () => Debug.Log("Swipe Left");
    swipe.OnSwipe += dir => Debug.Log($"Направление: {dir}");

    // Drag
    swipe.OnDrag += delta => Debug.Log($"Перетаскивание: {delta}");

    // Pinch (scale)
    swipe.OnPinch += scale =>
    {
        if (scale > 1) Debug.Log("Zoom In (+)");
        else Debug.Log("Zoom Out (-)");
    };

    // Rotate
    swipe.OnRotate += angle =>
    {
        if (angle > 0) Debug.Log($"Вращение по часовой: {angle}");
        else Debug.Log($"Вращение против часовой: {angle}");
    };

    // Свайп завершён
    swipe.OnSwipeEnd += () => Debug.Log("✅ Свайп завершён");
}
```

``` cs
private void Start()
{
    var swipe = SwipeInput.Instance;

    swipe.OnSwipeLeft += () => Debug.Log("Свайп влево");
    swipe.OnSwipeRight += () => Debug.Log("Свайп вправо");
    swipe.OnTap += () => Debug.Log("Тап");

    swipe.OnSwipe += dir => Debug.Log($"Направление: {dir}");
    swipe.OnSwipeRaw += delta => Debug.Log($"Полный вектор: {delta}");
    swipe.OnSwipeNormalized += dir => Debug.Log($"Нормализовано: {dir}");
    swipe.OnDrag += delta => Debug.Log($"Драг: {delta}");
    swipe.OnSwipeEnd += () => Debug.Log("Свайп завершён");

    // пример изменения чувствительности
    swipe.DeadZoneX = 100f;
    swipe.DeadZoneY = 200f;
}
```

``` cs
private void Start()
{
    // Подписка на события
    SwipeInput.Instance.OnSwipe += dir => Debug.Log($"Свайп: {dir}");

    // Динамическое изменение DeadZone
    SwipeInput.Instance.DeadZone = 200f; 
}
```

``` cs
private void Start()
{
    SwipeInput.Instance.OnSwipeLeft += () => Debug.Log("Свайп влево");
    SwipeInput.Instance.OnSwipeRight += () => Debug.Log("Свайп вправо");
    SwipeInput.Instance.OnTap += () => Debug.Log("Тап!");
}
```
