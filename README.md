# data-company-files

Данные здесь синтетические. Имена, телефоны, почты и суммы выдуманы, домены взяты из зарезервированных под примеры (`example.com`, `example.ru`), совпадения с настоящими людьми и компаниями случайны.

Это папка, которую «компания передала как есть»: сорок файлов, накопленных вручную. Счета, банковские выписки, чеки, договоры, сканы, посторонние файлы и пять выгрузок контактов из разных источников. Имена файлов неочевидны, часть данных повторяется, форматы расходятся, а полезное прячется внутри файлов и по названию не угадывается. Набор сделан для учебного проекта Хекслета по автоматизации разбора файлов и годится для любой задачи, где нужен реалистичный беспорядок.

## Как получить

Клоном, без истории:

```sh
git clone --depth 1 https://github.com/hexlet-components/data-company-files.git
mv data-company-files/company-files company-files
rm -rf data-company-files
```

Набор лежит в подпапке репозитория, поэтому клон сам по себе кладёт его на уровень глубже, чем нужно, и папку достают наружу.

Архивом, если git не нужен, кнопка **Code → Download ZIP** на странице репозитория или напрямую:

```sh
curl -L -o company-files.zip https://github.com/hexlet-components/data-company-files/archive/refs/heads/main.zip
```

Архив разворачивается в папку `data-company-files-main/`, и набор лежит в ней как `data-company-files-main/company-files/`. Нужна только эта папка, остальное это обвязка самого репозитория.

## Что внутри

Тридцать четыре файла в корне набора и шесть во вложенной папке `Архив/`.

| Что | Файлы |
| --- | --- |
| Счета | `scheta-01-2025.csv` и ещё три месяца |
| Банковские выписки | `vypiska-yanvar.csv`, `vypiska-fevral.csv`, `vypiska-mart.csv` |
| Чеки | `cheki-komandirovka.csv`, `cheki-kanctovary.csv` |
| Договоры и заметки | три `dogovor-*.txt`, `zametki-po-dokumentam.md` |
| Выгрузки контактов | `kontakty-vebinar.csv`, `kontakty-crm.csv`, `anketa-konferencii.csv`, `crm-arhiv.json`, `Архив/kontakty-rassylka.csv` |
| Непарсимое | три pdf, два jpg, xlsx |
| Постороннее | `logotip.png`, `instrukciya.docx`, `.DS_Store`, `Thumbs.db`, пустой `pustaya-vygruzka.csv` |

Беспорядок в наборе намеренный, и каждый его вид отвечает за отдельное умение разбирающей программы.

- **Повторы.** `Копия scheta-01-2025.csv` и `scheta-01-2025 (1).csv` совпадают с оригиналом побайтово. `SCHETA-02-2025.CSV` и `scheta-02-2025 (1).csv` отличаются от `scheta-02-2025.csv` регистром имени и одной цифрой в содержимом, то есть по хешу они разные, а по смыслу тот же документ.
- **Имена врут.** У `rekvizity` расширения нет вовсе, и тип виден только по первым байтам. У `crm-arhiv.json` в имени нет слова «контакты», хотя это выгрузка контактов, а у счетов есть колонка «Контрагент», хотя контактов в них нет.
- **Форматы расходятся.** `kontakty-vebinar.csv` идёт с BOM и запятой, `kontakty-crm.csv` с точкой с запятой и своими названиями колонок, `crm-arhiv.json` вообще не таблица. Кодировка везде UTF-8.
- **Значения грязные.** Телефоны записаны четырьмя способами, часть имён в верхнем регистре или с лишними пробелами, в одной строке вместо телефона стоит «не указан», а одна запись не несёт ни телефона, ни почты.
- **Вложенность.** Пятая выгрузка контактов лежит в `Архив/`, поэтому программа, которая не заходит в подпапки, теряет и документы, и людей.

## Проверка набора

```sh
make test
```

Считает файлы, ловит кодировку кроме UTF-8 и проверяет, что ловушки на месте. Нужна, когда набор правят: пропавшая ловушка снаружи неотличима от целого набора.

---

[![Hexlet Ltd. logo](https://raw.githubusercontent.com/Hexlet/assets/master/images/hexlet_logo128.png)](https://hexlet.io/?utm_source=github&utm_medium=link&utm_campaign=data-company-files)

This repository is created and maintained by the team and the community of Hexlet, an educational project. [Read more about Hexlet](https://hexlet.io/pages/about?utm_source=github&utm_medium=link&utm_campaign=data-company-files).
