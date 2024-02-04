# Детектор лебедей

## Установка и запуск приложения
Склонировать репозиторий в папку, в путь без пробелов и кириллицы

```shell
git clone https://github.com/LIvanoff/gusey-net
```

Установить все необходимые зависимости

```shell
cd gusey-net
pip install -r requirements.txt
```

Запуск приложения

```shell
python main.py
```

## Требования
<li> Python 3.9+

## Выбор архитектуры

При выборе модели была прочитана статья [**_A COMPREHENSIVE REVIEW OF YOLO: FROM YOLOV1 TO
YOLOV8 AND BEYOND_**](https://arxiv.org/pdf/2304.00501v1.pdf), в которой рассматриваются всё семейство архитектуры YOLO.
В конечном итоге выбор был сделан в пользу наиболее популярном и устоявшемся решении YOLOv5.

## Датасет

В качестве задаче был выбран датасет из 9000 фотографий лебедей, состоящий из 3 видов: шипун, кликун и малый лебедей.
На каждый тип лебедя по 3000 фотографий. На рисунке снизу можно наблюдать пример детекции шипуна.

## Обучение

Код обучение модели можно посмотреть в Jupter Notebook:
    [colab](https://github.com/LIvanoff/gus-detect/blob/master/notebook_yolov5.ipynb)
   [github](https://colab.research.google.com/gist/LIvanoff/6afc9bb8cea3801b40e76297effc4247/yolov5.ipynb)
Была обучена YOLOv5 всех размеров, включая YOLOv5x. Обучение всех версий производилось в течении 50 эпох на NVIDIA TESLA A100 40GB.

## Результаты

При обучении модели были получены результаты по метрике mIoU: 95 - 0.995 на обучающей выборке и 0.987 на отложенной. Помимо прочего 
дополнительно была посчитана метрика Accuracy, поскольку вероятность того, что на одной фотографии будут лебеди разных типов очень низка.
Были получены следующие результаты на модели YOLOv5 размеров nano, small, mdeium, large и extra. 

<p align="center">
  <img src="https://github.com/LIvanoff/gus-detect/blob/master/exp.png" width="560" alt="Experiments">
</p>
На основе полученных метрик был сделан выбор в пользую large версии, поскольку именно данная модель показала наилучший результат немного уступив Extra версии при Confidence: 90%.

## GUI

Для взаимодействия с обученной моделью был создан графический интерфейс при помощи библиотеки PyQT. Также для сохранения всех
результатов работы была создана локальная база данных при помощи SQLite. 


<p align="center">
  <img src="https://github.com/LIvanoff/gus-detect/blob/master/assets/gui.png"  alt="GUI">
</p>
