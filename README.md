# SQL

MODULE 2 :

DRL (Data Retrieval Language - Langage d’extraction de données)
 Partie I : SELECT … FROM …
Exercice 2.1.1 – Les requêtes suivantes fonctionnent-elles sous SQL-Server ? Si non, comment 
les corriger ?
N’hésitez pas à tester vos requêtes directement sous Management Studio 

1: SELECT last_name , first_name AS F name FROM student; // Il y'avait un espace entre F et name

2: SELECT last_name lname , first_name AS Fname FROM student; correct

3: SELECT last_name || _ || first_name AS name FROM student ; 
les 4 barres ne doivent pas se retrouver là ===> 
SELECT last_name , first_name AS name FROM student; 

4: SELECT last_name + first_name AS name , Year_result * 10 result , FROM student ; Il y'a une virgule en trop 

Exercice 2.1.2 – Ecrire une requête pour présenter, pour chaque étudiant, le nom de l’étudiant, 
la date de naissance, le login et le résultat pour l’année de l’ensemble des étudiants.




Exercice 2.1.3 – Ecrire une requête pour présenter, pour chaque étudiant, son nom complet 
(nom et prénom séparés par un espace), son id et sa date de naissance.

SELECT CONCAT(last_name , " " , first_name )AS "nom complet" , student_id , birth_date FROM student;





Exercice 2.1.4 – Ecrire une requête pour présenter, pour chaque étudiant, dans une seule 
colonne (nommée « Info Étudiant ») l’ensemble des données relatives à un étudiant séparées par 
le symbole « | ». Sous SQL Server, il est nécessaire d’avoir recours à la fonction de conversion 
CONVERT(type, champs)

SELECT CONCAT(student_id , "|" , birth_date , "|" , course_id , 
"|" , last_name , "|" , first_name )
 AS "info étudient" 
FROM student;

REQUETE LAMBA :

SELECT * FROM student 
WHERE year_result >= 10 


Partie II : SELECT … FROM … WHERE … ORDER BY

Exercice 2.2.1 – Ecrire une requête pour présenter le login et le résultat de tous les étudiants 
ayant obtenu un résultat annuel supérieur à 16

SELECT login , year_result FROM student WHERE year_result > 16;

Exercice 2.2.2 – Ecrire une requête pour présenter le nom et l’id de section des étudiants dont 
le prénom est Georges

SELECT last_name , section_id FROM student WHERE first_name = 'Georges';

Exercice 2.2.3 – Ecrire une requête pour présenter le nom et le résultat annuel de tous les 
étudiants ayant obtenu un résultat annuel compris entre 12 et 16

SELECT last_name , year_result FROM student WHERE year_result BETWEEN 12 AND 16;

Exercice 2.2.4 – Ecrire une requête pour présenter le nom, l’id de section et le résultat annuel 
de tous les étudiants qui ne font pas partie des sections 1010, 1020 et 1110

SELECT last_name , section_id , year_result FROM student WHERE section_id NOT IN(1010,1020,1110);


Exercice 2.2.5 – Ecrire une requête pour présenter le nom et l’id de section de tous les 
étudiants qui ont un nom de famille qui termine par « r »

SELECT last_name , section_id FROM student WHERE last_name LIKE '%r';

Exercice 2.2.6 – Ecrire une requête pour présenter le nom et le résultat annuel de tous les 
étudiants qui ont un nom de famille pour lequel la troisième lettre est un « n » et qui ont obtenu 
un résultat annuel supérieur à 10

SELECT last_name , year_result FROM student WHERE last_name LIKE '__n%' AND year_result > 10;


Exercice 2.2.7 – Ecrire une requête pour présenter le nom et le résultat annuel classé par 
résultats annuels décroissants de tous les étudiants qui ont obtenu un résultat annuel inférieur ou 
égal à 3

SELECT last_name , year_result FROM student WHERE year_result <= 3;

Exercice 2.2.8 – Ecrire une requête pour présenter le nom complet (nom et prénom séparés par
un espace) et le résultat annuel classé par nom croissant sur le nom de tous les étudiants 
appartenant à la section 1010

