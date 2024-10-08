# Домашнее задание к занятию 17 «Инцидент-менеджмент»

## Задание

Составьте постмортем на основе реального сбоя системы GitHub в 2018 году.

Информацию о сбое можно изучить по ссылкам ниже:

* [краткое описание на русском языке](https://habr.com/ru/post/427301/);
* [развёрнутое описание на английском языке](https://github.blog/2018-10-30-oct21-post-incident-analysis/).

|          <!-- -->          |                                                                                                                                                                                                                                                                                                 <!-- -->                                                                                                                                                                                                                                                                                                 |
|:--------------------------:|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
| Краткое описание инцидента |                                                                                                                                                                                                                                         Сбой сетевого раздела с последующим сбоем БД, что привело к появлению непоследовательной информации на сайте github.com                                                                                                                                                                                                                                          | 
|   Предшествующие события   |                                                                                                                                                                                                                                                    Плановые работы по техническому обслуживанию по замене неисправного оптического оборудования 100G                                                                                                                                                                                                                                                     |
|     Причина инцидента      |                                                                                                                                                                                                                                     Потеря соединения между сетевым узлом на восточном побережье США и основным центром обработки данных на восточном побережье США                                                                                                                                                                                                                                      |
|        Воздействие         |                                                                                                                                                                                                                                                                      Деградация части предоставления сервиса на 24 часа и 11 минут                                                                                                                                                                                                                                                                       |
|        Обнаружение         |                                                                                                                                                                                                                               2018 21 октября 22:54 UTC внутренние системы мониторинга начали генерировать оповещения, указывающие на многочисленные сбои в работе система                                                                                                                                                                                                                               |
|          Реакция           |   В 23:02 UTC инженеры группы быстрого реагирования определили, что топологии многочисленных кластеров баз данных находятся в неожиданном состоянии. Запрос к API Orchestrator показал топологию репликации базы данных, которая включала только серверы из центра обработки данных на западном побережье США. В 23:09 UTC группа реагирования перевела сайт в желтый статус. Это действие автоматически перевело ситуацию в активный инцидент и отправило предупреждение координатору инцидента. В 23:11 UTC подключился координатор инцидентов и через две минуты изменил статус решения на красный.   |
|       Восстановление       |                                                                                                                                                                              2018 22 октября 00:05 UTC Разработан план восстановления - восстановление данных из резервных копий, синхронизация реплик на обеих площадках, возврат к стабильной топологии обслуживания, а затем возобновление обработки заданий в очереди.                                                                                                                                                                               |
|          Таймлайн          |                                                                                                                                                                                                                                          2018-10-21 22:52 UTC Кратковременная потеря соединения между центрами обработки данных, начало деградации кластера БД                                                                                                                                                                                                                                           |
|          <!-- -->          |                                                                                                                                                                                                                                                                 2018-10-21 22:54 UTC Генерация оповещений внутренней системы мониторинга                                                                                                                                                                                                                                                                 |
|          <!-- -->          |                                                                                                                                                                                                                                                                          2018-10-21 23:02 UTC Подтверждение проблемы инженерами                                                                                                                                                                                                                                                                          |
|          <!-- -->          |                                                                                                                                                                                                                                                                  2018-10-21 23:07 UTC Блокировка внутренних инструментов развертывания                                                                                                                                                                                                                                                                   |
|          <!-- -->          |                                                                                                                                                                                                                                                                         2018-10-21 23:09 UTC Изменение статуса сервиса на желтый                                                                                                                                                                                                                                                                         |
|          <!-- -->          |                                                                                                                                                                                                                                                      2018-10-21 23:11 UTC Привлечение координатора инцидентов, изменение статуса сервиса на красный                                                                                                                                                                                                                                                      |
|          <!-- -->          |                                                                                                                                                                                                                                                                   2018-10-21 23:13 UTC Обнаружение конкретной проблемы с кластерами БД                                                                                                                                                                                                                                                                   |
|          <!-- -->          |                                                                                                                                                                                                                                              2018-10-21 23:19 UTC Частичная контролируемая остановка выполнения заданий, выполняющих запись метаданных в БД                                                                                                                                                                                                                                              |
|          <!-- -->          |                                                                                                                                                                                                                                                            2018-10-22 00:05 UTC Разработка плана по восстановлению данных из резервных копий                                                                                                                                                                                                                                                             |
|          <!-- -->          |                                                                                                                                                                                                                                                              2018-10-22 00:41 UTC Начало процесса восстановления данных из резервных копий                                                                                                                                                                                                                                                               |
|          <!-- -->          |                                                                                                                                                                                                                                                            2018-10-22 06:51 UTC Начало второго этапа восстановления данных из резервных копий                                                                                                                                                                                                                                                            |
|          <!-- -->          |                                                                                                                                                                                                                                                                    2018-10-22 07:46 UTC Публикация сообщения с описанием сбоя в блоге                                                                                                                                                                                                                                                                    |
|          <!-- -->          |                                                                                                                                                                                                                       2018-10-22 11:12 UTC Завершение процесса восстановления данных. Начало процесса реплицирования данных между кластерами. Улучшение отзывчивости работы сайта                                                                                                                                                                                                                        |
|          <!-- -->          |                                                                                                                                                                                                                   2018-10-22 13:15 UTC Предоставление дополнительных реплик чтения MySQL в общедоступном облаке Восточного побережья США для уменьшения задержи репликации на чтение.                                                                                                                                                                                                                    |
|          <!-- -->          |                                                                                                                                                                                                                         2018-10-22 16:24 UTC Завершение синхронизации реплик. Статус сервисов сохранен на красном уровне, чтобы закончить процессы, накопившиеся за время сбоя.                                                                                                                                                                                                                          |
|          <!-- -->          |                                                                                                                                                                                                                                                  2018-10-22 16:45 UTC Обработка фоновых задач, накопившихся за время аварии. Удаление устаревших задач.                                                                                                                                                                                                                                                  |
|          <!-- -->          |                                                                                                                                                                                  2018-10-22 23:03 UTC Все ожидающие сборки веб-перехватчиков и страниц были обработаны, а целостность и правильная работа всех систем подтверждены. Статус сайта изменился на зеленый. Восстановление работы сервиса в штатном режиме.                                                                                                                                                                                   |
|   Последующие действия     | Были проанализированы бинарные записи восстановления MySQL для восстановления записей, не скопированных в ЦОД Западного побережья. Были внесены изменения в настройки оркестровщика, так, чтобы предотвратить распространение основных баз данных за пределы региональных границ. Ускорен переход на новый механизм отчетов статуса предоставления сервиса. За несколько недель до инцидента начата общекорпоративная инициатива по поддержке обслуживания трафика GitHub из нескольких ЦОД, поддержка резервирования N+1. Внедрение практики проверки негативных сценариев до того, как они произойдут. |



