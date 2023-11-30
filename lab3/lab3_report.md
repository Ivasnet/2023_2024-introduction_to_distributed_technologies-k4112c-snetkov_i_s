University: [ITMO University](https://itmo.ru/ru/)

Faculty: [FICT](https://fict.itmo.ru)

Course: [Introduction to distributed technologies](https://github.com/itmo-ict-faculty/introduction-to-distributed-technologies)

Year: 2023/2024

Group: K4112c

Author: Snetkov Ivan Sergeevich

Lab: Lab3

Date of create: 23.11.2023

Date of finished: -

_________________________________________________________________________________________________________________________________________________________


## Подготовка
1. Для начала скачаем репозиторий на рабочий компьютер:
  `docker pull ifilyaninitmo/itdt-contained-frontend:master`
2. Запускаем Minikube:
  `minikube start`
3. Затем включим Ingress:
  `minikube addons enable ingress`

## Выполнение работы
1. Создадим [configMap](https://github.com/Ivasnet/2023_2024-introduction_to_distributed_technologies-k4112c-snetkov_i_s/blob/main/lab3/configmap.yaml) с переменными `REACT_APP_USERNAME` и `REACT_APP_COMPANY_NAME`

2. Применим configMap:
  `kubectl apply -f configMap.yaml`

3. Создадим и применим replicaSet с двумя репликами контейнера [ifilyaninitmo/itdt-contained-frontend:master](https://hub.docker.com/repository/docker/ifilyaninitmo/itdt-contained-frontend), а также передадим переменные из configMap `REACT_APP_USERNAME` и `REACT_APP_COMPANY_NAME`: 
  ![изображение](https://github.com/Ivasnet/2023_2024-introduction_to_distributed_technologies-k4112c-snetkov_i_s/assets/70843270/09feaa8e-671d-48c2-95a5-e05d0c1cbe64)


4. Создадим и применим service: 
  `kubectl apply -f service.yaml`

5. Сгенерируем TLS-сертификат и импортируем его в `minikube`:
  `openssl req -x509 -newkey rsa:4096 -sha256 -days 12 -nodes -keyout tls.key -out tls.crt -subj "/CN=lab3.front.com"`
  `kubectl create secret tls lab3-local-tls --cert=tls.crt --key=tls.key`
![изображение](https://github.com/Ivasnet/2023_2024-introduction_to_distributed_technologies-k4112c-snetkov_i_s/assets/70843270/1c4a6a61-eabd-466f-a3d6-7484d491b9b7)


6. Создадим `Ingress`:
`kubectl apply -f ingress.yaml`

7. Пропишем адрес в hosts и прокинем туннель между `minikube` и локальной машиной:
`127.0.0.1 lab3.front.local`

8. Переходим на сайт: https://lab3.front.local
![изображение](https://github.com/Ivasnet/2023_2024-introduction_to_distributed_technologies-k4112c-snetkov_i_s/assets/70843270/e2d6d961-1c2c-47cc-9df8-a10e4f9230ed)

А также сертификат:
![изображение](https://github.com/Ivasnet/2023_2024-introduction_to_distributed_technologies-k4112c-snetkov_i_s/assets/70843270/e1fd8ead-d40e-4b39-ab13-bcc4bb17babb)



## Схема организации контейеров и сервисов
![изображение](https://github.com/Ivasnet/2023_2024-introduction_to_distributed_technologies-k4112c-snetkov_i_s/assets/70843270/aed2e4bb-5635-4748-9275-e96d5dedd314)