SELECT CONCAT (last_name , " " , first_name) AS 'Nom complet ' , year_result
FROM student
WHERE section_id = 1010
ORDER BY  year_result  ;

Exercice 2.2.9 – Ecrire une requête pour présenter le nom, l’id de section et le résultat annuel 
classé par ordre croissant sur la section de tous les étudiants appartenant aux sections 1010 et 
1020 ayant un résultat annuel qui n’est pas compris entre 12 et 18

SELECT last_name , section_id , year_result
 FROM student
 WHERE section_id IN (1010,1020) AND year_result NOT BETWEEN 12 AND 18
 ORDER BY section_id;

Exercice 2.2.10 – Ecrire une requête pour présenter le nom, l’id de section et le résultat annuel 
sur 100 (nommer la colonne « Résultat sur 100 ») classé par ordre décroissant du résultat de tous 
les étudiants appartenant aux sections commençant par 13 et ayant un résultat annuel sur 100 
inférieur ou égal à 60

SELECT last_name , section_id , year_result * 5 AS 'resulta 100' 
FROM student
WHERE section_id LIKE "13%" AND year_result * 5 <= 60 
ORDER BY year_result DESC;



Exercice 2.2.11 – Ceci clôture la première partie DRL du cours. Avant de passer à la suite 
de la matière, nous vous invitons à prendre un peu de temps afin d’évaluer 
personnellement votre niveau de compréhension de la matière en vous référant aux 
derniers slides du module (slides d’auto-évaluation)




Partie III : Les Fonctions
Exercice 2.3.1 – Pourquoi lorsque l’on utilise la fonction « MAX » ou « MIN » les valeurs 
« NULL » sont-elles ignorées ? 
Car elle n'a aucune valeur

Exercice 2.3.2 – Pourquoi le type des données n’a-t-il pas d’importance lorsque l’on utilise la 
fonction « COUNT » ?
parce que on combre combient de résultat demander il y 'a 

Exercice 2.3.3 – La fonction « AVG » renvoie la moyenne de toutes les lignes résultantes d’une 
requête SELECT sur une colonne incluant toutes les valeurs « NULL ». (Faux )


Exercice 2.3.4 – La fonction « SUM » est utilisée pour ajouter des totaux aux colonnes.
(Vrai)


Exercice 2.3.5 – La fonction « COUNT(*) » compte toutes les lignes d’une table. (Faux)
cologne

Exercice 2.3.6 – Les requêtes suivantes sont-elles valides ?

1: SELECT COUNT *
FROM student ==> non car il manque des infos

2: SELECT COUNT (student_id) , login
FROM student ==> non car il manque des info

3: SELECT MIN (year_result) , MAX(birth_date)
FROM student ==> birth_date n'est pas un entier

Exercice 2.3.7 – Donner le résultat annuel moyen pour l’ensemble des étudiants

SELECT AVG(year_result) AS 'Moyen générale' FROM student;

Exercice 2.3.8 – Donner le plus haut résultat annuel obtenu par un étudiant

SELECT MAX(year_result) AS 'Plus haut resultat' FROM student;

Exercice 2.3.9 – Donner la somme des résultats annuels

SELECT SUM(year_result) AS 'Sommes des resultat' FROM student;

Exercice 2.3.10 – Donner le résultat annuel le plus faible

SELECT MIN(year_result) AS 'Plus haut resultat' FROM student;

Exercice 2.3.11 – Donner le nombre de lignes qui composent la table « STUDENT »

SELECT COUNT(student_id) AS 'Nombre etudient ' FROM student;

Exercice 2.3.12 – Donner la liste des étudiants (login et année de naissance) nés après 1970

SELECT login , birth_date FROM student WHERE year(birth_date) >= 1970;

Exercice 2.3.13 – Donner le login et le nom de tous les étudiants qui ont un nom composé d’au 
moins 8 lettres

SELECT login , last_name FROM student WHERE CHAR_LENGTH (last_name) >= 8;

Exercice 2.3.14 – Donner la liste des étudiants ayant obtenu un résultat annuel supérieur ou 
égal à 16. La liste présente le nom de l’étudiant en majuscules (nommer la colonne « Nom de 
Famille ») et le prénom de l’étudiant dans l’ordre décroissant des résultats annuels obtenus

