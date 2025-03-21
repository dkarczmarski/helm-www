---
title: "Локалізація документації Helm"
description: "Інструкції для локалізації документації Helm."
weight: 5
---

Цей посібник пояснює, як локалізувати документацію Helm.

## Початок роботи {#getting-started}

Внесення змін у переклади використовує той самий процес, що й внесення змін у документацію. Переклади подаються через [пул-реквести](https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/about-pull-requests) до репозиторію [helm-www](https://github.com/helm/helm-www), і пул-реквести перевіряються командою, яка управляє вебсайтом.

### Дволітерний код мови {#two-letter-language-code}

Документація організована відповідно до стандарту [ISO 639-1](https://www.loc.gov/standards/iso639-2/php/code_list.php) для мовних кодів. Наприклад, дволітерний код для корейської мови — `ko`, української — `uk`.

У контенті та конфігураціях ви знайдете використовувані мовні коди. Ось 3 приклади:

- У теці `content` мовні коди використовуються як підтеки, і локалізований контент для кожної мови знаходиться в кожній теці, переважно в підтеці `docs` кожної теки мовного коду.
- Тека `i18n` містить конфігураційний файл для кожної мови з фразами, що використовуються на вебсайті. Файли називаються за шаблоном `[LANG].toml`, де `[LANG]` — це дволітерний код мови.
- У конфігураційному файлі верхнього рівня `config.toml` є конфігурація для навігації та інших деталей, організованих за мовним кодом.

Англійська мова, з мовним кодом `en`, є стандартною мовою та джерелом для перекладів.

### Форк, Гілка, Зміна, Пул-Реквест {#fork-branch-change-pull-request}

Щоб зробити переклад, почніть зі [створення форку](https://help.github.com/en/github/getting-started-with-github/fork-a-repo) репозиторію [helm-www](https://github.com/helm/helm-www) на GitHub. Ви почнете з внесення змін у вашому форку.

Стандартно ваш форк буде налаштовано на роботу з основною гілкою, відомою як `main`. Будь ласка, використовуйте гілки для розробки ваших змін та створення пул-реквестів. Якщо ви не знайомі з гілками, ви можете [прочитати про них у документації GitHub](https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/about-branches).

Коли у вас зʼявиться гілка, внесіть зміни для додавання перекладів та локалізації контенту потрібною мовою.

Зверніть увагу, що Helm використовує [Developers Certificate of Origin](https://developercertificate.org/). Всі коміти повинні мати підпис. При виконанні коміту ви можете використовувати прапорець `-s` або `--signoff`, щоб використовувати ваше налаштоване імʼя та адресу електронної пошти для підпису коміту. Більше деталей можна знайти у файлі [CONTRIBUTING.md](https://github.com/helm/helm-www/blob/main/CONTRIBUTING.md#sign-your-work).

Коли ви будете готові, створіть [пул-реквест](https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/about-pull-requests) з перекладом назад до репозиторію helm-www.

Після створення пул-реквесту один з підтримувачів перевірить його. Деталі цього процесу можна знайти у файлі [CONTRIBUTING.md](https://github.com/helm/helm-www/blob/main/CONTRIBUTING.md).

## Переклад Контенту {#translating-content}

Локалізація всього контенту Helm є великою задачею. Добре почати з малого. Переклади можуть розширюватися з часом.

### Переклади новою мовою {#starting-a-new-language}

Коли ви починаєте переклад новою мовою, є необхідний мінімум. Він включає:

- Додавання теки `content/[LANG]/docs`, що містить файл `_index.md`. Це головна сторінка документації для мови.
- Створення файлу `[LANG].toml` в теці `i18n`. Спочатку ви можете скопіювати файл `en.toml` як відправну точку.
- Додавання розділу для мови до файлу `config.toml`, щоб відкрити новий мовний розділ. Наявні мовні розділи можуть слугувати відправною точкою.

### Переклад {#translation}

Перекладений контент має знаходитися в теці `content/[LANG]/docs`. Він повинен мати ту ж URL-адресу, що й англійське джерело. Наприклад, для перекладу вступу на корейську мову може бути корисно скопіювати англійське джерело як:

```sh
mkdir -p content/ko/docs/intro
cp content/en/docs/intro/install.md content/ko/docs/intro/install.md
```

Контент у новому файлі може бути перекладено іншою мовою.

Не додавайте неперекладену копію англійського файлу в `content/[LANG]/`. Як тільки мова існує на сайті, будь-які неперекладені сторінки автоматично перенаправлятимуться на англійську версію. Переклад займає час, і ви завжди хочете перекладати найактуальнішу версію документації, а не застарілу версію.

Переконайтеся, що ви видалили будь-які рядки `aliases` з розділу заголовка. Рядка на зразок `aliases: ["/docs/using_helm/"]` не має бути в перекладах. Це перенаправлення для старих посилань, які не існують для нових сторінок.

Зверніть увагу, що інструменти для перекладу можуть допомогти в процесі. Це включає автоматично згенеровані переклади. Автоматично згенеровані переклади повинні бути переглянути та перевірені носієм мови перед публікацією.

## Навігація між мовами {#navigation-between-languages}

![Скріншот 2020-05-11 о 11 24 22
AM](https://user-images.githubusercontent.com/686194/81597103-035de600-937a-11ea-9834-cd9dcef4e914.png)

Глобальний файл [config.toml](https://github.com/helm/helm-www/blob/main/config.toml#L83L89) є місцем, де налаштована навігація між мовами.

Щоб додати нову мову, додайте новий набір параметрів, використовуючи [дволітерний мовний код](./localization/#two-letter-language-code), визначений вище. Приклад:

```toml
# Korean
[languages.ko]
title = "Helm"
description = "Helm - The Kubernetes Package Manager."
contentDir = "content/ko"
languageName = "한국어 Korean"
weight = 1
```

## Розвʼязання внутрішніх посилань {#resolving-internal-links}

Перекладений контент іноді міститиме посилання на сторінки, які існують тільки в іншій мові. Це призведе до [помилок збірки сайту](https://app.netlify.com/sites/helm-merge/deploys). Приклад:

```
12:45:31 PM: htmltest started at 12:45:30 on app
12:45:31 PM: ========================================================================
12:45:31 PM: ko/docs/chart_template_guide/accessing_files/index.html
12:45:31 PM:   hash does not exist --- ko/docs/chart_template_guide/accessing_files/index.html --> #basic-example
12:45:31 PM: ✘✘✘ failed in 197.566561ms
12:45:31 PM: 1 error in 212 documents
```

Щоб вирішити це, потрібно перевірити ваш контент на наявність внутрішніх посилань.

- посилання-якоря повинні відображати перекладене значення `id`
- внутрішні посилання на сторінки потрібно виправити

Для внутрішніх сторінок, які не існують _(або ще не були перекладені)_, сайт не збереться до тих пір, поки не буде внесено виправлення. Як альтернативний варіант, URL може вказувати на іншу мову, де цей контент _існує_, наступним чином:

`< relref path="/docs/topics/library_charts.md" lang="en" >`

Дивіться [документацію Hugo про перехресні посилання між
мовами](https://gohugo.io/content-management/cross-references/#link-to-another-language-version) для докладнішої інформації.
