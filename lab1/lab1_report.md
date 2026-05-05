---
University: [ITMO University](https://itmo.ru/ru/)
Faculty: [FICT](https://fict.itmo.ru)
Course: [Введение в веб технологии](https://itmo-ict-faculty.github.io/introduction-in-web-tech/)
Year: 2025/2026
Group: U4125
Author: Ganin Mikhail Aleksandrovich
Lab: Lab1
Date of create: 05.05.2026
Date of finished: 05.05.2026
---

# Лабораторная работа №1
## Обзор Google Cloud и исследование основных сервисов

## Цель работы
Ознакомиться с основными возможностями и преимуществами облачной платформы Google Cloud, научиться создавать сервисные аккаунты, управлять ролями IAM, создавать виртуальные машины в режиме Spot, работать с Cloud Storage через утилиту gsutil.

## Ход работы

### 1. Получение доступа к Google Cloud
Заполнена Google-форма с указанием Gmail почты. Получен доступ к проекту в GCP.

### 2. Создание Service Account
В разделе IAM & Admin → Service Accounts создан сервисный аккаунт:

| Параметр | Значение |
|----------|----------|
| Имя | mganin-sa-lab1 |
| Роль | Storage Admin |

![Создание сервисного аккаунта](img1.png)

### 3. Создание виртуальной машины
В разделе Compute Engine → VM instances создана VM:

| Параметр | Значение |
|----------|----------|
| Имя | mganin-vm-lab1 |
| Тип машины | e2-micro |
| Режим | Spot VM |
| ОС | Debian 11 |

![Создание VM](img2.png)

### 4. Подключение к VM
Через веб-интерфейс GCP нажата кнопка SSH. Подключение успешно.

### 5. Копирование файлов из бакета
Выполнены команды:

Просмотр содержимого бакета
gsutil ls gs://lab1-bucket-itmo/

Копирование файлов
gsutil cp gs://lab1-bucket-itmo/* .

### 6. Просмотр файлов на VM
ls -lah
Результат: три файла (pic1.jpg, pic1.jpg, pic1.jpg) успешно скопированы.

![Копирование файлов и их вывод](img3.png)

### 7. Изменение роли сервисного аккаунта
В разделе IAM роль изменена:

Было: Storage Admin

Стало: Compute Viewer

![Изменение роли](img4.png)

### 8. Проверка доступа после смены роли
Повторная попытка копирования:

gcloud cp gs://lab1-bucket-itmo/* .
Результат: ошибка AccessDeniedException (403)

![Ошибка AccessDeniedException (403)](img5.png)

# Вывод

Роль Storage Admin даёт доступ к бакету, а роль Compute Viewer — нет.
Система IAM Google Cloud работает по принципу наименьших привилегий.