University: [ITMO University](https://itmo.ru/ru/)
Faculty: [FICT](https://fict.itmo.ru)
Course: [Introduction to distributed technologies](https://github.com/itmo-ict-faculty/introduction-to-distributed-technologies)
Year: 2023/2024
Group: K4112c
Author: Snetkov Ivan Sergeevich
Lab: Lab1
Date of create: 09.11.2023
Date of finished: -

_________________________________________________________________________________________________________________________________________________________


# Подготовка
1. Установим [Docker](https://www.docker.com/) на рабочий компьютер
2. Установим [Minikube](https://minikube.sigs.k8s.io/docs/start/)
3. Выполним запуск Minikube: 
  `minikube start`
4. Проверим, что Minikube запущен: 
  `minikube status`
   ![изображение](https://github.com/Ivasnet/2023_2024-introduction_to_distributed_technologies-k4112c-snetkov_i_s/assets/70843270/03d9a5dd-bf22-400a-abac-fbb995439ba6)
5. Установим kubectl: 
  `minikube kubectl`

# Выполнение работы
1. Создадим манифест [vault.yaml](https://github.com/Ivasnet/2023_2024-introduction_to_distributed_technologies-k4112c-snetkov_i_s/blob/main/lab1/vault.yaml)
![изображение](https://github.com/Ivasnet/2023_2024-introduction_to_distributed_technologies-k4112c-snetkov_i_s/assets/70843270/a4b3d9ef-97d6-40c4-81fe-b1c37212a087)
2. Применим данный манифест для создания пода: 
  `minikube kubectl -- apply -f vault.yaml`
3. Создадим сервис для доступа к поду: 
  `minikube kubectl -- expose pod vault --type=NodePort --port=8200`
4. Пробросим порты для доступа: 
  `minikube kubectl -- port-forward service/vault 8200:8200`
5. Найдём данные для входа в vault в логах с использованием комманды:
 `minikube kubectl -- logs vault`
![скрин](https://github.com/Ivasnet/2023_2024-introduction_to_distributed_technologies-k4112c-snetkov_i_s/assets/70843270/14c8d30e-eeaf-46e9-9d19-03e9692b8129)
6. С помощью `Root Token` произведём вход на портал:
![изображение](https://github.com/Ivasnet/2023_2024-introduction_to_distributed_technologies-k4112c-snetkov_i_s/assets/70843270/f6d636b5-7926-4837-ae95-17183b42e3f4)

# Очистка ресурсов
1. Удалим под:
  `minikube kubectl -- delete pod vault`
2. Удалим сервис:
  `minikube kubectl -- delete service vault`
3. Остановим работу кластера:
  `minikube stop`
