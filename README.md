# Unity---GestureController
# Описание GestureController и Singleton

## GestureController

**GestureController** - это универсальный контроллер жестов для Unity, поддерживающий различные типы жестов:
- Свайпы (влево, вправо, вверх, вниз)
- Тапы (одиночные и двойные)
- Долгие нажатия
- Перетаскивание (Drag)
- Масштабирование двумя пальцами (Pinch)
- Вращение двумя пальцами (Rotate)

### Ключевые особенности:
- Кросс-платформенная поддержка (мышь/тачскрин)
- Настраиваемые параметры (dead zones, timing)
- Событийная система для всех типов жестов
- Интеграция с системой Singleton

### Использование:
```csharp
// Подписка на события
GestureController.Instance.OnSwipeLeft += HandleSwipeLeft;
GestureController.Instance.OnPinch += HandlePinch;
```

``` cs
private void Start()
{
    var swipe = GestureController.Instance;

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
    var swipe = GestureController.Instance;

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
    var swipe = GestureController.Instance;

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
    GestureController.Instance.OnSwipe += dir => Debug.Log($"Свайп: {dir}");

    // Динамическое изменение DeadZone
    GestureController.Instance.DeadZone = 200f; 
}
```

``` cs
private void Start()
{
    GestureController.Instance.OnSwipeLeft += () => Debug.Log("Свайп влево");
    GestureController.Instance.OnSwipeRight += () => Debug.Log("Свайп вправо");
    GestureController.Instance.OnTap += () => Debug.Log("Тап!");
}
```

## Singleton

**Singleton** - это базовый класс для реализации шаблона Singleton в Unity с поддержкой:
- Потокобезопасной инициализации
- Автоматического создания экземпляров
- Защиты от дублирования объектов
- Сохранения между сценами (DontDestroyOnLoad)
- Корректной обработки завершения приложения

### Особенности реализации:
- Ленивая инициализация
- Интерфейс IInitialized для контроля инициализации
- Предотвращение ошибок при уничтожении объектов
- Логирование для отладки

Оба компонента предназначены для создания надежной системы управления вводом в Unity-приложениях с поддержкой мультитач-жестов.
