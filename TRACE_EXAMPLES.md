# Пять конкретных примеров и трассы

Трасса записана по шагам `forward`, завершённым именам и откатам, а не по каждому токену. Параметры были зафиксированы до оценки.
## 1. ID 754, world_1, debug

Вопрос: What are the countries where either English or Dutch is the official language ?

**Эталон:**

```sql
select country.name from country join countrylanguage on country.code = countrylanguage.countrycode where countrylanguage.language = 'english' and isofficial = 't' union select country.name from country join countrylanguage on country.code = countrylanguage.countrycode where countrylanguage.language = 'dutch' and isofficial = 't'
```

**IterGen:**

```sql
SELECT c.code, c.name, c.continent, c.region, c.surfacearea, c.indepyear, c.population, c.lifeexpectancy, c.gnp, c.gnpold, c.localname, c.governmentform, c.headofstate, c.capital, c.code2 FROM country c JOIN countrylanguage cl ON c.code = cl.countrycode WHERE cl.isofficial =1 OR cl.isofficial =0;
```

Результат: результат совпал с эталоном на текущей базе. Статус: `stopped`; причина: `EosTokenCriteria`; откатов: 0; сгенерировано токенов: 94.

**Обычная генерация:**

```sql
SELECT c.code, c.name, c.continent, c.region, c.surfacearea, c.indepyear, c.population, c.lifeexpectancy, c.gnp, c.gnpold, c.localname, c.governmentform, c.headofstate, c.capital, c.code2 FROM country c JOIN countrylanguage cl ON c.code = cl.countrycode WHERE cl.isofficial = '1' OR cl.isofficial = '0';
```

**SynCode:**

```sql
SELECT c2_code, c2_name, c2_continent, c2_region, c2_surfacearea, c2_indepyear, c2_population, c2_lifeexpectancy, c2_gnp, c2_gnpold, c2_localname, c2_governmentform, c2_headofstate, c2_capital, c2_code2 FROM country WHERE c2_code IN (     SELECT code2     FROM countrylanguage     WHERE language = 'English'     OR language = 'Dutch' ) ORDER BY c2_code;
```

### Последовательность проверок

- Шаг 1: `column_name` = `c.code`; проверка пройдена; действие `continue`.

- Шаг 2: `column_name` = `c.name`; проверка пройдена; действие `continue`.

- Шаг 3: `column_name` = `c.continent`; проверка пройдена; действие `continue`.

- Шаг 4: `column_name` = `c.region`; проверка пройдена; действие `continue`.

- Шаг 5: `column_name` = `c.surfacearea`; проверка пройдена; действие `continue`.

- Шаг 6: `column_name` = `c.indepyear`; проверка пройдена; действие `continue`.

- Шаг 7: `column_name` = `c.population`; проверка пройдена; действие `continue`.

- Шаг 8: `column_name` = `c.lifeexpectancy`; проверка пройдена; действие `continue`.

- Шаг 9: `column_name` = `c.gnp`; проверка пройдена; действие `continue`.

- Шаг 10: `column_name` = `c.gnpold`; проверка пройдена; действие `continue`.

- Шаг 11: `column_name` = `c.localname`; проверка пройдена; действие `continue`.

- Шаг 12: `column_name` = `c.governmentform`; проверка пройдена; действие `continue`.

- Шаг 13: `column_name` = `c.headofstate`; проверка пройдена; действие `continue`.

- Шаг 14: `column_name` = `c.capital`; проверка пройдена; действие `continue`.

- Шаг 15: `column_name` = `c.code2`; проверка пройдена; действие `continue`.

- Шаг 16: `table_name` = `country`; проверка пройдена; действие `continue`.

**Разбор.** Запрос оказался правильным без откатов,поэтому этот случай не доказывает пользу отката.

## 2. ID 580, student_transcripts_tracking, debug

Вопрос: What other details can you tell me about students in reverse alphabetical order?

**Эталон:**

```sql
select other_student_details from students order by other_student_details desc
```

