1. Даны две таблицы в PostgresSQL - таблица статей и таблица комментариев к этим статьям 

Необходимо написать запрос, который выведет все статьи без комментариев (у которых нет комментариев)

Таблицы тут: http://sqlfiddle.com/#!17/84c62 (Или тут https://www.db-fiddle.com/f/kGzmoWLCRkQ9mzHM83u2vT/0)

Предполагаю 2 варианта запросов через вложенный запрос с exists и через join.

```sql
select * from article a
where not exists (select 1 from "comment" c where a.id = c.article_id);
```

```sql
select * from article a 
left join "comment" c on a.id = c.article_id
where article_id is null;
```

2. На входе есть такие записи выполненных часов работниками
(по дням, дни можно опустить - они не имеют значения):

```python
from collections import defaultdict

# Входные данные
data = """
Андрей 9
Василий 11
Роман 7
X Æ A-12 45
Иван Петров 3
Андрей 6
Роман 11
"""


def print_calculate_total_hours(info_about_employees: str) -> None:
    hours_by_employee = defaultdict(list)

    for employer in info_about_employees.splitlines():
        space_index = employer.rfind(' ')
        if space_index != -1:
            name = employer[:space_index]
            hours = int(employer[space_index + 1:])
            hours_by_employee[name].append(hours)

    for name, hours in hours_by_employee.items():
        hours_list = ", ".join(map(str, hours))
        print(f"{name}: {hours_list}; sum: {sum(hours)}")


print_calculate_total_hours(data)
```


