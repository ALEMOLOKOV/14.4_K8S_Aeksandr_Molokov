# 14.4_K8S_Aeksandr_Molokov

### Задание 1. Выбрать стратегию обновления приложения и описать ваш выбор

1. Имеется приложение, состоящее из нескольких реплик, которое требуется обновить.
2. Ресурсы, выделенные для приложения, ограничены, и нет возможности их увеличить.
3. Запас по ресурсам в менее загруженный момент времени составляет 20%.
4. Обновление мажорное, новые версии приложения не умеют работать со старыми.
5. Вам нужно объяснить свой выбор стратегии обновления приложения.

### Ответ

Так как нет возможности увеличить ресурсы остается выбрать из стратегий Rolling update и Recreate (остальные стратегии обновления предполагают развертывание сразц двух версий, что влечет за собой згачительно увеличение необходимых ресурсов). Исходя из условий, я бы предложил стратегию обновления Rolling update.
При данной стратегии обновления приложение останется доступным, даже при неудачном обновлении и легко можно будет откатить обновление. 
Запас ресурсов в менее загруженный момент времени 20% - соответсвенно Recreate отпадает т.к. приложеие постоянно находиться под нагрузкой и нет возможности его остановить для обновления.
При правильно выставленных параметрах обновления запаса хватит для того чтобы обносить приложение не перегрузив систему вцелом.

### Задание 2. Обновить приложение

1. Создать deployment приложения с контейнерами nginx и multitool. Версию nginx взять 1.19. Количество реплик — 5.
2. Обновить версию nginx в приложении до версии 1.20, сократив время обновления до минимума. Приложение должно быть доступно.
3. Попытаться обновить nginx до версии 1.28, приложение должно оставаться доступным.
4. Откатиться после неудачного обновления.

### Ответ

![Deployment]()

#### ВМ YandexCloud кластер развернут с помощью kubespray 
![yandexcloude vm](https://github.com/ALEMOLOKOV/14.4_K8S_Aeksandr_Molokov/assets/109212419/2e9a9f30-7a63-4ac0-8052-9f1ee0eec6a7)

#### Кластер развернут
![cluster OK](https://github.com/ALEMOLOKOV/14.4_K8S_Aeksandr_Molokov/assets/109212419/789ef34d-ed0f-4960-9403-89842f5960a1)

#### Deployment с версией  nginx 1.19
![pods up](https://github.com/ALEMOLOKOV/14.4_K8S_Aeksandr_Molokov/assets/109212419/5c29d2fb-2b37-4923-9ba5-b85a061133f9)

#### Обновление версии до 1.20 стратегия Rolling-update т.к. в условии сказано что приложение должно быть доступно, параметры maxSurge: 4 и maxUnavailable: 4 - для максимально быстрого обновления
![update version till 1 20](https://github.com/ALEMOLOKOV/14.4_K8S_Aeksandr_Molokov/assets/109212419/6ac6cc69-e92f-4b23-b975-b3fee4407f3e)

![1 20 update 1 pod working](https://github.com/ALEMOLOKOV/14.4_K8S_Aeksandr_Molokov/assets/109212419/bd27882a-554c-4f0b-b554-b688a47b904b)

#### Попытка обновления до версии 1.28
![update 1 28](https://github.com/ALEMOLOKOV/14.4_K8S_Aeksandr_Molokov/assets/109212419/e6266bd7-3904-4a8d-9c3a-2dbe080b32aa)

![статус после неудачного обновления](https://github.com/ALEMOLOKOV/14.4_K8S_Aeksandr_Molokov/assets/109212419/f22ca57e-232a-4190-8f92-2cf150b2ac00)

#### Откат обновления
![откат обновления](https://github.com/ALEMOLOKOV/14.4_K8S_Aeksandr_Molokov/assets/109212419/3878c99b-7339-4e97-ac9d-d430e542d2a6)

#### Статус посде отката
![статус после отката](https://github.com/ALEMOLOKOV/14.4_K8S_Aeksandr_Molokov/assets/109212419/c74dd86c-4a59-4a2d-8511-27f1e09e2cd6)



