# Практическая работа N3

Студент: Семин Матвей Романович  
Группа: ЭФБО-10-24

## Задание 1. Разрешение merge-конфликта

Были созданы две ветки:

- `conflict/readme-update-1`
- `conflict/readme-update-2`

При слиянии был получен конфликт в `README.md`. Финальная версия README объединяет оба варианта: содержит данные студента, описание проекта, стек и список файлов репозитория.

## Задание 2. Merge vs Rebase

После merge история содержала merge-коммит:

```text
*   9056838 merge: integrate feature A
|\  
| * f18dd4d docs: add details for feature A
| * ed409ba feat: add feature A description
|/  
```

После rebase/fast-forward история стала линейной:

```text
* f18dd4d docs: add details for feature A
* ed409ba feat: add feature A description
```

Разница: `merge` сохраняет факт параллельной разработки отдельным merge-коммитом, а `rebase` делает историю линейной и проще для чтения.

## Задание 3. Interactive Rebase / очистка истории

Грязная история до очистки:

```text
a23c65e oops
6854da5 add docs
d0c0b8b fix typo in subtract
6a6020f add subtract
9a70825 wip
c8d5f1b start calculator
```

Чистая история после переписывания:

```text
570ff0d docs: add calculator README
867533c feat: implement subtract function
d1c3556 feat: implement add function
```

Файл `calculator.py` содержит функции `add` и `subtract`, а исправление `# fixed` сохранено.

## Задание 4. Multi-Remote

Текущий remote:

```text
origin  https://github.com/MatuhaBtww/devops-course-2026.git
```

Для полного выполнения задания нужно создать второй пустой репозиторий-зеркало, например:

```text
git@github.com:MatuhaBtww/devops-course-2026-mirror.git
```

После создания mirror-репозитория команды будут такими:

```bash
git remote add mirror git@github.com:MatuhaBtww/devops-course-2026-mirror.git
git push mirror --all
git push mirror --tags
git remote set-url --add --push origin git@github.com:MatuhaBtww/devops-course-2026.git
git remote set-url --add --push origin git@github.com:MatuhaBtww/devops-course-2026-mirror.git
git remote -v
```

## Задание 5. Cherry-pick, Reflog, Revert

### Cherry-pick

В `main` перенесен только критический фикс:

```text
8aa4999 fix: critical bug in calculator
```

В `calculator.py` есть `IMPORTANT_FIX = True`, но нет экспериментальных функций `multiply` и `divide`.

### Reflog

Потерянный коммит был найден через reflog:

```text
76f582d HEAD@{1}: commit: feat: add very important data
```

Файл `important_data.md` был восстановлен во временной ветке `temp/recovered-branch`.

### Revert

Сломанный коммит был отменен безопасно через `git revert`:

```text
0e61bb9 Revert "feat: add new feature (accidentally broken)"
ce23d6a feat: add new feature (accidentally broken)
8aa4999 fix: critical bug in calculator
```

Строка `BROKEN_CODE = True` удалена из `calculator.py`, а история не переписана.
