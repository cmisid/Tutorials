<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table des matières**  

- [[Draw.io](https://www.draw.io/)](#drawiohttpswwwdrawio)
- [[Pony](https://ponyorm.com/)](#ponyhttpsponyormcom)
  - [Schéma entité/association](#sch%C3%A9ma-entit%C3%A9association)
  - [Code généré par *Pony*](#code-g%C3%A9n%C3%A9r%C3%A9-par-pony)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

Vous trouverez ici plusieurs outils productifs qui pourront vous faire gagner du temps.

## [Draw.io](https://www.draw.io/)
``draw.io`` est un logiciel de diagrammes en ligne permettant notamment de réaliser des organigrammes, des schémas UML ou E/A, et il propose même des maquettes graphiques pour le développement d'applications mobiles.

## [Pony](https://ponyorm.com/)
``pony``est un logiciel en ligne qui permet d'établir des schémas entités/associations, puis de générer automatiquement du code pour instancier une BD.

### Schéma entité/association
![Exemple](http://i.imgur.com/Gjs3Bwh.png)

### Code généré par *Pony* 
```sql
CREATE TABLE "ville" (
  "idville" SERIAL PRIMARY KEY,
  "nom" TEXT NOT NULL
);

CREATE TABLE "entreprise" (
  "ident" SERIAL PRIMARY KEY,
  "nom" TEXT NOT NULL,
  "ville" INTEGER NOT NULL
);

CREATE INDEX "idx_entreprise__ville" ON "entreprise" ("ville");

ALTER TABLE "entreprise" ADD CONSTRAINT "fk_entreprise__ville" FOREIGN KEY ("ville") REFERENCES "ville" ("idville");

CREATE TABLE "employe" (
  "idemp" SERIAL PRIMARY KEY,
  "prenom" TEXT NOT NULL,
  "nom" TEXT NOT NULL,
  "adresse" TEXT NOT NULL,
  "salaire" DOUBLE PRECISION NOT NULL,
  "entreprise" INTEGER NOT NULL,
  "ville" INTEGER NOT NULL
);

CREATE INDEX "idx_employe__entreprise" ON "employe" ("entreprise");

CREATE INDEX "idx_employe__ville" ON "employe" ("ville");

ALTER TABLE "employe" ADD CONSTRAINT "fk_employe__entreprise" FOREIGN KEY ("entreprise") REFERENCES "entreprise" ("ident");

ALTER TABLE "employe" ADD CONSTRAINT "fk_employe__ville" FOREIGN KEY ("ville") REFERENCES "ville" ("idville")
```