SELECT UPPER (last_name ) AS 'Nom de famille', first_name , year_result
 FROM student
 WHERE year_result >= 16
 ORDER BY year_result DESC;

Exercice 2.3.15 – Donner un nouveau login à chacun des étudiants ayant obtenu un résultat 
annuel compris entre 6 et 10. Le login se compose des deux premières lettres du prénom de 
l’étudiant suivi par les quatre premières lettres de son nom le tout en minuscule. Le résultat 
reprend pour chaque étudiant, son nom, son prénom l’ancien et le nouveau login (colonne « 
Nouveau login »)


SELECT last_name , first_name , login ,
 LOWER(CONCAT(SUBSTRING(first_name,1,2) ,'' , SUBSTRING(last_name,2,4))) AS "Nouveau login"
 FROM student 
WHERE year_result BETWEEN 6 AND 10;


Exercice 2.3.16 – Donner un nouveau login à chacun des étudiants ayant obtenu un résultat 
annuel égal à 10, 12 ou 14. Le login se compose des trois dernières lettres de son prénom suivi du 
chiffre obtenu en faisant la différence entre l’année en cours et l’année de leur naissance. Le 
résultat reprend pour chaque étudiant, son nom, son prénom l’ancien et le nouveau login (colonne
« Nouveau login »)

SELECT first_name , last_name , login , CONCAT(RIGHT(first_name,3) , (year(CURRENT_DATE())-year(birth_date))) 
AS "Nouveau login"
 FROM student 
WHERE year_result IN (10,12,14);



Exercice 2.3.17 – Donner la liste des étudiants (nom, login, résultat annuel) qui ont un nom 
commençant par « D », « M » ou « S ». La liste doit présenter les données dans l’ordre croissant 
des dates de naissance des étudiants

SELECT first_name , last_name , year_result FROM student WHERE LEFT(last_name , 1 ) IN ('D' , 'S' , 'M');


Exercice 2.3.18 – Donner la liste des étudiants (nom, login, résultat annuel) qui ont obtenu un 
résultat impair supérieur à 10. La liste doit être triée du plus grand résultat au plus petit

SELECT first_name , last_name  , year_result
FROM student
WHERE year_result % 2 != 0 AND year_result > 10 
ORDER BY year_result DESC




Exercice 2.3.19 – Donner le nombre d’étudiants qui ont au moins 7 lettres dans leur nom de 
famille

SELECT COUNT(*) AS "nbre de noms de plus de 7 lettre"
FROM student
WHERE CHAR_LENGTH(last_name) > 6

Exercice 2.3.20 – Pour chaque étudiant né avant 1955, donner le nom, le résultat annuel et le 
statut. Le statut prend la valeur « OK » si l’étudiant à obtenu au moins 12 comme résultat annuel 
et « KO » dans le cas contraire

SELECT last_name , year_result ,
CASE 
WHEN year_result >= 10 THEN "OK"
WHEN year_result< 10 THEN "KO"
END AS "Statut"
FROM student
WHERE YEAR(birth_date) <= 1955


Exercice 2.3.21 – Donner pour chaque étudiant né entre 1955 et 1965 le nom, le résultat 
annuel et la catégorie à laquelle il appartient. La catégorie est fonction du résultat annuel obtenu : 
un résultat inférieur à 10 appartient à la catégorie « inférieure », un résultat égal à 10 appartient à 
la catégorie « neutre », un résultat autre appartient à la catégorie « supérieure »

SELECT last_name , year_result , 
CASE
WHEN year_result >10 THEN "Supérieur" 
WHEN year_result< 10 THEN "inférieur" 
WHEN year_result = 10 THEN "Neutre" 
END AS "Catégorie" 
FROM student
 WHERE YEAR(birth_date) BETWEEN 1955 AND 1965;


Exercice 2.3.22 – Donner pour chaque étudiant né entre 1975 et 1985, son nom, son résultat 
annuel et sa date de naissance sous la forme: jours en chiffre, mois en lettre et années en quatre 
chiffres (ex : 11 juin 2005)


