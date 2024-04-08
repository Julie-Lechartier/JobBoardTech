# JobBoardTech
Conception d'une base de données pour un Job Board IT

Objectif : Concevoir et mettre en place une base de données relationnelle permettant de stocker les profils techniques et leurs informations pertinentes, tout en permettant des recherches avancées basées sur différents critères.

## Etape 1 
On commence par la conception d'un schéma conceptuel de la base de données en utilisant la méthode MERISE

## Etape2
MOCODO

## Etape 3

Entrée du code dans MySQL. On force la conversion du type de serveur en InnoDB

CREATE TABLE CANDIDAT(
    id_candidat int NOT NULL AUTO_INCREMENT,
    email VARCHAR(42),
    Git_Hub VARCHAR(42),
    departement VARCHAR(42),
    PRIMARY KEY (id_candidat)
); 
CREATE TABLE CANDIDAT_CONTRAT(
    id_candidat_contrat int not null AUTO_INCREMENT,
    id_candidat int NOT NULL,
    id_contrat int NOT NULL,
    PRIMARY KEY (id_candidat_contrat),
    FOREIGN KEY (id_candidat) REFERENCES CANDIDAT(id_candidat),
    FOREIGN KEY (id_contrat) REFERENCES  TYPE_CONTRAT(id_contrat)
); 

CREATE TABLE CANDIDAT_EXPERIENCE(
    id_candidat_experience int NOT null AUTO_INCREMENT,
    id_candidat int NOT NULL,
    id_experience int NOT NULL,
    PRIMARY KEY (id_candidat_experience),
    FOREIGN KEY (id_candidat) REFERENCES CANDIDAT(id_candidat),
    FOREIGN KEY (id_experience) REFERENCES NIVEAU_EXPERIENCE(id_experience)
); 

CREATE TABLE CANDIDAT_FORMATION(
    id_candidat_formation int NOT NULL AUTO_INCREMENT,
    id_candidat int NOT NULL,
    id_formation int NOT NULL,
    PRIMARY KEY(id_candidat_formation),
    FOREIGN KEY (id_candidat) REFERENCES CANDIDAT(id_candidat),
    FOREIGN KEY (id_formation) REFERENCES FORMATION(id_formation)
); 

CREATE TABLE CANDIDAT_TECH(
    id_candidat_tech int not null AUTO_INCREMENT,
    id_candidat int NOT NULL,
    id_tech int NOT NULL,
    PRIMARY KEY (id_candidat_tech),
    FOREIGN KEY (id_candidat) REFERENCES candidat(id_candidat),
    FOREIGN KEY (id_tech) REFERENCES TECHNOLOGIE(id_tech)
); 

CREATE TABLE CANDIDAT_TYPE_REMOTE(
    id_candidat_remote int AUTO_INCREMENT,
    id_candidat int NOT NULL,
    id_remote int NOT NULL,
    PRIMARY KEY(id_candidat_remote),
    FOREIGN KEY(id_candidat) REFERENCES candidat(id_candidat),
    FOREIGN KEY(id_remote) REFERENCES TYPE_REMOTE(id_remote)
); 

CREATE TABLE EXPERIENCE_DETAIL(
    id_experience_detail int not null AUTO_INCREMENT,
    id_candidat int NOT NULL,
    titre_poste VARCHAR(42),
    description VARCHAR(150),
    PRIMARY KEY (id_experience_detail),
    FOREIGN KEY (id_candidat) REFERENCES candidat(id_candidat)
); 

CREATE TABLE FORMATION(
    id_formation int NOT NULL AUTO_INCREMENT,
    TYPE VARCHAR(42),
    PRIMARY KEY (id_formation)
); 

CREATE TABLE NIVEAU_EXPERIENCE(
    id_experience int NOT NULL AUTO_INCREMENT,
    NAME VARCHAR(42),
    PRIMARY KEY(id_experience)
); 

CREATE TABLE TECHNOLOGIE(
    id_tech int NOT NULL AUTO_INCREMENT,
    NAME VARCHAR(42),
    PRIMARY KEY(id_tech)
); 

CREATE TABLE TYPE_CONTRAT(
    id_contrat int NOT NULL AUTO_INCREMENT,
    NAME VARCHAR(42),
    PRIMARY KEY (id_contrat)
); 

CREATE TABLE TYPE_REMOTE(
    id_remote int NOT NULL AUTO_INCREMENT,
    TYPE VARCHAR(42),
    PRIMARY KEY(id_remote)
); 

CREATE TABLE POSTE( 
	id_poste int not null AUTO_INCREMENT,
    name varchar(50),
    PRIMARY KEY (id_poste)
);
CREATE TABLE CANDIDAT_POSTE(
    id_candidat_poste int not null AUTO_INCREMENT,
    id_candidat int,
    id_poste int,
    PRIMARY KEY (id_candidat_poste),
    FOREIGN key (id_candidat) REFERENCES candidat(id_candidat),
    FOREIGN KEY (id_poste) REFERENCES poste(id_poste)
);

