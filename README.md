# Sistema-Distribuidos
Elias Soares  2111983
UNIEVANGELICA
/* Create tables */
CREATE TABLE office (
id INT PRIMARY KEY AUTO_INCREMENT,
name VARCHAR(100),
location VARCHAR(150)
);

CREATE TABLE professional (
id INT PRIMARY KEY AUTO_INCREMENT,
specialty_id INT,
office_id INT,
name VARCHAR(100),
crm VARCHAR(13),
FOREIGN KEY (specialty_id) REFERENCES specialty (id),
FOREIGN KEY (office_id) REFERENCES office (id)
);

CREATE TABLE patient (
id INT PRIMARY KEY AUTO_INCREMENT,
name VARCHAR(100),
birth_date DATE,
insurance_number VARCHAR(15)
);

CREATE TABLE appointment (
id INT PRIMARY KEY AUTO_INCREMENT,
professional_id INT,
patient_id INT,
schedule DATETIME,
FOREIGN KEY (professional_id) REFERENCES professional (id),
FOREIGN KEY (patient_id) REFERENCES patient (id)
);

CREATE TABLE specialty (
id INT PRIMARY KEY AUTO_INCREMENT,
name VARCHAR(80),
description VARCHAR(200)
);

/* Select queries */
SELECT * FROM office;
SELECT p.name, p.crm, s.name AS specialty, o.name AS office
FROM professional p
INNER JOIN specialty s ON s.id = p.specialty_id
INNER JOIN office o ON p.office_id = o.id;
SELECT * FROM patient;
SELECT * FROM appointment WHERE schedule = "2023-03-24 01:39:00";
SELECT * FROM appointment WHERE professional_id = 1;
SELECT * FROM appointment WHERE patient_id = 1;
SELECT MAX(schedule) AS MostRecentAppointment FROM appointment;
SELECT MIN(schedule) AS OldestAppointment FROM appointment;

/* Insert queries */
INSERT INTO specialty (name, description) VALUES ("Cardiology", "Lorem Ipsum");
INSERT INTO office (name, location) VALUES ("Office 1", "Room 1");
INSERT INTO professional (specialty_id, office_id, name, crm) VALUES (1, 1, "Doctor 1", "CRM/GO123456");
INSERT INTO patient (name, birth_date, insurance_number) VALUES ("Patient 1", "2001-06-25", "1234567890");
INSERT INTO appointment (professional_id, patient_id, schedule) VALUES (1, 1, "2023-03-24 01:39:00");

/* Update query */
UPDATE appointment SET schedule = "2023-03-30 01:39:00" WHERE id = 2;

/* Delete query */
DELETE FROM appointment WHERE id = 2;