**IterGen:**

```sql
SELECT DISTINCT s.first_name, s.middle_name, s.last_name, s.cell_mobile_number, s.email_address, s.ssn, s.date_first_registered, s.date_left, s.other_student_details FROM students ORDER BY s.other_student_details ASC;
```

Результат:<br>
SQL не исполняется: no such column: s.first_name. Статус: `stopped`; причина: `EosTokenCriteria`; откатов: 0; сгенерировано токенов: 55.

**Обычная генерация:**

```sql
SELECT DISTINCT s.first_name, s.middle_name, s.last_name, s.cell_mobile_number, s.email_address, s.ssn, s.date_first_registered, s.date_left, s.other_student_details FROM students s WHERE s.other_student_details IS NOT NULL ORDER BY s.other_student_details ASC;
```

**SynCode:**

```sql
SELECT DISTINCT s.OTHER_STUDENT_DETAILS, s.OTHER_ADDRESS_DETAILS, s.OTHER_DEGREE_DETAILS, s.OTHER_COURSE_DETAILS, s.OTHER_SEMESTER_DETAILS, s.OTHER_DEGREE_PROGRAM_DETAILS, s.OTHER_TRANSCRIPT_DETAILS, s.OTHER_TRANSCRIPT_CONTENT_DETAILS, s.OTHER_DEGREE_PROGRAM_DETAILS, s.OTHER_TRANSCRIPT_CONTENT_DETAILS, s.OTHER_TRANSCRIPT_CONTENT_DETAILS, s.OTHER_TRANSCRIPT_CONTENT_DETAILS, s.OTHER_TRANSCRIPT_CONTENT_DETAILS, s.OTHER_TRANSCRIPT_CONTENT_DETAILS, s.OTHER_TRANSCRIPT_CONTENT_DETAILS, s.OTHER_TRANSCRIPT_CONTENT_DETAILS, s.OTHER_TRANSCRIPT_CONTENT_DETAILS, s.OTHER_TRANSCRIPT_CONTENT_DETAILS, s.OTHER_TRANSCRIPT_CONTENT_DETAILS, s.OTHER_TRANSCRIPT_CONTENT_DETAILS, s.OTHER_TRANSCRIPT_CONTENT_DETAILS, s.OTHER_TRANSCRIPT_CONTENT_DETAILS, s.OTHER_TRANSCRIPT_CONTENT_DETAILS, s.OTHER_TRANSCRIPT_CONTENT_DETAILS, s.OTHER_TRANSCRIPT_CONTENT_DETAILS, s.OTHER
```

### Последовательность проверок

- Шаг 1: `column_name` = `s.first_name`; проверка пройдена; действие `continue`.

- Шаг 2: `column_name` = `s.middle_name`; проверка пройдена; действие `continue`.

- Шаг 3: `column_name` = `s.last_name`; проверка пройдена; действие `continue`.

- Шаг 4: `column_name` = `s.cell_mobile_number`; проверка пройдена; действие `continue`.

- Шаг 5: `column_name` = `s.email_address`; проверка пройдена; действие `continue`.

- Шаг 6: `column_name` = `s.ssn`; проверка пройдена; действие `continue`.

- Шаг 7: `column_name` = `s.date_first_registered`; проверка пройдена; действие `continue`.

- Шаг 8: `column_name` = `s.date_left`; проверка пройдена; действие `continue`.

- Шаг 9: `column_name` = `s.other_student_details`; проверка пройдена; действие `continue`.

- Шаг 10: `table_name` = `students`; проверка пройдена; действие `continue`.

- Шаг 11: `column_name` = `s.other_student_details`; проверка пройдена; действие `continue`.

**Разбор.** Механизм остановки сработал, но SQL остался неверным, статус остановки не заменяет проверку выполнения.

## 3. ID 456, wta_1, debug

Вопрос: What are the full names of all players, sorted by birth date?

**Эталон:**

```sql
select first_name , last_name from players order by birth_date asc
```

