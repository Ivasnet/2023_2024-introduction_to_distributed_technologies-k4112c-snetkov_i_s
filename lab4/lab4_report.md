University: [ITMO University](https://itmo.ru/ru/)

Faculty: [FICT](https://fict.itmo.ru)

Course: [Introduction to distributed technologies](https://github.com/itmo-ict-faculty/introduction-to-distributed-technologies)

Year: 2023/2024

Group: K4112c

Author: Snetkov Ivan Sergeevich

Lab: Lab4

Date of create: 28.11.2023

Date of finished: -

_________________________________________________________________________________________________________________________________________________________


## Выполнение работы
1. Запустим Minikube с плагином CNI Calico и в режиме `Multi-Node Clusters`:
  `minikube start --network-plugin=cni --cni=calico --nodes 2 -p multinode`
  ![изображение](https://github.com/Ivasnet/2023_2024-introduction_to_distributed_technologies-k4112c-snetkov_i_s/assets/70843270/4d5edb7c-db7c-4209-8185-04ad5280a26f)


2. Выполним проверку при помощи команд `kubectl get nodes` и `kubectl get pods -n kube-system -l k8s-app=calico-node`:
  ![изображение](https://github.com/Ivasnet/2023_2024-introduction_to_distributed_technologies-k4112c-snetkov_i_s/assets/70843270/af182b40-e70d-4ed5-8bc2-c5fd7c31ba30)


3. Пропишем `label`:
  `kubectl label node multinode culture=1`
  `kubectl label node multinode-m02 culture=2`
  ![изображение](https://github.com/Ivasnet/2023_2024-introduction_to_distributed_technologies-k4112c-snetkov_i_s/assets/70843270/4d3a3ae6-0a92-4eac-be43-c8c16a54604d)


4. Выполним проверку:
  ![изображение](https://github.com/Ivasnet/2023_2024-introduction_to_distributed_technologies-k4112c-snetkov_i_s/assets/70843270/ae4b765b-13db-4c23-a866-e999ff599418)


5. Создадим `calico.yaml` и применим его:
  `kubectl create -f calico.yaml`

6. Создадим IPPOOL с помощью `calico`: 
  `kubectl exec -i -n kube-system calicoctl -- /calicoctl create -f - < ippool.yaml --allow-version-mismatch`
  ![изображение](https://github.com/Ivasnet/2023_2024-introduction_to_distributed_technologies-k4112c-snetkov_i_s/assets/70843270/20fe7f07-277b-459c-b34a-3dbc4b65673c)



## Схема организации контейеров и сервисов
![изображение](https://github.com/Ivasnet/2023_2024-introduction_to_distributed_technologies-k4112c-snetkov_i_s/assets/70843270/f0ba807b-e40b-434a-afa1-187dcb3f55a0)



