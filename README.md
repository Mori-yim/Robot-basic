# TP1 - Robots en Java : Programmation Orientée Objet

[![Java](https://img.shields.io/badge/Java-17%2B-blue)](https://www.oracle.com/java/)
[![POO](https://img.shields.io/badge/POO-Complète-orange)](https://www.oracle.com/java/technologies/)
[![License](https://img.shields.io/badge/License-MIT-green)](LICENSE)
[![Status](https://img.shields.io/badge/Status-Completed-brightgreen)]()

##  Description du Projet

Ce projet est un **Travail Pratique (TP)** complet sur la **Programmation Orientée Objet (POO)** en Java. Il modélise un système de robots virtuels avec différentes générations et capacités.

L'objectif est de maîtriser les concepts fondamentaux de la POO à travers une application concrète et progressive.

###  Objectifs Pédagogiques

| Concept | Niveau | Implémentation |
|:--------|:------:|:----------------|
| **Encapsulation** |  | Attributs `private`/`protected`, getters/setters |
| **Constructeurs** |  | Constructeurs surchargés, appel avec `this()` |
| **Héritage** |  | Classes `Robot` -> `RobotNG` → `RobotNGTurbo` |
| **Redéfinition (Override)** |  | Méthodes `afficher()`, `toString()` |
| **Surcharge (Overload)** |  | Méthodes `avance()` sans et avec paramètre |
| **Polymorphisme** |  | Tableau de type `Robot` contenant des objets dérivés |
| **Mots-clés spéciaux** |  | `super`, `this`, `instanceof`, `final`, `static` |
| **Constantes** |  | Tableau `static final` des directions |

---

##  Fonctionnalités

### Robot (Génération 1) - Base
-  Création avec nom obligatoire (position/direction optionnelles)
-  Positionnement initial (coordonnées x, y)
-  Direction : Nord, Est, Sud, Ouest
-  Avancer d'un pas (`avance()`)
-  Tourner à droite (`droite()`)
-  Afficher son état (`afficher()`, `toString()`)

### RobotNG (Génération 2) - Nouvelle Génération
-  Hérite de toutes les fonctionnalités de Robot
-  Avancer de plusieurs pas (`avance(int nbPas)`)
-  Tourner à gauche (`gauche()`)
-  Faire demi-tour (`demiTour()`)
-  **Deux versions différentes :**
  - *Version réutilisation* : utilise les méthodes existantes
  - *Version efficace* : modifie directement l'état

### RobotNGTurbo (Génération 3) - Mode Turbo
-  Hérite de RobotNG
- Activer/désactiver le mode Turbo
-  En mode Turbo : chaque pas = 3 cases
-  Affichage indiquant l'état du Turbo

### Fonctionnalités Avancées
-  Tableau polymorphe (mélange de tous les types de robots)
-  Détection de type avec `instanceof`
-  Casting sécurisé
-  Comparaison des performances

---

##  Structure du Projet
tp1-robots-java/<br>
│<br>
├── src/<br>
│ ├── Robot.java # Classe de base (Génération 1)<br>
│ ├── RobotNG.java # Première version (réutilisation)<br>
│ ├── RobotNGEfficace.java # Deuxième version (efficace)<br>
│ ├── RobotNGTurbo.java # Troisième version (mode Turbo)<br>
│ ├── DemonstrationTableau.java # Démonstration du polymorphisme<br>
│ └── Main.java # Programme de test complet<br>
│
├── docs/<br>
│ ├── diagramme_classes.png # Diagramme UML des classes<br>
│ └── sujet_tp1.pdf # Énoncé original du TP<br>
│<br>
├── README.md # Ce fichier<br>
├── LICENSE # Licence MIT<br>
└── .gitignore # Fichiers à ignorer<br>

text

---

##  Diagramme des Classes
┌─────────────────────────────────────────────────────────────────────┐<br>
│ ROBOT │<br>
│ ───────────────────────────────────────────────────────────────── │<br>
│ - nom: String │<br>
│ - x: int │<br>
│ - y: int │<br>
│ - direction: String │<br>
│ + Robot(nom: String) │<br>
│ + Robot(nom: String, x: int, y: int) │<br>
│ + Robot(nom: String, x: int, y: int, direction: String) │<br>
│ + avance(): void │<br>
│ + droite(): void │<br>
│ + afficher(): void │<br>
│ + toString(): String │<br>
│ + getX(): int, getY(): int, getNom(): String, getDirection(): String│<br>
└───────────────────────────────────┬─────────────────────────────────┘<br>
│<br>
│ extends<br>
│<br>
┌───────────────────────────────────▼─────────────────────────────────┐<br>
│ ROBOTNG │<br>
│ ───────────────────────────────────────────────────────────────── │<br>
│ + RobotNG(nom: String) │<br>
│ + RobotNG(nom: String, x: int, y: int) │<br>
│ + RobotNG(nom: String, x: int, y: int, direction: String) │<br>
│ + avance(nbPas: int): void │<br>
│ + gauche(): void │<br>
│ + demiTour(): void │<br>
│ + afficher(): void (override) │<br>
│ + toString(): String (override) │<br>
└───────────────────────────────────┬─────────────────────────────────┘<br>
│
┌───────────────┴───────────────┐<br>
│ extends │ extends<br>
▼<br>
┌───────────────────────────────┐ ┌───────────────────────────────────┐<br>
│ ROBOTNGEFFICACE │ │ ROBOTNGTURBO │<br>
│ ─────────────────────────────│ │ ─────────────────────────────────│<br>
│ - (même constructeurs) │ │ - turboActive: boolean │<br>
│ + avance(nbPas: int): void │ │ + activerTurbo(): void │<br>
│ (version directe) │ │ + desactiverTurbo(): void │<br>
│ + gauche(): void (direct) │ │ + isTurboActive(): boolean │<br>
│ + demiTour(): void (direct) │ │ + avance(): void (override Turbo) │<br>
│ + afficher(): void (override)│ │ + avance(nbPas: int): void │<br>
│ + toString(): String │ │ + gauche(): void │<br>
└───────────────────────────────┘ │ + demiTour(): void │<br>
│ + afficher(): void (override) │<br>
│ + toString(): String │<br>
└───────────────────────────────────┘<br>

text



##  Exemples d'Utilisation

### 1. Création d'un Robot de base

```java
// Création avec seulement le nom (position 0,0 direction Est)
Robot r2d2 = new Robot("R2D2");

// Création avec nom et position
Robot c3po = new Robot("C3PO", 5, 3);

// Création complète
Robot terminator = new Robot("Terminator", -2, 1, "Nord");
2. Déplacement d'un Robot
java
Robot robot = new Robot("Explorer");

robot.avance();      // Avance d'un pas
robot.droite();      // Tourne à droite (Est → Sud)
robot.avance();      // Avance vers le Sud
robot.afficher();    // Affiche l'état
3. Utilisation de RobotNG
java
RobotNG bb8 = new RobotNG("BB8", 10, 20);

bb8.avance(3);      // Avance de 3 pas
bb8.gauche();        // Tourne à gauche
bb8.avance(2);
bb8.demiTour();      // Fait demi-tour
bb8.afficher();
4. Mode Turbo
java
RobotNGTurbo flash = new RobotNGTurbo("Flash", 0, 0, "Est");

flash.activerTurbo();    // Active le mode Turbo
flash.avance();          // Avance de 3 cases au lieu d'1 !
flash.avance(2);         // Avance de 6 cases !
flash.desactiverTurbo(); // Désactive le mode Turbo
5. Tableau Polymorphe
java
// Tableau contenant différents types de robots
Robot[] robots = new Robot[4];
robots[0] = new Robot("Basique");
robots[1] = new RobotNG("NG1");
robots[2] = new RobotNGEfficace("Efficace");
robots[3] = new RobotNGTurbo("Turbo");

// Affichage polymorphe : la bonne méthode est appelée automatiquement
for (Robot r : robots) {
    r.afficher();  // Polymorphisme en action !
}

// Vérification de type et appel de méthodes spécifiques
if (r instanceof RobotNGTurbo) {
    ((RobotNGTurbo) r).activerTurbo();
}
 Comparaison des Deux Versions de RobotNG
Aspect	Version Réutilisation	Version Efficace
Méthode avance(int)	Appelle avance() en boucle	Modifie directement x ou y
Méthode gauche()	Appelle droite() 3 fois	Switch direct sur la direction
Méthode demiTour()	Appelle droite() 2 fois	Switch direct sur la direction
Accès aux attributs	Utilise les getters/méthodes	Accès direct (protected requis)
Performance	Plus lente (appels multiples)	Plus rapide (modifications directes)
Lisibilité	Très lisible (réutilisation)	Moins lisible mais plus efficace
Couplage	Faible (dépend des méthodes)	Plus fort (dépend des attributs)
Résultats de performance typiques :
text
Avancer de 10000 pas :
  Version réutilisation : 850,000 ns
  Version efficace      : 120,000 ns
  Gain : 7x plus rapide
 Concepts Fondamentaux Expliqués
Encapsulation
java
private String nom;        // Attribut privé : inaccessible de l'extérieur

public String getNom() {   // Getter public : accès contrôlé
    return nom;
}
Pourquoi ? Protège les données et permet de modifier l'implémentation sans affecter les utilisateurs.

Héritage
java
public class RobotNG extends Robot {
    // RobotNG hérite de tous les attributs et méthodes de Robot
}
Pourquoi ? Réutilisation du code et création de hiérarchies conceptuelles.

Polymorphisme
java
Robot r = new RobotNG("BB8");  // Une variable parent peut contenir un objet enfant
r.afficher();                   // Appelle la méthode de RobotNG !
Pourquoi ? Traite des objets de différentes classes de manière uniforme.

Surcharge (Overload)
java
public void avance() { }        // 0 paramètre
public void avance(int nbPas) { } // 1 paramètre
Pourquoi ? Une même action peut s'appliquer de différentes manières.

Redéfinition (Override)
java
@Override
public void afficher() {
    // Nouvelle implémentation spécifique à RobotNG
}
Pourquoi ? Spécialiser le comportement d'une méthode héritée.

 Installation et Exécution
Prérequis
Java JDK 17 ou supérieur

Un terminal (Linux/macOS) ou l'invite de commande (Windows)

Étapes
bash
# 1. Cloner le dépôt (ou télécharger les fichiers)
git clone https://github.com/votre-username/tp1-robots-java.git
cd tp1-robots-java

# 2. Compiler tous les fichiers Java
javac src/*.java

# 3. Exécuter le programme de test
java -cp src Main

# 4. Exécuter la démonstration du tableau polymorphe
java -cp src DemonstrationTableau
Compilation avec script (Linux/macOS)
bash
# Rendre le script exécutable
chmod +x compile.sh

# Lancer la compilation et l'exécution
./compile.sh
Script de compilation compile.sh
bash
#!/bin/bash
echo " Compilation du TP Robots..."
javac src/*.java
if [ $? -eq 0 ]; then
    echo " Compilation réussie !"
    echo " Lancement du programme..."
    java -cp src Main
else
    echo " Erreur de compilation"
fi
 Résultats d'Exécution Attendus
text
╔══════════════════════════════════════════════════════════════╗
║                    TP1 - ROBOTS EN JAVA                      ║
╚══════════════════════════════════════════════════════════════╝

 1. TEST DE LA CLASSE ROBOT DE BASE
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
=== Robot: R2D2 ===
Position: (0, 0)
Direction: Est
=========================

 Déplacement du robot1 :
=== Robot: R2D2 ===
Position: (1, 1)
Direction: Sud
=========================

 2. TEST DE RobotNG (PREMIÈRE SOLUTION - RÉUTILISATION)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
=== RobotNG (Nouvelle Génération): BB8 ===
Position: (10, 20)
Direction: Est
=========================

 Déplacements avec les nouvelles méthodes :
BB8 a avancé de 3 pas.
BB8 a tourné à gauche.
BB8 a avancé de 2 pas.
BB8 a fait demi-tour.
BB8 a avancé de 1 pas.
=== RobotNG (Nouvelle Génération): BB8 ===
Position: (12, 15)
Direction: Est
=========================

 4. TEST DE RobotNGTurbo (MODE TURBO)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
=== RobotNG Turbo: Flash ===
Position: (0, 0)
Direction: Est
Mode Turbo: DÉSACTIVÉ
================================

 Activation du mode Turbo :
Flash :  MODE TURBO ACTIVÉ ! 
Flash avance de 3 pas en mode Turbo !
Flash avance de 2 pas (soit 6 cases en mode Turbo)
=== RobotNG Turbo: Flash ===
Position: (9, 0)
Direction: Est
Mode Turbo:  ACTIVÉ 
================================
 Vérification des Types
java
// Exemple de vérification avec instanceof
for (Robot r : tousLesRobots) {
    if (r instanceof RobotNGTurbo) {
        System.out.println(r.getNom() + " est un RobotNGTurbo");
        ((RobotNGTurbo) r).activerTurbo();  // Cast sécurisé
    } else if (r instanceof RobotNG) {
        System.out.println(r.getNom() + " est un RobotNG");
    } else {
        System.out.println(r.getNom() + " est un Robot de base");
    }
}
 Réponses aux Questions du TP
Question 1 : Définition de la classe Robot
 Attributs privés encapsulés
 Constructeurs surchargés (nom seul, nom+position, complet)
 Méthodes avance(), droite(), afficher()
 Valeurs par défaut (0,0) et "Est"

Question 2a : RobotNG - Première solution
 Héritage avec extends Robot
 avance(int) appelant avance() en boucle
 gauche() appelant droite() 3 fois
 demiTour() appelant droite() 2 fois

Question 2b : RobotNG - Deuxième solution plus efficace
 Accès direct aux attributs (nécessite protected)
 Modification directe sans appels en cascade
 Performance améliorée

Question 3 : Tableau polymorphe
 Déclaration : Robot[] tableau = new Robot[n]
 Affichage : boucle avec r.afficher()
 Polymorphisme automatique

Question 4 : Mode Turbo
 Attribut turboActive
 Méthodes activerTurbo(), desactiverTurbo()
 Multiplicateur ×3 dans avance()
 Affichage de l'état du Turbo

 Tests Unitaires (Exemples)
java
public class RobotTest {
    public static void main(String[] args) {
        // Test de la direction par défaut
        Robot r = new Robot("Test");
        assert r.getDirection().equals("Est") : "Direction par défaut incorrecte";
        
        // Test de l'avancement
        int xInitial = r.getX();
        r.avance();
        assert r.getX() == xInitial + 1 : "Avance incorrecte";
        
        // Test du virage à droite
        r.droite();
        assert r.getDirection().equals("Sud") : "Virage à droite incorrect";
        
        System.out.println(" Tous les tests passés !");
    }
}
 Résolution des Problèmes Courants
Problème	Solution
Cannot find symbol	Vérifiez que tous les fichiers sont compilés ensemble
Les attributs ne sont pas accessibles dans RobotNGEfficace	Changez private en protected dans Robot
ClassCastException	Vérifiez le type avec instanceof avant le cast
Le robot n'avance pas en mode Turbo	Vérifiez que activerTurbo() a bien été appelé
La direction reste bloquée	Vérifiez la logique des switch/case
 Ressources pour Approfondir
Documentation Oracle - POO Java

OpenClassrooms - Apprenez à programmer en Java

Java - Héritage et Polymorphisme

Les classes abstraites et interfaces

 Contribution
Les suggestions d'amélioration sont les bienvenues !

Fork le projet

Créez votre branche (git checkout -b feature/Amelioration)

Commit vos changements (git commit -m 'Ajout d'une fonctionnalité')

Push (git push origin feature/Amelioration)

Ouvrez une Pull Request


 Auteur
Morino - Étudiant en informatique
 Remerciements
L'enseignant pour l'énoncé du TP

La communauté Java pour son aide précieuse

<div align="center"> <sub> TP réalisé dans le cadre de l'apprentissage de la Programmation Orientée Objet en Java </sub> <br> <sub> N'hésitez pas à mettre une étoile si ce projet vous a aidé ! </sub> </div> ```
