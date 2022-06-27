# BrainHunt
    BrainHunt - это реализация инструмента brainflayer на языке Python. это простой и одновременно функциональный инструмент. 
    Функционал расширен если смотреть на источник. Программы производить хеширование в 3х алгоритмах (SHA256, SHA3, Keccak-256)
    После хеширования полученный хеш является private key, из полученного ключа создаются 3 HASH160 (compress,uncompress,SegWit) а также адрес ethereum.
    после генерации все хеши прогоняются через фильтры на совпадения.

## Предварительные установки
    для работы программы требуется Python 3.6 или выше.
    В версии 3.11 скорость будт выше, это связанно с изменениями CPython
    ```python:
    pip install pysha3
    ```

## Создание базы BloomFilter:
    для создания блюм фитьтров вам необходим список файлов с адресами:
    скачать его можно ![Database Dumps](https://blockchair.com/dumps#database)
    Если вы скачиваете файлы адресов по вышеуказаной ссылке, то перед использование файлов их надо отредактировать.
    Для редактирования рекомендую EMEDITOR
    ```python:
    winndows:
    python create-bloom.py <IN File> <OUT File>
    linux:
    python3 create-bloom.py <IN File> <OUT File>
    ```
    IN File - Файл с адресами построчно (один адрес на одну строку)
    OUT File - Файл BloomFilter, в процесе конвертации и фильтрации адресов в него добавляются данные.

## Описание параметров программы
    -th - количество ядер для обработки данных
    -dbbtc - база BloomFilter созданная из адресов BTC
    -dbeth - база BloomFilter созданная из адресов ETH
    -bal - проверка баланса, если в BloomFilter найдено совпадение
    -telegram - отправка сообщения вам в telegram при совпадении.

    ```python:
    winndows:
    python BrainHunt.py -th 4 -dbbtc BF/btc.bf -dbeth BF/eth.bf -bal -telegram
    linux:
    python3 BrainHunt.py -th 4 -dbbtc BF/btc.bf -dbeth BF/eth.bf -bal -telegram
    ```

Если Вас заинтересовала эта программа, пишите в телеграмм.
