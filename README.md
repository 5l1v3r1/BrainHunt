# BrainHunt
    BrainHunt - это реализация инструмента brainflayer на языке Python. это простой и одновременно функциональный инструмент. 
    Функционал расширен если смотреть на источник. 
    Функционал разбит на три программы:
        BrainHunt.py - Класическая реализация, но с расширенным хешированием (SHA256, SHA3, Keccak-256). Программа читает файл любого объема, полученые строки из файла подает в хеширование где создается приватный ключ.
        BrainHunt_EX.py - Реализация основана на класической с теми же функциями, но подача данных идет не из чтения из файла, а с внешнего источника, сделана для работы с генераторами (генераторы в наличии)
        BrainHunt_SEQ.py - Эта программа для последовательного поиска. в параметрах указывается слово и это слово начинает хешироватся до бесконечности.
    После хеширования полученный хеш является private key, из полученного ключа создаются три HASH160 (compress,uncompress,SegWit) а также адрес ethereum.
    После генерации все хеши прогоняются через фильтры на совпадения.
    В блюмфильтре ALL.BF содержатся 7 валетов (BTC,BTC-SV,BTC-CASH,DASH,DOGECOIN,LITECOIN,ZCASH) - рекомендую его использовать вместо BTC

## Предварительные установки
    для работы программы требуется Python 3.6 или выше.
    ```python:
    pip install -r requirements.txt
    ```

## Создание базы BloomFilter:
    для создания блюм фитьтров вам необходим список файлов с адресами:
    скачать его можно ![Database Dumps](https://blockchair.com/dumps#database)
    Если вы скачиваете файлы адресов по вышеуказаной ссылке, то перед использование файлов их надо отредактировать.
    Для редактирования рекомендую EMEDITOR
    после редактирования можно создавать блюмфильтр
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
    -dbbtc - база BloomFilter созданная из адресов BTC (на текущий момент BTC и ALL)
    -dbeth - база BloomFilter созданная из адресов ETH
    -dbalt - база BloomFilter созданная из адресов альткоинов (альткоины третьего эшелона)
    -bal - проверка баланса, если в BloomFilter найдено совпадение
    -telegram - отправка сообщения вам в telegram при совпадении.
    -id - если вы запускаете несколько копий программы (что в полне обоснованно) то для сохнанения положения вам потребуется ID процесса.
    -desc - описание машины на которой запускается процесс
    -save - указание времени сохранения положения поиска в секундах (кроме SEQ)
    -in - выходящий файл (для ревизии BrainHunt)

    PS: сохрание точек в ревизии SEQ не предусмотренно.

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
    python BrainHunt_SEQ.py -th 1 -id 0 -dbbtc BF/all.bf -dbeth BF/eth.bf -bal -telegram -word genesis -desc home
    linux:
    python3 BrainHunt_SEQ.py -th 1 -id 0 -dbbtc BF/all.bf -dbeth BF/eth.bf -bal -telegram -word genesis -desc home
    ```

## P.S.
    в программу добаылены куча генераторов, которые решат все ваши потребности.

## Заинтересованы ?
    пишите в Telegram
