# Домашняя работа к занятию «Базовые объекты K8S» - Боровик А.А.

### Цель задания

В тестовой среде для работы с Kubernetes, установленной в предыдущем ДЗ, необходимо развернуть Pod с приложением и подключиться к нему со своего локального компьютера. 

------

### Чеклист готовности к домашнему заданию

1. Установленное k8s-решение (например, MicroK8S).
2. Установленный локальный kubectl.
3. Редактор YAML-файлов с подключенным Git-репозиторием.

------

### Инструменты и дополнительные материалы, которые пригодятся для выполнения задания

1. Описание [Pod](https://kubernetes.io/docs/concepts/workloads/pods/) и примеры манифестов.
2. Описание [Service](https://kubernetes.io/docs/concepts/services-networking/service/).

------

### Задание 1. Создать Pod с именем hello-world

1. Создать манифест (yaml-конфигурацию) Pod.
2. Использовать image - gcr.io/kubernetes-e2e-test-images/echoserver:2.2.
3. Подключиться локально к Pod с помощью `kubectl port-forward` и вывести значение (curl или в браузере).

### Ответ:

[Манифест пода](https://github.com/Lex-Chaos/kuber-02-hw/blob/main/files/pod-hello-world.yaml):

```
apiVersion: v1
kind: Pod
metadata:
  name: hello-world
  labels:
    app: hlwrld
spec:
  containers:
  - name: hello-world
    image: gcr.io/kubernetes-e2e-test-images/echoserver:2.2
    ports:
    - containerPort: 8080
```

Проброс порта:

![Проброс порта](https://github.com/Lex-Chaos/kuber-02-hw/blob/main/img/Task1-1.png)


Вывод браузера:

![Вывод браузера](https://github.com/Lex-Chaos/kuber-02-hw/blob/main/img/Task1-2.png)


------

### Задание 2. Создать Service и подключить его к Pod

1. Создать Pod с именем netology-web.
2. Использовать image — gcr.io/kubernetes-e2e-test-images/echoserver:2.2.
3. Создать Service с именем netology-svc и подключить к netology-web.
4. Подключиться локально к Service с помощью `kubectl port-forward` и вывести значение (curl или в браузере).

### Ответ:

[Манифест пода](https://github.com/Lex-Chaos/kuber-02-hw/blob/main/files/pod-netology-web.yaml):

```
apiVersion: v1
kind: Pod
metadata:
  name: netology-web
  labels:
    app: netology-web
spec:
  containers:
  - name: hello-world
    image: gcr.io/kubernetes-e2e-test-images/echoserver:2.2
```

[Манифест сервиса](https://github.com/Lex-Chaos/kuber-02-hw/blob/main/files/svc-netology-web.yaml):

```
apiVersion: v1
kind: Service
metadata:
  name: netology-svc
  namespace: default
spec:
  selector:
    app: netology-web
  ports:
  - protocol: TCP
    port: 8080
```

Созданные объекты:

![Объекты](https://github.com/Lex-Chaos/kuber-02-hw/blob/main/img/Task2-1.png)

Проброс порта:

![Проброс порта](https://github.com/Lex-Chaos/kuber-02-hw/blob/main/img/Task2-2.png)

Вывод браузера:

![Вывод браузера](https://github.com/Lex-Chaos/kuber-02-hw/blob/main/img/Task2-3.png)

------

### Правила приёма работы

1. Домашняя работа оформляется в своем Git-репозитории в файле README.md. Выполненное домашнее задание пришлите ссылкой на .md-файл в вашем репозитории.
2. Файл README.md должен содержать скриншоты вывода команд `kubectl get pods`, а также скриншот результата подключения.
3. Репозиторий должен содержать файлы манифестов и ссылки на них в файле README.md.

------

