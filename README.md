# sql-query-practice
*Практика составления SQL-запросов, выполненная в рамках курса Надежды Дудник ProTestingInfo https://protestinginfo.ru/*

![sql-1](https://github.com/user-attachments/assets/7ea3efe8-4482-4cab-be85-e7af3d3193bf)

![sql-2](https://github.com/user-attachments/assets/e027e06a-4fc6-496f-b6e0-a4afd484541c)

![sql-3](https://github.com/user-attachments/assets/0292be43-489d-43f0-969e-9baed4565026)

### Задания

1. Вывести всех сотрудников с ролью 'Tester'

**Ответ**
```sql
SELECT employeeName FROM employees
WHERE roleEmployee = 'Tester';
```

2. Вывести заказчиков, у которых длительность проекта больше средней

**Ответ**
```sql
SELECT productOwner FROM projects
WHERE duration > (SELECT AVG(duration) FROM projects);
```

3. Вывести список всех сотрудников, заменив в значениях phone все '-' на '.'

**Ответ**
```sql
SELECT empId, employeeName, roleEmployee, place, REPLACE(phone, '-', '.')
FROM Employees;
```

4. Получить отчет по сотрудникам с минимальной и максимальной загрузкой. Сортировать по максимальной загрузке по убыванию

**Ответ**
```sql
SELECT employeeName, MIN(workload) AS minWorkload, MAX(workload) AS maxWorkload
FROM Works
GROUP BY employeeName
ORDER BY maxWorkload DESC;
```

5. Обновить данные для проекта с projectId равным 4 , проставить наименование заказчика с "External" на "Internal"

**Ответ**
```sql
UPDATE projects
SET productOwner = 'Internal'
WHERE projectId = 4;
```

6. Сгруппировать по названиям проектов и найти все группы, для которых определена общая сумма объема работы более 30%

**Ответ**
```sql
SELECT projectName, SUM(workload) AS totalWorkload FROM Works
GROUP BY projectName
HAVING SUM(workload) > 30;
```

7. Вывести количество номеров телефонов сотрудников, у которых есть телефон

**Ответ**
```sql
SELECT COUNT(phone) FROM Employees WHERE phone IS NOT NULL;
```

8. Посчитать количество сотрудников на проектах с длительностью от 2-х до 10-ти месяцев

**Ответ**
```sql
SELECT COUNT(workId) FROM Works AS w
JOIN Projects AS pr On w.projectname = pr.projectname
WHERE duration BETWEEN 2 and 10;
```

9. Вывести место сотрудника, где встречается цифра "6" в месте сотрудника, и сотрудник работает 2 месяца

**Ответ**
```sql
SELECT place FROM Employees AS e
JOIN Works AS w ON e.employeeName = w.employeeName
JOIN Projects AS pr ON w.projectName = pr.projectName
WHERE place LIKE '%6%' AND duration = 2;
```
