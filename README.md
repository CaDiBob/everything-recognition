# Раcпознования лица с помощью Python

### Скрипт run.py

Скрипт использует библиотеку [opencv](https://docs.opencv.org/4.x/d6/d00/tutorial_py_root.html) котороя в свою очередь использует [каскады Хаара](https://ru.wikipedia.org/wiki/%D0%9F%D1%80%D0%B8%D0%B7%D0%BD%D0%B0%D0%BA%D0%B8_%D0%A5%D0%B0%D0%B0%D1%80%D0%B0) харанятся в корне скрипта в папке `haarcascades`, и веб-камеру для распознования лица пользователя.
При запуске скрипта также запускается Web-камера.
Послезапуска распознает Лицо, улыбку, глаза, профиль, фас и анфас дополнительно может распозновать мордочки кошек.
**Вимание!!! Скрипт сильно нагружает систему не рекомендуятся к использованию на слабых пк и ноутбуках!!!**

Некоторые камеры не поддерживаются по умолчанию. Вы можите самотоятельно сменить id вашего устройсва в скрипте, сменив параметр `cv2.VideoCapture(0)` тут:

```Python
if __name__ == "__main__":
    cascades = get_cascades()
    video_capture = cv2.VideoCapture(0)
    while True:
        if not video_capture.isOpened():
            print("Couldn't find your webcam... Sorry :c")
        _, webcam_frame = video_capture.read()
        gray_frame = cv2.cvtColor(webcam_frame, cv2.COLOR_BGR2GRAY)
        for cascade, color in cascades:
            captures = [cascade.detectMultiScale(
                gray_frame,
                scaleFactor=1.1,
                minNeighbors=10,
                minSize=(30, 30)
            )]
            for capture in captures:
                for (x, y, w, h) in capture:
                    draw_sqare(webcam_frame, color)
        show_frame(webcam_frame)

        if is_user_wants_quit():
            break
    video_capture.release()
    cv2.destroyAllWindows()

```

Распознаные части лица на экране выделяются квадратами.

### Скрипт config.py

Тут находится словарь с путями к [каскадам Хаара](https://ru.wikipedia.org/wiki/%D0%9F%D1%80%D0%B8%D0%B7%D0%BD%D0%B0%D0%BA%D0%B8_%D0%A5%D0%B0%D0%B0%D1%80%D0%B0)

### Как использовать

Поддерживате все версии `Python от 2.7 до 3.10`.

В файл `requirements.txt` указана устаревшая версия `opencv-python==3.4.3.18` ее нет в официальных репозиториях, можно использовать любую верси старше.

Затем используйте `pip или pip3`
```bash
$ pip install opencv-python
```
или

```bash
$ sudo apt install python3-opencv
```

##### Запуск

```bash
$ python run.py
```