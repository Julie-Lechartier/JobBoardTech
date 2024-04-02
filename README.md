# JobBoardTech
Conception d'une base de données pour un Job Board IT

Objectif : Concevoir et mettre en place une base de données relationnelle permettant de stocker les profils techniques et leurs informations pertinentes, tout en permettant des recherches avancées basées sur différents critères.

## Etape 1 
On commence par la conception d'un schéma conceptuel de la base de données en utilisant la méthode MERISE

## Etape2
MOCODO

## Etape 3

Entrée du code dans MySQL

CREATE TABLE CANDIDAT (
  PRIMARY KEY (id_candidat),
  id_candidat VARCHAR(42) NOT NULL,
  email       VARCHAR(42),
  Git_Hub     VARCHAR(42),
  departement VARCHAR(42)
);

CREATE TABLE CANDIDAT_CONTRAT (
  PRIMARY KEY (id_candidat, id_contrat),
  id_candidat         VARCHAR(42) NOT NULL,
  id_contrat          VARCHAR(42) NOT NULL,
  id_candidat_contrat VARCHAR(42)
);

CREATE TABLE CANDIDAT_EXPERIENCE (
  PRIMARY KEY (id_candidat, id_experience),
  id_candidat            VARCHAR(42) NOT NULL,
  id_experience          VARCHAR(42) NOT NULL,
  id_candidat_experience VARCHAR(42)
);

CREATE TABLE CANDIDAT_FORMATION (
  PRIMARY KEY (id_candidat, id_formation),
  id_candidat           VARCHAR(42) NOT NULL,
  id_formation          VARCHAR(42) NOT NULL,
  id_candidat_formation VARCHAR(42)
);

CREATE TABLE CANDIDAT_TECH (
  PRIMARY KEY (id_candidat, id_tech),
  id_candidat      VARCHAR(42) NOT NULL,
  id_tech          VARCHAR(42) NOT NULL,
  id_candidat_tech VARCHAR(42)
);

CREATE TABLE CANDIDAT_TYPE_REMOTE (
  PRIMARY KEY (id_candidat, id_remote),
  id_candidat        VARCHAR(42) NOT NULL,
  id_remote          VARCHAR(42) NOT NULL,
  id_candidat_remote VARCHAR(42)
);

CREATE TABLE EXPERIENCE_DETAIL (
  PRIMARY KEY (id_candidat),
  id_candidat          VARCHAR(42) NOT NULL,
  id_experience_detail VARCHAR(42),
  titre_poste          VARCHAR(42),
  description          VARCHAR(42)
);

CREATE TABLE FORMATION (
  PRIMARY KEY (id_formation),
  id_formation VARCHAR(42) NOT NULL,
  type         VARCHAR(42)
);

CREATE TABLE NIVEAU_EXPERIENCE (
  PRIMARY KEY (id_experience),
  id_experience VARCHAR(42) NOT NULL,
  name          VARCHAR(42)
);

CREATE TABLE TECHNOLOGIE (
  PRIMARY KEY (id_tech),
  id_tech VARCHAR(42) NOT NULL,
  name    VARCHAR(42)
);

CREATE TABLE TYPE_CONTRAT (
  PRIMARY KEY (id_contrat),
  id_contrat VARCHAR(42) NOT NULL,
  name       VARCHAR(42)
);

CREATE TABLE TYPE_REMOTE (
  PRIMARY KEY (id_remote),
  id_remote VARCHAR(42) NOT NULL,
  type      VARCHAR(42)
);

ALTER TABLE CANDIDAT_CONTRAT ADD FOREIGN KEY (id_contrat) REFERENCES TYPE_CONTRAT (id_contrat);
ALTER TABLE CANDIDAT_CONTRAT ADD FOREIGN KEY (id_candidat) REFERENCES CANDIDAT (id_candidat);

ALTER TABLE CANDIDAT_EXPERIENCE ADD FOREIGN KEY (id_experience) REFERENCES NIVEAU_EXPERIENCE (id_experience);
ALTER TABLE CANDIDAT_EXPERIENCE ADD FOREIGN KEY (id_candidat) REFERENCES CANDIDAT (id_candidat);

ALTER TABLE CANDIDAT_FORMATION ADD FOREIGN KEY (id_formation) REFERENCES FORMATION (id_formation);
ALTER TABLE CANDIDAT_FORMATION ADD FOREIGN KEY (id_candidat) REFERENCES CANDIDAT (id_candidat);

ALTER TABLE CANDIDAT_TECH ADD FOREIGN KEY (id_tech) REFERENCES TECHNOLOGIE (id_tech);
ALTER TABLE CANDIDAT_TECH ADD FOREIGN KEY (id_candidat) REFERENCES CANDIDAT (id_candidat);

ALTER TABLE CANDIDAT_TYPE_REMOTE ADD FOREIGN KEY (id_remote) REFERENCES TYPE_REMOTE (id_remote);
ALTER TABLE CANDIDAT_TYPE_REMOTE ADD FOREIGN KEY (id_candidat) REFERENCES CANDIDAT (id_candidat);

ALTER TABLE EXPERIENCE_DETAIL ADD FOREIGN KEY (id_candidat) REFERENCES CANDIDAT (id_candidat);
