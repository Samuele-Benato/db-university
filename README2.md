# DB University2

## Query con GROUP BY.

### 1. Contare quanti iscritti ci sono stati ogni anno

- SELECT YEAR(enrolment_date) AS anno_iscrizione, COUNT(\*) AS numero_iscritti
  FROM `students`
  GROUP BY YEAR(enrolment_date)