ALTER TABLE
    CANDIDAT ENGINE = INNODB;
ALTER TABLE
    CANDIDAT_CONTRAT ENGINE = INNODB;
ALTER TABLE
    CANDIDAT_EXPERIENCE ENGINE = INNODB;
ALTER TABLE
    CANDIDAT_FORMATION ENGINE = INNODB;
ALTER TABLE
    CANDIDAT_TECH ENGINE = INNODB;
ALTER TABLE
    CANDIDAT_TYPE_REMOTE ENGINE = INNODB;
ALTER TABLE
    EXPERIENCE_DETAIL ENGINE = INNODB;
ALTER TABLE
    FORMATION ENGINE = INNODB;
ALTER TABLE
    NIVEAU_EXPERIENCE ENGINE = INNODB;
ALTER TABLE
    TECHNOLOGIE ENGINE = INNODB;
ALTER TABLE
    TYPE_REMOTE ENGINE = INNODB;
ALTER TABLE
    TYPE_CONTRAT ENGINE = INNODB;
ALTER TABLE
	POSTE ENGINE = INNODB;
ALTER TABLE
	CANDIDAT_POSTE ENGINE = INNODB;

ALTER TABLE
    CANDIDAT_CONTRAT ADD FOREIGN KEY(id_contrat) REFERENCES TYPE_CONTRAT(id_contrat);
ALTER TABLE
    CANDIDAT_CONTRAT ADD FOREIGN KEY(id_candidat) REFERENCES CANDIDAT(id_candidat);
ALTER TABLE
    CANDIDAT_EXPERIENCE ADD FOREIGN KEY(id_experience) REFERENCES NIVEAU_EXPERIENCE(id_experience);
ALTER TABLE
    CANDIDAT_EXPERIENCE ADD FOREIGN KEY(id_candidat) REFERENCES CANDIDAT(id_candidat);
ALTER TABLE
    CANDIDAT_FORMATION ADD FOREIGN KEY(id_formation) REFERENCES FORMATION(id_formation);
ALTER TABLE
    CANDIDAT_FORMATION ADD FOREIGN KEY(id_candidat) REFERENCES CANDIDAT(id_candidat);
ALTER TABLE
    CANDIDAT_TECH ADD FOREIGN KEY(id_tech) REFERENCES TECHNOLOGIE(id_tech);
ALTER TABLE
    CANDIDAT_TECH ADD FOREIGN KEY(id_candidat) REFERENCES CANDIDAT(id_candidat);
ALTER TABLE
    CANDIDAT_TYPE_REMOTE ADD FOREIGN KEY(id_remote) REFERENCES TYPE_REMOTE(id_remote);
ALTER TABLE
    CANDIDAT_TYPE_REMOTE ADD FOREIGN KEY(id_candidat) REFERENCES CANDIDAT(id_candidat);
ALTER TABLE
    EXPERIENCE_DETAIL ADD FOREIGN KEY(id_candidat) REFERENCES CANDIDAT(id_candidat);
ALTER TABLE
	CANDIDAT_POSTE ADD FOREIGN KEY(id_candidat) REFERENCES candidat(id_candidat);
ALTER TABLE
	CANDIDAT_POSTE ADD FOREIGN KEY(id_poste) REFERENCES poste(id_poste);


Les dernières lignes permettent d'afficher les liens entre les tables dans le concepteur de MySQL.

## Ajout des valeurs dans les tables 

INSERT INTO `candidat` (`email`, `Git_Hub`, `departement`) VALUES ( 'lorem@sfr.fr', 'loremipsum', '69');
	Ici on créé un nouveau candidat dans la table candidat 

## Ajout des requêtes

On rempli ensuite les tables de valeur pour pouvoir tester différentes requêtes :

SELECT * FROM candidat_poste JOIN candidat ON candidat_poste.id_candidat = candidat.id_candidat WHERE candidat_poste.id_poste = '3' AND candidat.departement = '01';
	on affiche ici tout les candidat qui sont développeur back-end et qui sont dans le département 01

 SELECT * FROM candidat_experience JOIN niveau_experience ON candidat_experience.id_experience = niveau_experience.id_experience WHERE candidat_experience.id_experience = '3';
 	on affiche tout les candidats avec un niveau d'expérience Senior

SELECT *
FROM candidat_type_remote
JOIN candidat_tech ON candidat_type_remote.id_candidat = candidat_tech.id_candidat
WHERE candidat_type_remote.id_remote = '2' AND candidat_tech.id_tech = '8';
	on afficher les candidats avec une utilisation de PHP et qui sont en full remote

 
