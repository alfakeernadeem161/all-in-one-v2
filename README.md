[![Typing SVG](https://readme-typing-svg.herokuapp.com?color=%2336BCF7&lines=All-in-one+V2)](https://git.io/typing-svg)

Идеальный скрипт-V2 для ведения фермы. Освоив его, ты сможешь (идет перечисление модулей) :

1. web3_checker : очень быстро (асинка) смотрит баланс монеты в любой evm сети.
2. debank_checker : около быстро (асинка) смотрит все токены, нфт и протоколы во всех evm сетях (которые доступны на самом [debank](https://debank.com/)). 
3. exchange_withdraw : вывод монет с бирж : binance, mexc, kucoin, bybit, huobi, bitget.
4. okx_withdraw : вывод с биржи okx + в подарок вывод с субов. отдельным модулем из-за функции вывода с суб-аккаунтов.
5. transfer : вывод монет с кошельков в evm сетях.
6. 0x_swap : аграгатор, хорошая замена 1inch.
7. [orbiter](https://www.orbiter.finance/) : бридж eth во всех сетях, включая zksync era и starknet. чтобы бриджит на starknet, нужно добавить адреса кошельков старкнета в файл `starknet_address.txt`.
8. [woofi](https://fi.woo.org/) : bridge. бридж проходит через stargate (layerzero). универсален, доступны все монеты и сети, которые там есть. 
9. [woofi](https://fi.woo.org/) : swap. универсален, доступны все монеты и сети, которые там есть. 
10. sushiswap : универсальный, доступны все основные сети, кроме optimism (пока что).
11. bungee_refuel : дешевый бридж нативки между сетями.
12. tx_checker : смотрит nonce во всех (почти) evm сетях.
13. 1inch_swap : агрегатор. 
14. merkly_refuel : отправка газа с одной сети в другую через layerzero.
15. nft_checker : очень быстро (асинка) смотрит баланс конкретной nft.

Дополнительная информация :
1. Вместо принтов сделал logger. 
2. Добавил tg_sender. Все результаты прописываются не только в терминал, но и в тг-бота.
3. Для чекеров сделал csv файлы. 
4. Сделал нормальные try exceptы.
5. Сделал проверку транзакций на фейл (check_status_tx).
6. Сделал универсальный апрув и предварительную проверку на кол-во апрувнутых монет (check_allowance). то есть лишних апрувов делать не будет.
7. Добавил возможность включить прокси в web3. Работает это так : берет все твои кошельки и поочередно берет прокси из файла `proxies.txt`. То есть распределение на прокси будет равным. Кол-во кошельков и прокси может отличаться. Например, если будет 10 кошельков и 3 прокси, то распределение будет такое : прокси_1 = 4 кошелька, прокси_2 = 3 кошелька, прокси_3 = 3 кошелька.
8. Добавил чекер base_gas (https://etherscan.io/gastracker) в эфире, чтобы скрипт висел в ожидании если газ > заданного числа.
9. Добавил максимальную плату за газ в $ для каждой сети. если газ в транзе будет выше заданного числа, скрипт будет спать, пока газ не снизится (`setting.py => MAX_GAS_CHARGE`)
10. Если транзакция висит в пендинге > заданного времени (`config.py => max_time_check_tx_status`), она считается исполненной. это я сделал из-за bsc, тк с 1 гвеем некоторые транзы висят в пендинге часами, и скрипт соответственно тоже.
11. Для 0x_swap требуется api key, который можно получить здесь : https://dashboard.0x.org/apps. Более подробно описал здесь : https://t.me/never_broke_again_v1/315

# Настройка.

1. Вся настройка делается в файле `setting.py`, описание там же. 
2.  В папке `data` есть 5 файлов : `wallets.txt`, `recipients.txt`, `proxies.txt`, `starknet_address.txt`, `data.py` :
- `wallets.txt` - сюда записываем кошельки (приватники / адреса).
- `recipients.txt` - сюда записываем адреса для трансфера, используется только в модуле transfer когда выводим с кошелька на адрес. 1 кошелек = 1 адрес.
- `proxies.txt` - сюда записываем прокси, они используются в debank чекере, без них он работать не будет, и в web3, если `USE_PROXY = True` (в конфиге). Формат : http://login:password@ip:port
- `starknet_address.txt` - сюда записываем адреса кошельков старкнета. если не будете бриджить с орбитера на старкнет, можно не вставлять.
- `data.py` - здесь вся приватная информация : rpc, tg_token, tg_id, апи ключи от бирж.
3. Настраивать модули нужно в функциях value в файле `setting.py`.
4. Запускать нужно файл `main.py`, в терминале будет список с модулями, нужно будет выбрать один.

Устанавливаем библиотеки : `pip install -r requirements.txt`

Огромная просьба сначала все прочитать на 10 раз, все протестировать, погуглить и только потом задавать вопросы в наш код чат. В личку админам с вопросами по коду просьба не писать, они не ответят.

Donate (evm) : `0xb7415DB78c886c67DBfB25D3Eb7fcd496dAf9021` or `donates-for-hodlmod.eth`

Паблик : https://t.me/hodlmodeth. [ code ] чат : https://t.me/code_hodlmodeth. Канал с обновлениями и лайф-рофл-контентом : https://t.me/never_broke_again_v1
