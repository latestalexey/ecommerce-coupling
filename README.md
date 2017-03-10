# Слабая связанннось в режиме онлайн

суть репозитория - показать принципы слабой связанности в режимах когда необходим онлайн между онлайн магазином и 1С
и дополнительно показать принципы

* нескольких подписчиков на одно событие средствами AMQP
* работу в 1С с заказами покупателей на сайте в режиме онлайн

## Контур проверки

ориентирован на Docker - для быстрой проверки и отладки

состав контура (docker контейнеры)

* магазин https://github.com/reactioncommerce/reaction
 * с плагином для работы с подписками RMQ
* rabbitmq - для подключения контура доставки данных
* elastisearch - для организации DWH в режиме наполнения данных
* kibana - для отображения данных реальном времени
* сложная аналитика - для обработки данных DWH https://hub.docker.com/r/dataiku/dss/

### Дополнительно

* добавлена конфигурация эмулятор УТ 11 (1С) в режиме подключенния к ElasticSearch 
  * для владельцев infostart.ru/public/570477/ содержит код интеграции в реальном времени

## Как проверить

требуется установленный docker старше 1.12 (для Windows требуется msgit с установленным sh.exe интерпретатором)

* `build.sh` - соберет все контейнеры
* `run.sh` - запустит все контейнеры на разных портах

после чего откройте браузер

* начните добавлять товар в корзину - смотрите как меняется данные в Kibana и в 1С
* сформируйте заказ - увидите как меняется данные в Kibana и в 1С

### Как проверить слабую связанность

* убейте ELK - `kill-elk.sh`
* закройте 1С

* начните добавлять товар в корзину
* сформируйте заказ

* запустите ELK - `start-elk.sh`


## FAQ

* почему не Bitrix ?  - А он слишком платный, а Node.JS платформа `reactioncommerce/reaction` дает возможность поэкспериментировать бесплатно
* откуда взялся `dataiku` ? - заходим сюда http://gallery.dataiku.com/ и смотрим ;-)
* зачем это репозиторий ? - [смотрим расширенное описание](./docs/)


## LICENCE

`Mozilla Public License Version 2.0` - c упоминанием авторства, не забывайте ;-)
