1. Contare quanti iscritti ci sono stati ogni anno

 SELECT YEAR(`enrolment_date`) AS `enrolment_date`, COUNT(`id`) AS `number`  
FROM `students`  
GROUP BY YEAR(`enrolment_date`)  
ORDER BY YEAR(`enrolment_date`);  

2. Contare gli insegnanti che hanno l'uffico nello stesso edificio

  SELECT `office_number`, COUNT(`id`)  
FROM `teachers`  
GROUP BY `office_number`  
ORDER BY `office_number`;  

3. Calcolare la media dei voti di ogni appello d'esame

 SELECT AVG(`vote`), `exam_id`  
FROM `exam_student`  
GROUP BY `exam_id`;  

4. Contare quanti corsi di laurea ci sono per ogni dipartimento

 SELECT `department_id` AS `department`, COUNT(`id`) AS `degrees_number`  
FROM `degrees`  
GROUP BY `department_id`;  