# Домашнее задание к занятию «Хранение в K8s. Часть 2» - Филатов А. В.

### Цель задания

В тестовой среде Kubernetes нужно создать PV и продемострировать запись и хранение файлов.

------

### Чеклист готовности к домашнему заданию

1. Установленное K8s-решение (например, MicroK8S).
2. Установленный локальный kubectl.
3. Редактор YAML-файлов с подключенным GitHub-репозиторием.

------

### Дополнительные материалы для выполнения задания

1. [Инструкция по установке NFS в MicroK8S](https://microk8s.io/docs/nfs). 
2. [Описание Persistent Volumes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/). 
3. [Описание динамического провижининга](https://kubernetes.io/docs/concepts/storage/dynamic-provisioning/). 
4. [Описание Multitool](https://github.com/wbitt/Network-MultiTool).

------

### Задание 1

**Что нужно сделать**

Создать Deployment приложения, использующего локальный PV, созданный вручную.

1. Создать Deployment приложения, состоящего из контейнеров busybox и multitool.
2. Создать PV и PVC для подключения папки на локальной ноде, которая будет использована в поде.
3. Продемонстрировать, что multitool может читать файл, в который busybox пишет каждые пять секунд в общей директории. 
4. Удалить Deployment и PVC. Продемонстрировать, что после этого произошло с PV. Пояснить, почему.
5. Продемонстрировать, что файл сохранился на локальном диске ноды. Удалить PV.  Продемонстрировать что произошло с файлом после удаления PV. Пояснить, почему.
5. Предоставить манифесты, а также скриншоты или вывод необходимых команд.

### Решение 1

[data-sharing-deployment.yaml](https://github.com/v1us1885/k8s-2.2/blob/main/data-sharing-deployment.yaml)   
[local-pv.yaml](https://github.com/v1us1885/k8s-2.2/blob/main/local-pv.yaml)   
[local-pvc.yaml](https://github.com/v1us1885/k8s-2.2/blob/main/local-pvc.yaml)   

![alt text](Screenshot_1.png)   
![alt text](Screenshot_2.png)   
![alt text](Screenshot_3.png)   
![alt text](Screenshot_4.png)   

- После удаления PVC, PV останется в статусе Released, так как политика persistentVolumeReclaimPolicy установлена на Retain. Это означает, что данные на PV остаются, даже если PVC было удалено.
------

### Задание 2

**Что нужно сделать**

Создать Deployment приложения, которое может хранить файлы на NFS с динамическим созданием PV.

1. Включить и настроить NFS-сервер на MicroK8S.
2. Создать Deployment приложения состоящего из multitool, и подключить к нему PV, созданный автоматически на сервере NFS.
3. Продемонстрировать возможность чтения и записи файла изнутри пода. 
4. Предоставить манифесты, а также скриншоты или вывод необходимых команд.

### Решение 1

[deployment-nfs.yaml](https://github.com/v1us1885/k8s-2.2/blob/main/deployment-nfs.yaml)   
[nfs-pv.yaml](https://github.com/v1us1885/k8s-2.2/blob/main/nfs-pv.yaml)   
[nfs-pvc.yaml](https://github.com/v1us1885/k8s-2.2/blob/main/nfs-pvc.yaml)   
[storageclass-nfs.yaml](https://github.com/v1us1885/k8s-2.2/blob/main/storageclass-nfs.yaml)   

![alt text](Screenshot_5.png)   
![alt text](Screenshot_6.png)   

------

### Правила приёма работы

1. Домашняя работа оформляется в своём Git-репозитории в файле README.md. Выполненное задание пришлите ссылкой на .md-файл в вашем репозитории.
2. Файл README.md должен содержать скриншоты вывода необходимых команд `kubectl`, а также скриншоты результатов.
3. Репозиторий должен содержать тексты манифестов или ссылки на них в файле README.md.