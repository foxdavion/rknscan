#RKNScanner
Scanner for testing DPI + ability to scan Roskomnadzor registry and custom lists
В планах:
- Добавление функции проверки доступности сайта по всем отрезолвиным IP.
- Добавление функции проверки доступности сайта по записям IP из реестра(принцип работы ревизора с последними изменениями).
- Автоматическое оповещение на почту с результатами сканирования.

##Установка в Ubuntu(debian)
apt-get install python3
apt-get install python3-pip

Для того что бы скрипт делал скриншоты открытых сайтов необходимо установить phantomjs. Файл rasterize.js из папки example дистрибутива phantomjs разместить в папке /opt/assets. Создайте папку /opt/rkn в которой будут создаваться папки со скриншотами сайтов по результатам сканирования.

Файл реестра dump.xml необходимо разместить в директории скрипта.

##Модули для установки в pip install
```
request
pyOpenSSL 
ndg-httpsclient 
pyasn1 
dnspython3
colorama
termcolor
```

## Usage
```
Usage: rknscan.py [options]

Options:
  -h, --help            show this help message and exit
  -r REGEXP, --regexp=REGEXP
                        Установить регулярное выражение, по которому будет
                        матчиться вывод открываемой страницы (тут необходимо
                        указать какой-либо кусок со страницы заглушки)
  -v, --verbose         Увеличить вербозность (для дебага)
  -n N_THREADS, --numthreads=N_THREADS
                        Установить количество потоков (defaul=50)
  -p, --printscreen		При указании будет делать скриншоты сайтов(необходимо что бы был установлен phantomjs)
  -t TIMEOUT, --timeout=TIMEOUT
                        Таймаут по истечению которого неответивший сайт
                        считается недоступным (default=3)
  -f FILE, --file=FILE  Указать файл с перечнем URL для проверки (НЕ в случае
                        реестра Роскомнадзора)
  -s, --substituteip    Добавление в выборку URL адресов, с
                        замененным доменом на IP адрес (в случае реестра
                        Роскомнадзора)
  -c, --console         Запуск в консольном режиме (без интерактива)

```
После сканирования в директории скрипта будет создан файл not_block_дата с результатами сканирования.

If we are going to check RKN registry - firstly we have to download it (dump.xml) manualy from http://vigruzki.rkn.gov.ru/tooperators_form/ and put it in the same directory with rknscan.py

typically command to run:

```
python3 rknscan.py -p -t 3 -n 400 -r "nap.rkn.gov.ru" -c
```
