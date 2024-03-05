SELECT

1. Selezionare tutti gli studenti nati nel 1990 (160)

```
SELECT *
FROM `students`
WHERE YEAR(`date_of_birth`) = 1990;
```

2. Selezionare tutti i corsi che valgono più di 10 crediti (479)

```
SELECT *
FROM `courses`
WHERE `cfu` > 10;
```

3. Selezionare tutti gli studenti che hanno più di 30 anni

```
SELECT *
FROM `students`
WHERE YEAR(`date_of_birth`) <= 1994 && MONTH(`date_of_birth`) <= 3 && DAY(`date_of_birth`) <= 4;
```

4. Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di laurea (286)

```
SELECT * 
FROM `courses`
WHERE `year`= 1 && `period` = "I semestre";
```

5. Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del 20/06/2020 (21)

```
SELECT * 
FROM `exams`
WHERE `date` = "2020-06-20" && HOUR(`hour`) > 14;
```

6. Selezionare tutti i corsi di laurea magistrale (38)

```
SELECT * 
FROM `degrees`
WHERE `level` = "magistrale";
```

7. Da quanti dipartimenti è composta l'università? (12)

```
SELECT COUNT(id) 
FROM `departments`;
```

8. Quanti sono gli insegnanti che non hanno un numero di telefono? (50)

```
SELECT COUNT(id) 
FROM `teachers`
WHERE `phone` IS NULL;
```

GROUP BY

1. Contare quanti iscritti ci sono stati ogni anno

```
SELECT COUNT(id) AS "Numero_iscritti", YEAR(`enrolment_date`) AS "Anno"
FROM `students`
GROUP BY YEAR(`enrolment_date`);
```

2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio

```
SELECT COUNT(id) AS "Numero insegnanti", `office_address` AS "indirizzo"
FROM `teachers`
GROUP BY `office_address`;
```

3. Calcolare la media dei voti di ogni appello d'esame

```
SELECT AVG(`vote`) AS "Media", `exam_id` AS "Appello"
FROM `exam_student`
GROUP BY `exam_id`;
```

4. Contare quanti corsi di laurea ci sono per ogni dipartimento

```
SELECT COUNT(id) AS "Numero corsi", `department_id` AS "Dipartimento"
FROM `degrees`
GROUP BY `department_id`;
```

JOIN

1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

```
SELECT `degrees`.`name` AS "Corso di Laurea", `students`.*
FROM `students`
JOIN `degrees`
ON `degrees`.`id` = `students`. `degree_id`
WHERE `degrees`.`name`= "Corso di Laurea in Economia";
```

2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze

```
SELECT `degrees`.`name`
FROM `degrees`
JOIN `departments`
ON `departments`.`id` = `degrees`. `department_id`
WHERE `degrees`.`level`= "magistrale"
AND `departments`.`name` = "Dipartimento di Neuroscienze";
```

3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

```
SELECT `courses`.`name` AS "Corsi di Fulvio Amato"
FROM `courses`
JOIN `course_teacher`
ON `course_teacher`.`course_id` = `courses`.`id`
JOIN `teachers`
ON `course_teacher`.`teacher_id` = `teachers`.`id`
WHERE `teachers`.`id`= 44;
```

4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome

```

```

5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)
7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18.