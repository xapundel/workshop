# Школа по искуственному интелекту. Лабораторные работы. 

Предварительная подготовка:
1.	Подключиться к [телеграмм группе воркшопа](https://ibm.biz/BdZFsB)
1.	Зарегистрироваться в [IBM Cloud](https://ibm.biz/Bdi6FX)
1.	Установить [IBM Cloud CLI ](https://ibm.biz/BdZFsx)
1.	Установить [kubectl](https://ibm.biz/BdZFsR)
1.	Почитать о том что такое Docker, Kubernetes и Jupyter
1.	Установить Docker и проверить его работоспособность.
1.	Установить git
1.	Не забыть ноутбук и хорошее настроение

## Лабораторная 1. Аналитика в контейнере
*	В командной строке скопировать github проект лабораторных работ
```
git clone …
cd workshop
```
* Создать изолированную сеть Docker командой
```
docker network create mynet
```
* Скачать Docker image и запустить на выполнение NoSQL Cloudant
```
docker pull ibmcom/cloudant-developer
docker run \
       --name cloudant \
       --detach \
       --network=mynet \
       --volume cloudant:/srv \
       --name cloudant-developer \
       --publish 8080:80 \
       --hostname cloudant.dev \
       ibmcom/cloudant-developer
```
* проверить работоспособность ссылок [json базы](http://localhost:8080) и [пользовательского интерфейса](http://localhost:8080/dashboard.html).  Логин и пароль по умолчанию admin /pass
* Скачать Docker image и запустить на выполнение Jupyter notebook
```
docker pull jupyter/datascience-notebook
docker run --network=mynet -d -p 8888:8888 jupyter/datascience-notebook start-notebook.sh --NotebookApp.token=''
```
* проверить работоспособность [ссылки](http://localhost:8888/)
* загрузить тестовый ноутбук и запустить все блоки
* проверить данные в [cloudant](localhost:8080/dashboard.html)
## Лабораторная 2. Аналитика в облаке
* Зайти на сайт bluemix.net
* Активировать код 

`Manage` -> `Billing and Usage` -> `Billing` -> `Billing` -> `Feature(Promo) Codes` -> `Apply code`

* Создать новый space  в организации. Укажите `Region US South` и имя `dev`

`Manage` -> `Billing and Usage` -> `Billing` -> `Cloud Foundry Orgs` –> `View Details` -> `Add a Cloud Foundry Space`. 

* Следующие команды позволяют взаимодействовать с IBM Cloud из консоли
```
cd workshop/Bluemix-Jupyter-Notebook
#Авторизуйтесь введя свою почту, пароль к аккаунту, выберите название аккаунта
bx login   
#Укажите неймспейс и название организации используя
bx target -o <почта> -s dev
#опубликовать приложение без запуска
bx cf push --no-start
#запустить приложение
bx cf start ipython
```
* перейти в пользовательский интерфейс `IBM Cloud` -> `Dashboard` -> `ipython app` -> `Visit App URL` и проверить пользовательский интерфейс (поле ввода пароля оставить пустым)
* создать базу данных cloudant для этого перейти в
`IBM Cloud catalog` -> `Data & Analytics` ->`Cloudant NoSQL DB` -> `Create`. Перед созданием указать тот же namespace где развернуто приложение (dev)
* подключить Cloudant для этого перейти в
`IBM Cloud dashboard` -> `Ipython` -> `Connections` -> `Create connection` -> `Cloudant` -> `Connect`
* проверить пользовательский интерфейс загрузив demo.ipynb в пользовательский интерфейс и проверив базу данных по результату выполнения

## Лабораторная 3. Аналитика корпоративного уровня.
* Зайти на datascience.ibm.com
* Зарегистрироваться ( ассоциировать IBM Cloud аккаунт с используемой записью) нажав `Sign up`
* Создать проект добавив к нему Apache Spark и Object Storage `New Project` -> `Add Spark Service` -> `Add Object Storage`
* Загрузить demo.ipynb и модифицировать Credential доступа к Cloudant. Взяв их из IBM Cloud.