SELECT last_name , year_result , 
DATE_FORMAT(birth_date, '%d-%m-%Y') AS 'Litéral_date' 
FROM student WHERE YEAR(birth_date) BETWEEN 1955 AND 1965;


Exercice 2.3.23 – Donner pour chaque étudiant né en dehors des mois d’hiver et ayant obtenu 
un résultat inférieur à 7, son nom, le mois de sa naissance (en chiffre) son résultat annuel et son 
résultat annuel corrigé (« Nouveau résultat ») tel que si le résultat annuel est égal à 4, le valeur 
proposée est « NULL »

SELECT last_name , MONTH(birth_date) AS "Mois de naissance" 
, year_result , NULLIF(year_result , 4) AS "Nouveau résultat" 
FROM student
 WHERE MONTH(birth_date) NOT IN (12,1,2,3) AND year_result < 7;


Exercice 2.3.24 – Ceci clôture la deuxième partie DRL du cours. Avant de passer à la suite
de la matière, nous vous invitons à prendre un peu de temps afin d’évaluer 
personnellement votre niveau de compréhension de la matière en vous référant aux 
derniers slides du module (slides d’auto-évaluation)




derniers slides du module (slides d’auto-évaluation)
 Partie IV : GROUP BY … HAVING
Exercice 2.4.1 – L’utilisation de « GROUP BY » peut être considérée comme une forme de 
boucle dans une requête SQL ? (Vrai/Faux) 


Exercice 2.4.2 – La répartition en groupe se fait avant de prendre en compte les restrictions 
imposées par un « WHERE » ? (Vrai/Faux)



Exercice 2.4.3 – Un « GROUP BY » doit impérativement porter sur une colonne non alliacée ?


Exercice 2.4.4 – L’utilisation d’un « GROUP BY » a pour effet de trier les résultats dans l’ordre 
croissant de la colonne incluse dans le « GROUP BY » ? (Vrai/Faux)


Exercice 2.4.5 – La colonne sur laquelle porte le « GROUP BY » doit impérativement être 
présente dans la clause « SELECT » ? (Vrai/Faux)


Exercice 2.4.6 – Les requêtes suivantes sont-elles valides ?


Exercice 2.4.7 – Donner pour chaque section, le résultat maximum (dans une colonne appelée 
« Résultat maximum ») obtenu par les étudiants 

SELECT section_id , MAX(year_result) AS "Résultat Max" FROM student GROUP BY section_id;

Exercice 2.4.8 – Donner pour toutes les sections commençant par 10, le résultat annuel moyen 
PRÉCIS (dans une colonne appelée « Moyenne ») obtenu par les étudiants 

SELECT section_id , AVG(year_result) AS "Moyen" FROM student WHERE LEFT(section_id,2) = 10 GROUP BY section_id;

Exercice 2.4.9 – Donner le résultat moyen (dans une colonne appelée « Moyenne ») et le mois 
en chiffre (dans une colonne appelée « Mois de naissance ») pour les étudiants nés le même mois 
entre 1970 et 1985 

SELECT MONTH(birth_date) AS "Mois de naissance" , AVG(year_result) AS "Moyen" FROM student WHERE YEAR(birth_date) BETWEEN 1970 AND 1985 GROUP BY MONTH(birth_date);

Exercice 2.4.10 – Donner pour toutes les sections qui comptent plus de 3 étudiants, la 
moyenne PRÉCISE des résultats annuels (dans une colonne appelée « Moyenne ») 

SELECT section_id , CONVERT(AVG(year_result), DECIMAL(20, 8)) AS "Moyenne" FROM student GROUP BY section_id HAVING COUNT(section_id) > 3;

Exercice 2.4.11 – Donner le résultat maximum obtenu par les étudiants appartenant aux 
sections dont le résultat moyen est supérieur à 8+  

SELECT section_id , CONVERT(AVG(year_result), DECIMAL(20, 8)) AS "Moyenne" , MAX(year_result) AS "Résultat maximum" FROM student GROUP BY section_id HAVING AVG(year_result) > 8;



 Partie V : CUBE et ROLLUP
 