**IterGen:**

```sql
SELECT p.first_name, p.last_name, p.birth_date FROM players AS p JOIN matches AS m ON p.player_id = m.loser_id JOIN rankings AS r ON p.player_id = r.player_id WHERE m.loser_id = p.player_id ORDER BY p.birth_date;
```

Результат:<br>
SQL исполняется, но результат отличается от эталона. Статус: `stopped`; причина: `EosTokenCriteria`; откатов: 2; сгенерировано токенов: 74.

**Обычная генерация:**

```sql
SELECT p.first_name, p.last_name, p.birth_date FROM players p ORDER BY p.birth_date;
```

**SynCode:**

```sql
SELECT p1.first_name, p1.last_name, p1. birth_date FROM players AS p1 JOIN matches AS m ON m.loser_id = p1. player_id JOIN rankings AS r ON r. player_id = p1. player_id WHERE r. ranking_date > '2024-01-01' ORDER BY p1. birth_date;
```

### Последовательность проверок

- Шаг 1: `column_name` = `p.first_name`; проверка пройдена; действие `continue`.

- Шаг 2: `column_name` = `p.last_name`; проверка пройдена; действие `continue`.

- Шаг 3: `column_name` = `p.birth_date`; проверка пройдена; действие `continue`.

- Шаг 4: `table_name` = `players`; проверка пройдена; действие `continue`.

- Шаг 5: `table_name` = `matches`; проверка пройдена; действие `continue`.

- Шаг 6: `column_name` = `p.player_id`; проверка пройдена; действие `continue`.

- Шаг 7: `column_name` = `m.loser_id`; проверка пройдена; действие `continue`.

- Шаг 8: `table_name` = `rankings`; проверка пройдена; действие `continue`.

- Шаг 9: `column_name` = `p.player_id`; проверка пройдена; действие `continue`.

- Шаг 10: `column_name` = `r.player_id`; проверка пройдена; действие `continue`.

- Шаг 11: `column_name` = `m.loser_id`; проверка пройдена; действие `continue`.

- Шаг 12: `column_name` = `db_id`; проверка не пройдена; действие `backward_column_name`.

До отката:

```sql
SELECT p.first_name, p.last_name, p.birth_date
FROM players AS p
JOIN matches AS m ON p.player_id = m.loser_id
JOIN rankings AS r ON p.player_id = r.player_id
WHERE m.loser_id = db_id
ORDER
```

После отката:

```sql
SELECT p.first_name, p.last_name, p.birth_date
FROM players AS p
JOIN matches AS m ON p.player_id = m.loser_id
JOIN rankings AS r ON p.player_id = r.player_id
WHERE m.loser_id =
```

- Шаг 13: `column_name` = `wta_1`; проверка не пройдена; действие `backward_column_name`.

До отката:

```sql
SELECT p.first_name, p.last_name, p.birth_date
FROM players AS p
JOIN matches AS m ON p.player_id = m.loser_id
JOIN rankings AS r ON p.player_id = r.player_id
WHERE m.loser_id = wta_1
ORDER
```

После отката:

```sql
SELECT p.first_name, p.last_name, p.birth_date
FROM players AS p
JOIN matches AS m ON p.player_id = m.loser_id
JOIN rankings AS r ON p.player_id = r.player_id
WHERE m.loser_id =
```

- Шаг 14: `column_name` = `p.player_id`; проверка пройдена; действие `continue`.

- Шаг 15: `column_name` = `p.birth_date`; проверка пройдена; действие `continue`.

**Разбор.** Проверки существования имён не поймали смысловую ошибку: наличие таблиц и столбцов не проверяет необходимую семантику.

## 4. ID 872, network_1, eval

Вопрос: Show the ID of the high schooler named Kyle.

**Эталон:**

```sql
select id from highschooler where name = 'Kyle'
```

**IterGen:**

```sql
SELECT id FROM highschooler WHERE name = 'Kyle';
```

