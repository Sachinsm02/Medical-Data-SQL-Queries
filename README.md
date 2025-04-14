# Medical-Data-SQL-Queries
use project_medical_data_history;
select * from admissions;

-- Query 1
SELECT first_name, last_name, gender FROM patients WHERE gender = 'M';

-- Query 2
SELECT first_name, last_name FROM patients WHERE allergies IS NULL;

-- Query 3
SELECT first_name FROM patients WHERE first_name LIKE 'C%';

-- Query 4
SELECT first_name, last_name FROM patients WHERE weight BETWEEN 100 AND 120;

-- Query 5
UPDATE patients SET allergies = 'NKA' WHERE allergies IS NULL;

-- Query 6
SELECT CONCAT(first_name, ' ', last_name) AS full_name FROM patients; 

-- Query 7
SELECT p.first_name, p.last_name, prov.province_name FROM patients p JOIN province prov ON p.province_id = prov.province_id;

-- Query 8
SELECT count(*) FROM patients WHERE YEAR (birth_date) = 2010;

-- Query 9
SELECT first_name, last_name height FROM patients ORDER BY height DESC LIMIT 1;

-- Query 10
SELECT * FROM patients WHERE patient_id IN (1, 45, 534, 879, 1000);

-- Query 11
SELECT count(*) FROM admissions;

-- Query 12
SELECT * FROM admissions WHERE admission_date = discharge_date ;

-- Query 13
SELECT COUNT(*) FROM admissions WHERE patient_id = 579;

-- Query 14
SELECT DISTINCT city FROM patients WHERE province_id = 'NS';

-- Query 15
SELECT first_name, last_name, birth_date FROM patients WHERE height > 160 AND weight > 70 ;

-- Query 16
SELECT DISTINCT YEAR(birth_date) AS birth_year FROM patients ORDER BY birth_year ASC;

-- Query 17
SELECT first_name FROM patients GROUP BY first_name HAVING count(*) = 1 ;

-- Query 18
SELECT patient_id, first_name FROM patients WHERE first_name LIKE 's%s' AND LENGTH(first_name) >= 6;

-- Query 19
SELECT p.patient_id, p.first_name, p.last_name FROM patients p JOIN admissions a ON p.patient_id = a.patient_id WHERE a.diagnosis = 'Dementia';

-- Query 20
SELECT first_name FROM patients ORDER BY LENGTH(first_name), first_name ;

-- Query 21
SELECT COUNT(CASE WHEN gender = 'M' THEN 1 END) AS male_count, COUNT(CASE WHEN gender = 'F' THEN 1 END) AS female_count FROM patients;

-- Query 22
SELECT COUNT(CASE WHEN gender = 'M' THEN 1 END) AS male_count, COUNT(CASE WHEN gender = 'F' THEN 1 END) AS female_count FROM patients;

-- Query 23
SELECT patient_id, diagnosis FROM admissions GROUP BY patient_id, diagnosis HAVING COUNT(*) > 1;

-- Query 24
SELECT city, COUNT(*) AS total_patients FROM patients GROUP BY city ORDER BY total_patients DESC, city ASC;

-- Query 25
SELECT first_name, last_name, 'Patient' AS role FROM patients UNION SELECT first_name, last_name, 'Doctor' AS role FROM doctors;

-- Query 26
SELECT allergies, COUNT(*) AS frequency FROM patients WHERE allergies IS NOT NULL GROUP BY allergies ORDER BY frequency DESC;

-- Query 27
SELECT first_name, last_name, birth_date FROM patients WHERE YEAR(birth_date) BETWEEN 1970 AND 1979 ORDER BY birth_date ASC;

-- Query 28
SELECT CONCAT(UPPER(last_name), ',', LOWER(first_name)) AS full_name FROM patients ORDER BY LOWER(first_name) DESC;

-- Query 29
SELECT province_id, SUM(height) AS total_height FROM patients GROUP BY province_id HAVING SUM(height) >= 7000;

-- Query 30
SELECT MAX(weight) - MIN(weight) AS weight_difference FROM patients WHERE last_name = 'Maroni';

-- Query 31
SELECT DAY(admission_date) AS day, COUNT(*) AS admissions_count FROM admissions GROUP BY DAY(admission_date) ORDER BY admissions_count DESC;

-- Query 32
SELECT FLOOR(weight / 10) * 10 AS weight_group, COUNT(*) AS total FROM patients GROUP BY weight_group ORDER BY weight_group DESC;

-- Query 33
SELECT patient_id, weight, height, CASE WHEN (weight / POWER(height / 100.0, 2)) >= 30 THEN 1 ELSE 0 END AS isObese FROM patients;

-- Query 34
SELECT p.patient_id, p.first_name, p.last_name, d.specialty FROM patients p JOIN admissions a ON p.patient_id = a.patient_id JOIN doctors d ON a.doctor_id = d.doctor_id WHERE a.diagnosis = 'Epilepsy' AND d.first_name = 'Lisa';

-- Query 35
SELECT p.patient_id, CONCAT(p.patient_id, LENGTH(p.last_name), YEAR(p.birth_date)) AS temp_password FROM patients p JOIN admissions a ON p.patient_id = a.patient_id GROUP BY p.patient_id, p.last_name, p.birth_date;