Exercice 2.5.1 – L’utilisation de « ROLLUP » crée des groupes de données en se déplaçant dans 
une seule direction, partant de la gauche vers la droite par rapport aux colonnes sélectionnées ? 
(Vrai/Faux) 


Exercice 2.5.2 – Le résultat produit par un « ROLLUP » présente les résultats du plus agrégé au 
moins agrégé ? (Vrai/Faux) 

Exercice 2.5.3 – L’opérateur « CUBE » permet de produire moins de sous-totaux qu’avec 
l’opérateur « ROLLUP » ? (Vrai/Faux) 

Exercice 2.5.4 – Avec l’opérateur « CUBE », le nombre de groupes dans le résultat est 
indépendant du nombre de colonnes sélectionnées dans le « GROUP BY » ? (Vrai/Faux) 


Exercice 2.5.5 – L’opérateur « CUBE » ne peut pas être appliqué à la fonction d’agrégation 
« SUM » ? (Vrai/Faux) 


Exercice 2.5.6 – Donner la moyenne exacte des résultats obtenus par les étudiants par section 
et par cours, ainsi que la moyenne par section uniquement et enfin, la moyenne générale. La liste 
ainsi produite reprend l’id de section, de cours le résultat moyen (dans une colonne appelée « 
Moyenne »). Se baser uniquement sur les sections 1010 et 1320 



Exercice 2.5.7 – Donner la moyenne exacte des résultats obtenus par les étudiants par cours et
par section, ainsi que la moyenne par cours uniquement, puis par section uniquement et enfin, la 
moyenne générale. La liste ainsi produite reprend l’id de section, de cours le résultat moyen (dans 
une colonne appelée « Moyenne »). Se baser uniquement sur les sections 1010 et 1320 


Exercice 2.5.8 – Ceci clôture la troisième partie DRL du cours. Avant de passer à la suite 
de la matière, nous vous invitons à prendre un peu de temps afin d’évaluer 
personnellement votre niveau de compréhension de la matière en vous référant aux 
derniers slides du module (slides d’auto-évaluation)



 Partie VI : Jointures
Exercice 2.6.1 – Donner pour chaque cours le nom du professeur responsable ainsi que la 
section dont le professeur fait partie 


Exercice 2.6.2 – Donner pour chaque section, l’id, le nom et le nom de son délégué. Classer les 
sections dans l’ordre inverse des id de section. Un délégué est un étudiant de la table « STUDENT »


Exercice 2.6.3 – Donner pour chaque section, le nom des professeurs qui en sont membre 



Exercice 2.6.4 – Même objectif que la question 3 mais seuls les sections comportant au moins 
un professeur doivent être reprises 


Exercice 2.6.5 – Donner à chaque étudiant ayant obtenu un résultat annuel supérieur ou égal à
12 son grade en fonction de son résultat annuel et sur base de la table grade. La liste doit être 
classée dans l’ordre alphabétique des grades attribués 



Exercice 2.6.6 – Donner la liste des professeurs et la section à laquelle ils se rapportent ainsi 
que le(s) cour(s) (nom du cours et crédits) dont le professeur est responsable. La liste est triée par 
ordre décroissant des crédits attribués à un cours 



Exercice 2.6.7 – Donner pour chaque professeur son id et le total des crédits ECTS 
(« ECTS_TOT ») qui lui sont attribués. La liste proposée est triée par ordre décroissant de la somme 
des crédits alloués 



Exercice 2.6.8 – Donner la liste (nom et prénom) de l’ensemble des professeurs et des 
étudiants dont le nom est composé de plus de 8 lettres. Ajouter une colonne pour préciser la 
catégorie (S pour « STUDENT », P pour « PROFESSOR ») à laquelle appartient l’individu 



Exercice 2.6.9 – Donner l’id de chacune des sections qui n’ont pas de professeur attitré 


Exercice 2.6.10 – Ceci clôture la quatrième partie DRL du cours. Avant de passer à la 
suite de la matière, nous vous invitons à prendre un peu de temps afin d’évaluer 
personnellement votre niveau de compréhension de la matière en vous référant aux 
derniers slides du module (slides d’auto-évaluation)



