Результат:<br> 
результат совпал с эталоном на текущей базе. Статус: `stopped`; причина: `EosTokenCriteria`; откатов: 2; сгенерировано токенов: 21.

**Обычная генерация:**

```sql
SELECT db_id FROM db_info WHERE name = 'Kyle';
```

**SynCode:**

```sql
SELECT db_id FROM db_info WHERE name = 'Kyle'
```

**Абляция с двумя откатами:**

```sql
SELECT id FROM
```

Статус `backtrack_limit`, откатов 2; SQL не исполняется: incomplete input.

### Последовательность проверок

- Шаг 1: `column_name` = `db_id`; проверка не пройдена; действие `backward_column_name`.

До отката:

```sql
SELECT db_id FROM
```

После отката:

```sql
SELECT
```

- Шаг 2: `column_name` = `id`; проверка пройдена; действие `continue`.

- Шаг 3: `table_name` = `db_info`; проверка не пройдена; действие `backward_table_name`.

До отката:

```sql
SELECT id FROM db_info WHERE
```

После отката:

```sql
SELECT id FROM
```

- Шаг 4: `table_name` = `highschooler`; проверка пройдена; действие `continue`.

- Шаг 5: `column_name` = `name`; проверка пройдена; действие `continue`.

**Разбор.** Здесь зафиксировано совпадение результата после реальных откатов.

## 5. ID 1029, singer, extra (вне метрик)

Вопрос: What are the citizenships that are shared by singers with a birth year before 1945 and after 1955?

**Эталон:**

```sql
select citizenship from singer where birth_year < 1945 intersect select citizenship from singer where birth_year > 1955
```

**IterGen:**

```sql
SELECT DISTINCT
```

Результат:<br>
SQL не исполняется: incomplete input. Статус: `backtrack_limit`; причина: `backtrack_limit`; откатов: 8; сгенерировано токенов: 41.

### Последовательность проверок

- Шаг 1: `column_name` = `s.citizenship`; проверка пройдена; действие `continue`.

- Шаг 2: `table_name` = `db_singer_songs`; проверка не пройдена; действие `backward_table_name`.

До отката:

```sql
SELECT DISTINCT s.citizenship
FROM db_singer_songs AS
```

После отката:

```sql
SELECT DISTINCT s.citizenship
FROM
```

- Шаг 3: `table_name` = `singer_songs`; проверка не пройдена; действие `backward_table_name`.

До отката:

```sql
SELECT DISTINCT s.citizenship
FROM singer_songs as
```

После отката:

```sql
SELECT DISTINCT s.citizenship
FROM
```

- Шаг 4: `table_name` = `song_songs`; проверка не пройдена; действие `backward_table_name_then_select_expr`.

До отката:

```sql
SELECT DISTINCT s.citizenship
FROM song_songs as
```

После отката:

```sql
SELECT DISTINCT
```

- Шаг 5: `column_name` = `c.citizenship`; проверка пройдена; действие `continue`.

- Шаг 6: `table_name` = `db_info`; проверка не пройдена; действие `backward_table_name`.

До отката:

```sql
SELECT DISTINCT c.citizenship
FROM db_info i
```

После отката:

```sql
SELECT DISTINCT c.citizenship
FROM
```

- Шаг 7: `table_name` = `song_songs`; проверка не пройдена; действие `backward_table_name`.

До отката:

```sql
SELECT DISTINCT c.citizenship
FROM song_songs

```

После отката:

```sql
SELECT DISTINCT c.citizenship
FROM
```

- Шаг 8: `table_name` = `singer_songs`; проверка не пройдена; действие `backward_table_name_then_select_expr`.

До отката:

```sql
SELECT DISTINCT c.citizenship
FROM singer_songs as
```

После отката:

```sql
SELECT DISTINCT
```

**Разбор.**<br> 
Откаты работали, но исчерпали бюджет. Финальный SQL остался незавершённым => больше попыток не гарантирует нахождения правильного продолжения.
