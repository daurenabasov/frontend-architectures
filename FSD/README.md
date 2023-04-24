# FEATURES-SLICES-DESIGN

- В первую очерель разделим 3 такиз понятия как:

1. Слой
2. Слайс [ модуль ]
3. Сегмент

```sh
└── src/
    ├── app/                    # Инициализирующая логика приложения
    |                           #
    ├── processes/              # (ОПЦ.) Процессы приложения протекающие над страницами
    |   ├── {some-process}/     #     Slice: (e.g. CartPayment process)
    |   |   ├── lib/            #         Segment: Infrastructure-logic (helpers/utils)
    |   |   └── model/          #         Segment: Business Logic
    |   ...                     #
    |                           #
    ├── pages/                  # Страницы приложения
    |   ├── {some-page}/        #     Slice: (e.g. ProfilePage page)
    |   |   ├── lib/            #         Segment: Infrastructure-logic (helpers/utils)
    |   |   ├── model/          #         Segment: Business Logic
    |   |   └── ui/             #         Segment: UI logic
    |   ...                     #
    |                           #
    ├── widgets/                # Самостоятельные и полноценные блоки для страниц
    |   ├── {some-widget}/      #     Slice: (e.g. Header widget)
    |   |   ├── lib/            #         Segment: Infrastructure-logic (helpers/utils)
    |   |   ├── model/          #         Segment: Business Logic
    |   |   └── ui/             #         Segment: UI logic
    ├── features/               # (ОПЦ.) Обрабатываемые пользовательские сценарии
    |   ├── {some-feature}/     #     Slice: (e.g. AuthByPhone feature)
    |   |   ├── lib/            #         Segment: Infrastructure-logic (helpers/utils)
    |   |   ├── model/          #         Segment: Business Logic
    |   |   └── ui/             #         Segment: UI logic
    |   ...                     #
    |                           #
    ├── entities/               # (ОПЦ.) Бизнес-сущности, которые оперирует предметную   область
    |   ├── {some-entity}/      #     Slice: (e.g. entity User)
    |   |   ├── lib/            #         Segment: Infrastructure-logic (helpers/utils)
    |   |   ├── model/          #         Segment: Business Logic
    |   |   └── ui/             #         Segment: UI logic
    |   ...                     #
    |                           #
    ├── shared/                 # Переиспользуемые модули, без привязки к бизнес-логике
    |   ├── api/                #         Segment: Logic of API requests
    |   ├── config/             #         Segment: Application configuration
    |   ├── lib/                #         Segment: Infrastructure-application logic
    |   └── ui/                 #         Segment: UIKit of the application
    |   ...                     #
    |                           #
    └── index.tsx/              #
```

# ==== Слой ====

- Слоев по этой методологией строго ограниченное кол-ство их 7 штук

1. app
2. process
3. pages
4. widgets
5. features
6. etites
7. shared

- часть из этих слоев является опциональными, то есть не обязательными
- каждый слой имеет свою зону отвественности (здесь слои бизнес ориентированны)
- etites - сущности; features; widgets

- здесь иерархия тоже ступенчатая, то есть entity не может использовать features, фичи не могут виджеты (то есть здесь выше лежащие слои строго могут использовать ниже лежащие, то есть фича не может использовать другую фичу )
- мы используем только нижележащий слои для того чтобы получить линейный поток данных

# ==== SLICES ====

### Каждый слой содержит слайс так называемые модули ()

# entites

- entites это конкретно бизнес-сущности: пользователь, статься, продукт, документ, комментарий

- И каждый из таких модулей содержит в себе сегменты (все те же api, component, constants, helpers)

- Но тут уже привязка идет не абстрактно каким то глобальным моментом а конкретно к бизнес сущностям( запросы которые относятся к пользователям, запросы которые относятся к товару, helpers которые относятся к товару и т.д )

# Features

- это модули которые несут какую то бизнес ценность ( форма отправи фидбека, регистрация или авторизация по телефону, изменения номера и т.д )

- в себя они могут использовать как shared так и entities

# Виджеты

- Представлюят из себя максимально самостоятельно и насколько это возможно компоненты
- В первую очередеть они могут использовать фичи (примеру header, navbar, sidebar [ при том же хедер может внутри себя содержать куча разных фичей (открытия уведомлений, открытие dropdowns, для перехода на страницу профиля , ссылки и т.д. Также карточки поста ) ])

# ==== Сегменты ====

#### Слайсы внутри себя содержат сегменты

- UI
- MODEL
- LIB
- CONFIG
- API
- CONSTS

# UI

- Это наши компоненты

# MODEL

- Это наша бизнес-логика
- Взаимодействие со стэйтом
- Селекторы
- Экшены

# LIB

- Наши helpers

# CONFIG

- Редко встречающийся сегмент
- Какая то конфигурация нашего модуля если она требуется

# API

- Это запросы на сервер, который требуется для данного модуля

# CONSTS

- Константы которые нужно в конкретном модуле

===============

- Как мы выяснили поток у нас однонаправленный сверху вниз

[пример проекта](https://github.com/NIRumiantsev/feature-sliced-design)
