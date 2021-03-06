# TP
1° export articles.csv (déjà fait)
2° export client.csv 
    => rajouter l'age
    => déplacer le code dans un service : ExportArticleService
3° export client.xlsx avec la mise en forme demandée (cf fichier 04-clients-excel.xlsx)
4° export total factures (cf fichier 05-factures-excel.xlsx)
5° export PDF d'une facture (format au choix)

# Fonctionnement
Ouvrir le projet dans eclipse ou intellij.
Démarrer l'application avec la classe 'main' : com.example.demo.DemoApplication

## IHM 1 : Server side templating
Se connecter à la home page en accédant à l'url : http://localhost:9092/
Il s'agit d'une application Spring boot intégrant une petite base de données en mémoire.
L'application simule la gestion d'une base d'articles de clients et de factures.

## IHM 2 : Utiliser l'application angular
Cf README du projet ijva250-angular-app

# Data
Améliorer ses jeux de données (voir classe com.example.demo.service.InitData):
* Ajouter des données de tests (des nouveaux clients ou articles ...)
* Ajouter une nouvelle informations : la quantité d'article en stock
* Ajouter une nouvelle info age des clients

## CSV
Un fichier CSV est un fichier texte "à plat". Chaque ligne correspond à une ligne du tableau, chaque colonne est séparée par des ";"
Le contenu d'une cellule peut être entourée de double quotes
* Exporter la liste des clients au format CSV (colonnes: nom, prénom) => accessible via le lien csv dans la home page
* Ajouter une nouvelle colonne : age du client
* Bonus fiabiliser l'export ajouter la colonne description sur l'article (autorisant les caractères spéciaux ; et saut de ligne) 
et réaliser l'export du stock article en gérant ces caractères spéciaux.

## XLSX
Faire de même avec un export au format xlsx. Cela correspond au format Excel permettant des fichiers plus complexe (onglets, fusion de cellule, styles, formules, ...)
Exemple de code pour réaliser un fichier xslx
```
Workbook workbook = new XSSFWorkbook();
Sheet sheet = workbook.createSheet("Clients");
Row headerRow = sheet.createRow(0);
Cell cellPrenom = headerRow.createCell(0);
cellPrenom.setCellValue("Prénom");
workbook.write(fileOutputStream);
workbook.close();
```
Exercice:
* Créer un export XLSX de tous les clients (colonnes: nom, prénom) => accessible via le lien xlsx dans la home page
* Créer un export XLSX multi onglet : un pour le client sélectionné, et créer un onglet par factures correspondant au client
    chaque onglet contiendra le détail de la facture (colonnes : désignation, quantité, prixUnitaire, prixLigne) et rajouter le prix total de la facture en bas (utilise un colspan)
     => accessible via le lien "Télécharger toutes ses factures" dans la home page

## PDF (iText)
* Créer le PDF d'une facture entete : Nom prénom du client, tableau contenant le détail de la facture, prix total de la facture en dessous 
=> accessible via le lien pdf dans la home page
Astuce, il faut importer les classe com.itextpdf.* et non com.lowagi.*
AIDE : https://developers.itextpdf.com/examples/itext-action-second-edition/chapter-1

## CSV amélioré (BONUS a faire après)
Créer un objet permettant d'améliorer l'export.
* Bonus voir la méthode com.example.demo.service.export.ExportCSVService.exportAmeliorer et analyser comment cet export fonctionne et qu'est ce que cela apporte

## PDF (birt) (BONUS on verra ensemble)
Birt est un outil de templating pour générer des PDF (et autres)
Télécharer birt all in one  http://download.eclipse.org/birt/downloads/
créer un nouveau report
utiliser une datasource XML
* Créer un service de génération de PDF via BIRT : le service utilise un template birt et founit un dataset xml pour créer le PDF.

PS :
Ajouter des bordures, des images, des polices, des couleurs, du gras souligné etc...
