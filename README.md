# Подключение ротации прокси-серверов к проекту на scrapy

Подключение выполняется в Downloader Middleware.

Чтобы его подключить, надо

0) Инсталлировать 
    ```
    pipenv run python -m pip install -e git+http://gitlab.groupbwt.com/root/proxy-server.git/#egg=bwt_scrapy_proxy&subdirectory=bwt_scrapy_proxy
    ```
    или
    ```
    pip install -e git+http://gitlab.groupbwt.com/root/proxy-server.git/#egg=bwt_scrapy_proxy&subdirectory=bwt_scrapy_proxy
    ```

0) в settings.py в словарь DOWNLOADER_MIDDLEWARES добавить
   ```
   'bwt_scrapy_proxy.ProxyRotationMiddleware':530
   ```

0) в settings.py добавить параметры
   ```
      X_BWT_PROXY_MEDIATOR = "http://192.168.11.82:5001"
      X_BWT_PARSERNAME = "test"
   ```
   Сейчас mitmproxy работает на 192.168.11.82 и слушает порт 5001

   X_BWT_PARSERNAME = "test" - уникальный идентификатор парсера

0) в базу данных (таблица parsers) внести уникальный идентификатор парсера
   (параметр X_BWT_PARSERNAME из settings.py)
   и максимальное количество коннектов (parsers.threads_limit)
   Это делает админ БД парсеров.
