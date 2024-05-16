1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

SELECT *
FROM `students`
INNER JOIN `degrees`
ON `degrees`.`id` = `students`.`degree_id`
WHERE `degrees`.`name` = "Corso di Laurea in Economia";

2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze

SELECT *
FROM `degrees`
INNER JOIN `departments`
ON `departments`.`id` = `degrees`.`department_id`
WHERE `departments`.`name` = "Dipartimento di Neuroscienze";

3. Selezionare tutti i Corsi in cui insegna Fulvio Amato (id=44)

SELECT `courses`.*, `teachers`.`name` AS `teacher_name`
FROM `teachers`
INNER JOIN `course_teacher`
ON `teachers`.`id` = `course_teacher`.`teacher_id`
INNER JOIN `courses`
ON `course_teacher`.`course_id` = `courses`.`id`
WHERE `teachers`.`id` = 44

4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome

SELECT *
FROM `students`
INNER JOIN `degrees`
ON `degrees`.`id` = `students`.`degree_id`
INNER JOIN `departments`
ON `departments`.`id` = `degrees`.`department_id`
ORDER BY `students`.`name` ASC , `students`.`surname` ASC

5. Selezionare tutti i corsi di laurea con i relativi corsi ed insegnanti

SELECT `degrees`.* , `teachers`.`name` AS `teacher`, `courses`.`name` AS `course_name`
FROM `degrees`
INNER JOIN `courses`
ON `degrees`.`id` = `courses`.`degree_id`
INNER JOIN `course_teacher`
ON `courses`.`id` = `course_teacher`.`course_id`
INNER JOIN `teachers`
ON `course_teacher`.`teacher_id` = `teachers`.`id`

6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)

SELECT DISTINCT `teachers`.*
FROM `teachers`
INNER JOIN `course_teacher`
ON `teachers`.`id` = `course_teacher`.`teacher_id`
INNER JOIN `courses`
ON `course_teacher`.`course_id` = `courses`.`id`
INNER JOIN `degrees`
ON `degrees`.`id` = `courses`.`degree_id`
INNER JOIN `departments`
ON `departments`.`id` = `degrees`.`department_id`
WHERE `departments`.`name` = "Dipartimento di Matematica"  
ORDER BY `teachers`.`name` ASC;

7. BONUS: Selezionare per ogni studente quanti tentativi d’esame ha sostenuto per superare ciascuno dei suoi esami  
SELECT `students`.`name`, `students`.`surname`, `courses`.`name`, COUNT(`exam_student`.`vote`) AS `tentatives`, MAX(`vote`) AS `max_voto`  
FROM `exam_student`  
JOIN `students`  
ON `students`.`id` = `exam_student`.`student_id`  
JOIN `exams`  
ON `exam_student`.`exam_id` = `exams`.`id`  
JOIN `courses`  
ON `exams`.`course_id` = `courses`.`id`  
GROUP BY `students`.`id`, `courses`.`name`  
HAVING `max_voto` > 18  
ORDER BY `students`.`surname`, `students`.`name`, `courses`.`name`;  



