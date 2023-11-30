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


5. Создадим `calico.yaml`, `deployment.yaml` и `service.yaml` и применим их:
  `kubectl create -f deployment.yaml`
  `kubectl create -f service.yaml`
  `kubectl create -f calico.yaml`

6. Создадим IPPOOL с помощью `calico`: 
  `kubectl exec -i -n kube-system calicoctl -- /calicoctl create -f - < ippool.yaml --allow-version-mismatch`

7. Далее откроем доступ к `Minikube` и пробросим порты:
   `minikube service frontend-service`
   `kubectl port-forward service/frontend-service 9090:9090` 
8. Запустим клиента:
  ![изображение](https://github.com/Ivasnet/2023_2024-introduction_to_distributed_technologies-k4112c-snetkov_i_s/assets/70843270/07a6aeb0-59cc-4c8a-916b-882fda72d0e9)
9. С помощью команды `kubectl exec -it frontend-48dq56hd8-atuhq -- /bin/sh` выполним пинг одного из контейнеров:
   ```
    PING 10.244.134.187 (10.244.134.187): 56 data bytes
    64 bytes from 10.244.134.187: seq=0 ttl=64 time=1.003 ms
    64 bytes from 10.244.134.187: seq=1 ttl=64 time=0.237 ms
    64 bytes from 10.244.134.187: seq=2 ttl=64 time=0.125 ms
    64 bytes from 10.244.134.187: seq=3 ttl=64 time=0.101 ms


## Схема организации контейеров и сервисов
![изображение](https://github.com/Ivasnet/2023_2024-introduction_to_distributed_technologies-k4112c-snetkov_i_s/assets/70843270/e53a27ae-5960-45a7-a2ab-8942ccbb5df2)




