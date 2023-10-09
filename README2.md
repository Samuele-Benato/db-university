# DB University2

## Query con GROUP BY.

### 1. Contare quanti iscritti ci sono stati ogni anno

- SELECT YEAR(enrolment_date) AS anno_iscrizione, COUNT(\*) AS numero_iscritti
  FROM `students`
  GROUP BY YEAR(enrolment_date)

### 2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio

- SELECT office_address, COUNT(\*) AS insegnanti_nello_stesso_edificio
  FROM `teachers`
  GROUP BY office_address
  HAVING COUNT(\*) > 1;

  ### 3. Calcolare la media dei voti di ogni appello d'esame

  - SELECT exam_id, ROUND(AVG(vote)) AS media_voti
    FROM `exam_student`
    GROUP BY exam_id;

### 4. Contare quanti corsi di laurea ci sono per ogni dipartimento

- SELECT degree_id, COUNT(\*) AS numero_corsi_di_laurea
  FROM `courses`
  GROUP BY degree_id;

## Query con GROUP JOIN.

### 1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

- SELECT `students`.\*
  FROM `students`
  INNER JOIN `degrees`
  ON `students`.degree_id = `degrees`.id
  INNER JOIN `courses`
  ON `degrees`.id = `courses`.degree_id
  WHERE `degrees`.name = 'Corso di Laurea in Economia';

### 2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze

- SELECT `courses`.\*
  FROM `courses`
  INNER JOIN `degrees`
  ON `courses`.degree_id = `degrees`.id
  INNER JOIN `departments`
  ON `departments`.id = `degrees`.department_id
  WHERE `degrees`.level = 'magistrale' AND `departments`.name = 'Dipartimento di Neuroscienze';

### 3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

- SELECT courses.\*
  FROM courses
  INNER JOIN course_teacher
  ON courses.id = course_teacher.course_id
  INNER JOIN teachers
  ON course_teacher.teacher_id = teachers.id
  WHERE teachers.id = 44;

  ### 4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome

- SELECT students.name AS student_name, students.surname AS student_surname, degrees. name AS degree_name, departments.name AS department_name
  FROM students
  INNER JOIN degrees
  ON students.degree_id = degrees.id
  INNER JOIN departments
  ON degrees.department_id = departments.id
  ORDER BY students.surname, students.name;

### 5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti

- SELECT degrees.name AS corso_di_laurea,courses.name AS corso,
  GROUP_CONCAT(teachers.name, ' ', teachers.surname) AS insegnanti
  FROM degrees
  INNER JOIN courses
  ON degrees.id = courses.degree_id
  INNER JOIN course_teacher
  ON courses.id = course_teacher.course_id
  INNER JOIN teachers
  ON course_teacher.teacher_id = teachers.id
  GROUP BY degrees.name, courses.name;
