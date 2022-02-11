# Tutorial

:project Урок: Создание игры

## Прыжок!

:position 50,50,40,40

### Прыжок!

Нам нужно, чтобы наш герой прыгал по нажатию или щелчку мыши на экране. Прыжок означает приобретение некоторой вертикальной скорости, которая будет влиять на вертикальное положение героя. Вертикальная скорость скорость будет зависеть от гравитации.

## Прыжок!

### Прыжок!

Давайте выберем переменную ``hero_y`` в качестве вертикальной позиции героя и ``hero_vy`` в качестве вертикальной скорости героя.

``hero_y`` должна влиять на вертикальную позицию, в которой нарисован наш герой. Мы сделаем это, изменив следующую строку в теле нашей функции ``draw``:

```
  screen.drawSprite("hero", -80, -50+hero_y, 20)
```

Теперь на нашу вертикальную позицию должна влиять вертикальная скорость. Давайте смоделируем это в нашей функции ``update`` путем добавления:

```
  hero_y = hero_y + hero_vy
```

## Инициализация прыжка

### Инициализация прыжка

Нашими двумя условиями для выполнения прыжка являются:

1. Герой должен находиться на земле, таким образом ``hero_y == 0``.
2. Игрок касается экрана / удерживает кнопку мыши, что можно проверить с помощью ``touch.touching``.

Инициирование прыжка означает установку вертикальной скорости на некоторое положительное значение (вверх), например, ``hero_vy = 7``.

Добавим следующий код в тело функции ``update``:

```
  if touch.touching and hero_y == 0 then
    hero_vy = 7
  end
```

## Гравитация

### Гравитация

Теперь, когда вы заставляете своего героя прыгать, он пролетает сквозь потолок и исчезает очень быстро! Это потому, что мы еще не добавили гравитацию. Гравитация похожа на ускорение вниз. Каждый короткий промежуток времени она уменьшает нашу вертикальную скорость на фиксированную величину. Давайте добавим следующую строку в тело функции ``update``:

```
  hero_vy = hero_vy - 0.3
```

Довольно быстро наш герой упадет... и провалится сквозь землю. Нам нужно предотвратить это, изменив эту строку:

```
  hero_y = hero_y + hero_vy
```

на

```
  hero_y = max(0, hero_y+hero_vy)
```

Теперь мы просто убеждаемся, что вертикальное положение нашего героя не может быть ниже нуля.

## Конец

### Конец

В следующем коротком руководстве мы добавим препятствия, которые наш герой должен будет избегать, перепрыгивая через них.
Ниже приведен наш полный текущий код:

```
init = function()
end

update = function()
  position = position+2

  if touch.touching and hero_y == 0 then
    hero_vy = 7
  end

  hero_vy = hero_vy - 0.3
  hero_y = max(0, hero_y+hero_vy)
end

draw = function()
  screen.clear("rgb(57, 0, 57)")

  for i=-6 to 6 by 1
    screen.drawSprite("wall", i*40-position%40, -80, 40)
  end

  screen.drawSprite("hero", -80, -50+hero_y, 20)
end
```