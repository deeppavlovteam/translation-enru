# Модуль общедоменного перевода русский-английский, английский-русский

Модуль общедоменного перевода представляет собой две модели, предобученные на выборке параллельных текстов датасета [OPUS](https://opus.nlpl.eu/). Модели тестировались на тестовой выборке русского и английского языков соревнования [The Tatoeba Translation Challenge (v2021-08-07)](https://github.com/Helsinki-NLP/Tatoeba-Challenge/blob/master/README-v2021-08-07.md).

## Установка

- Необходимо установить виртуальное окружение Python не ниже 3.7
- Для установка зависимостей необходимо запустить `pip install -r requirements.txt`
- Для запуска моделей необходимо использовать GPU, таким образом префиксом команд будет `CUDA_VISIBLE_DEVICES=i`, где `i` -- индекс свободной GPU.

## Дообучение

- Необходимо запустить скрипт `create_base_model.py`, который подгрузит базовую модель для дообучения.
- Запуск скрипта `tatoeba_train_enru.sh` вызовет режим обучения в направлении английский-русский со следующими параметрами:
  - Количество эпох: 10
  - Максимальная длина входной последовательности: 192
  - Максимальная длина выходной последовательности: 192
- Обученная модель будет сохраненна в папку `output_enru`
- Аналогично для пары русский-английский.

## Эвалюация

- Для того, чтобы получить оценки качества модели в направлении английский-русский необходимо запустить `run_evaluate_enru.sh`. В результате работы скрипта будет представлена статистика качества перевода на тестовой выборке датасета Tatoeba для соревнования The Tatoeba Translation Challenge (v2021-08-07).
- Аналогично для пары русский-английский `run_evaluate_ruen.sh`.

## Генерация

Для генерации переводов необходимо использовать скрипт `run_predict.py`. Скрипт генерирует последовательности на целевом языке на основе `txt` файла с текстовыми последовательностями на исходном языке. Скрипт использует следующие параметры:

- `direction` -- направление перевода, либо `enru`, либо `ruen`.
- `sentences_path` -- путь к файлу с последовательностями на исходном языке.
- `output_file` -- путь к файлу с последовательностями на целевом языке.
