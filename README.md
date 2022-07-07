# BrainHunt
    BrainHunt - это реализация инструмента brainflayer на языке Python. это простой и одновременно функциональный инструмент. 
    Функционал расширен если смотреть на источник. Программы производить хеширование в 3х алгоритмах (SHA256, SHA3, Keccak-256)
    После хеширования полученный хеш является private key, из полученного ключа создаются 3 HASH160 (compress,uncompress,SegWit) а также адрес ethereum.
    после генерации все хеши прогоняются через фильтры на совпадения.

## Предварительные установки
    для работы программы требуется Python 3.6 или выше.
    В версии 3.11 скорость будет выше, это связанно с изменениями CPython
    ```python:
    pip install -r requirements.txt
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
    -dbbtc - база BloomFilter созданная из адресов BTC (на текущий момент BTC и альткоины)
    -dbeth - база BloomFilter созданная из адресов ETH
    -dbalt - база BloomFilter созданная из адресов альткоинов (это будет в процессе...)
    -bal - проверка баланса, если в BloomFilter найдено совпадение
    -telegram - отправка сообщения вам в telegram при совпадении.
    -id - если вы запускаете несколько копий программы (что в полне обоснованно) то для сохнанения положения вам потребуется ID процесса.
    -desc - описание машины на которой запускается процесса
    -save - указание времени сохраниея положения поиска в секундах
    -in - выходящий файл (для ревизии BrainHunt)

    ```python:
    winndows:
    python -B BrainHunt.py -th 3 -id 0 -dbbtc BF/all.bf -dbeth BF/eth.bf -in dictionaries/10-million-combos.txt -bal -telegram -desc home -save 10
    linux:
    python3 -B BrainHunt.py -th 3 -id 0 -dbbtc BF/all.bf -dbeth BF/eth.bf -in dictionaries/10-million-combos.txt -bal -telegram -desc home -save 10
    winndows:
    mp64.exe -i 1:7 -q 2 ?l?l?l?l?l?l?l | python BrainHunt_EX.py -th 3 -id 0 -dbbtc BF/all.bf -dbeth BF/eth.bf -bal -telegram -desc home -save 10
    linux:
    mp64.bin -i 1:7 -q 2 ?l?l?l?l?l?l?l | python3 BrainHunt_EX.py -th 3 -id 0 -dbbtc BF/all.bf -dbeth BF/eth.bf -bal -telegram -desc home -save 10
    winndows:
    python BrainHunt_SEQ.py -th 1 -id 0 -dbbtc BF/all.bf -dbeth BF/eth.bf -bal -telegram -word genesis -desc home -save 10
    linux:
    python3 BrainHunt_SEQ.py -th 1 -id 0 -dbbtc BF/all.bf -dbeth BF/eth.bf -bal -telegram -word genesis -desc home -save 10
    ```

##Общее описание
    Программа работает с мультиядерностью, за счет чего повышается скорость работы.
    одновременное хеширование из 3х хешей (sha256, sha3, Keccak-256) (получение приватного ключа)
    получение из приватного ключа всех возможных комбинаций адреса (uncompress, compress, sigwit)
    программа проверяет баланс при включении параметра включение баланса

##PS
    в программу добаылены куча генераторов, которые решат все ваши потребности.
    

