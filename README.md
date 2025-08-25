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

    swipe.OnTap += () => Debug.Log("👆 Tap");
    swipe.OnDoubleTap += () => Debug.Log("✨ Double Tap!");
    swipe.OnLongPress += () => Debug.Log("⏱ Long Press!");
    swipe.OnSwipeLeft += () => Debug.Log("⬅️ Swipe Left");
    swipe.OnPinch += scale => Debug.Log($"🔍 Pinch: {scale}");
    swipe.OnRotate += angle => Debug.Log($"↻ Rotate: {angle}");
}
```
