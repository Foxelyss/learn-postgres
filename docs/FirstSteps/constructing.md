---
title: Построение моделей
nav_order: 3
layout: default
parent: Первые шаги
---

Модели БД - схематическое представление

Виды моделей(этапы проектирования):
1. Концептуальная

![Концептуальная модель](/assets/img/concept-1.png)

{:style="counter-reset:step-counter 1"}
1. Логическая(ER)
![ER diagram](/assets/img/er-diagram.png)

{:style="counter-reset:step-counter 2"}
1. Физическая(На базе СУБД)

Словарь данных:

| **KEY** | **FIELD NAME** | **DATA TYPE / FIELD SIZE** | **REQUIRED?** | **NOTES**                                              |
| ------- | -------------- | -------------------------- | ------------- | ------------------------------------------------------ |
| PK      | **Code**       | VARCHAR (6)                | Y             |                                                        |
|         | **LastName**   | VARCHAR (100)              | Y             |                                                        |
|         | **FirstName**  | VARCHAR (50)               | Y             |                                                        |
|         | **Patronymic** | VARCHAR (50)               | Y             |                                                        |
|         | **Gender**     | CHAR(1)                    | Y             | Check Constraint  <br>(Допускается только 'F' или 'M') |
|         | **Phone**      | VARCHAR (20)               | Y             |                                                        |
|         | **Email**      | VARCHAR (50)               | Y             |                                                        |

Код: 
```sql
create table client(
Code	VARCHAR (6) primary key,
LastName	VARCHAR (100) not null,
FirstName	VARCHAR (50) not null,
Patronymic	VARCHAR (50) not null
Gender	CHAR(1) not null check(Gender in ('F', 'M')),
Phone	VARCHAR (20) not null,
Email	VARCHAR (50) not null
);
```

-----------

Разновидности моделей БД(От первых, до реляционных, которые мы используем прямо сейчас):
1. Иерархическая<br> ![](/assets/img/hierarchy-1.png)
2. Сетевая <br>![](/assets/img/net-1.png)
3. Реляционная <br> ![](/assets/img/relational-1.png)
----------

Нормализация отношений(Нормальные формы - НФ) - приведение таблиц к определенному формату по средствам при помощи
правил и ограничений

Существует 8 нормальных форм.

Мы рассмотрим только первые 3 формы:
1. Таблица без повторяющихся строк и без каскадов(1 поле = одно значение)
Пример каскада: ФИО, (BMW X7, BMW X8)

2. Таблица должна быть в 1 нф, все неключевые столбцы должны зависеть от одного ключевого столбца

3. Таблица должна быть во 2 нф без повторов в значениях(К примеру два раза встречается "Иванов Иван", 
вместо этого должна быть одна запись в таблице, а все остальные должны на неё ссылаться)
Все столбцы зависят друг от друга или зависят от сущности
