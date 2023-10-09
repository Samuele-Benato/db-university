# DB University2

## Query con GROUP BY.

### 1. Contare quanti iscritti ci sono stati ogni anno

- SELECT YEAR(enrolment_date) AS anno_iscrizione, COUNT(\*) AS numero_iscritti
  FROM `students`
  GROUP BY YEAR(enrolment_date)

### 2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio

- SELECT office_address, COUNT(_) AS insegnanti_nello_stesso_edificio
  FROM `teachers`
  GROUP BY office_address
  HAVING COUNT(_) > 1;
