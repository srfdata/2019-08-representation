# 2019-08-representation

## Vorbemerkungen

Dieses Dokument beschreibt die Vorprozessierung und explorative Analyse des Datensatzes, der Grundlage des auf srf.ch veröffentlichten Artikels [Wie das Parlament die Wähler abbildet – und wie nicht](https://www.srf.ch/news/schweiz/wahlen-2019/wahlen-2019-wie-das-parlament-die-waehler-abbildet-und-wie-nicht) ist.

SRF Data legt Wert darauf, dass die Datenvorprozessierung und -Analyse nachvollzogen und überprüft werden kann. SRF Data glaubt an das Prinzip offener Daten, aber auch offener und nachvollziehbarer Methoden. Zum anderen soll es Dritten ermöglicht werden, auf dieser Vorarbeit aufzubauen und damit weitere Auswertungen oder Applikationen zu generieren.

Das Endprodukt des vorliegenden Scripts, neben der explorativen Analyse, sind (Datenbeschreibung siehe unten):

* `councillors.json`: Datensatz aller Parlamentarier mit Geschlecht, Altersgruppe, Stadt-Land-Kategorisierung, Zivilstand, Bildung und Religionszugehörigkeit als JSON
* `representation.json`: Datensatz mit Ist- und Soll-Werten für die untersuchten Kategorien (Geschlecht, Altersgruppe etc.) als JSON


### R-Script & Daten

Die Vorprozessierung und Analyse wurde im Statistikprogramm R vorgenommen. Das zugrunde liegende Script sowie die prozessierten Daten können unter [diesem Link](https://srfdata.github.io/2019-08-representation/rscript.zip) heruntergeladen werden. Durch Ausführen von `main.Rmd` kann der hier beschriebene Prozess nachvollzogen und der für den Artikel verwendete Datensatz generiert werden. Dabei werden Daten aus dem Ordner `input` eingelesen und Ergebnisse in den Ordner `output` geschrieben. 

SRF Data verwendet das [rddj-template](https://github.com/grssnbchr/rddj-template) von Timo Grossenbacher als Grundlage für seine R-Scripts. Entstehen bei der Ausführung dieses Scripts Probleme, kann es helfen, die Anleitung von [rddj-template](https://github.com/grssnbchr/rddj-template) zu studieren.

### GitHub

Der Code für die vorliegende Datenprozessierung ist auf [https://github.com/srfdata/2019-08-representation](https://github.com/srfdata/2019-08-representation) zur freien Verwendung verfügbar.

### Lizenz

<a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/"><img alt="Creative Commons Lizenzvertrag" style="border-width:0" src="https://i.creativecommons.org/l/by-sa/4.0/88x31.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" href="http://purl.org/dc/dcmitype/Dataset" property="dct:title" rel="dct:type">2019-08-representation</span> von <a xmlns:cc="http://creativecommons.org/ns#" href="https://github.com/srfdata/2019-08-representation" property="cc:attributionName" rel="cc:attributionURL">SRF Data</a> ist lizenziert unter einer <a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">Creative Commons Namensnennung - Weitergabe unter gleichen Bedingungen 4.0 International Lizenz</a>.

### Weitere Projekte

Code & Daten von [SRF Data](http://srf.ch/data) sind unter [http://srfdata.github.io](http://srfdata.github.io) verfügbar.

### Haftungsausschluss

Die veröffentlichten Informationen sind sorgfältig zusammengestellt, erheben aber keinen Anspruch auf Aktualität, Vollständigkeit oder Richtigkeit. Es wird keine Haftung übernommen für Schäden, die  durch die Verwendung dieses Scripts oder der daraus gezogenen Informationen entstehen. Dies gilt ebenfalls für Inhalte Dritter, die über dieses Angebot zugänglich sind.

### Datenbeschreibung 

#### `councillors_supplemented.csv`

| Attribut | Typ | Beschreibung |
|-------|------|-----------------------------------------------------------------------------|
| id | Numeric | Offizielle Id der Parlamentarischen Dienste |
| fistName | String | Vorname der Parlamentarier |
| lastName | String | Nachname der Parlamentarier |
| ageGroup | String | Altersgruppe der Parlamentarier (sieben Kategorien) |
| gender | String | Geschlecht der Parlamentarier (m, f) |
| urbanRural | String | Stadt-Land-Einteilung der Parlamentarier gemäss Raumgliederung des BfS, vier Kategorien (big_city, urban, periurban, rural) |
| maritalStatus | String | Zivilstand der Parlamentarier |
| education | String | Höchste Ausbildung der Parlamentarier |
| religion | String | Religionszugehörigkeit der Parlamentarier |
| party | String | Partei der Parlamentarier |


#### `representation.csv`

| Attribut | Typ | Beschreibung |
|-------|------|-----------------------------------------------------------------------------|
| category | String | Kategoriebezeichnung in Englisch für die jeweilige demografische Angabe |
| group | String | Unterschiedliche Einteilungen der jeweiligen Kategorie (Geschlecht, Altersgruppen etc.) |
| is | Numeric | Ist-Wert für eine Gruppe: So viele Parlamentarier unter 30 Jahren sitzen im Parlament |
| should | Numeric | Soll-Wert für eine Gruppe: So viel Parlamentarier unter 30 Jahren müssten im Vergleich zur ständigen Wohnbevölkerung über 15 Jahren im Parlament sitzen |


### Originalquelle

#### Schweizer Parlamentarier (National- und Ständerat), Stand 28. Mai 2019 

&rarr; `input/councillorsCouncillor-export_de_ergaenzt_mit_religion.csv`

Die Daten über die Parlamentarier stammen von den [Parlamentarischen Diensten](https://www.parlament.ch/de/%C3%BCber-das-parlament/parlamentsdienste) und wurden von [Smartvote](https://www.smartvote.ch/) durch die eigene Datenbank und weitere Recherchen ergänzt. Im Datensatz befinden sich neben den verwendeten Kategorien auch noch weitere Angaben (Beruf, Sprache etc.) enthalten.

#### Ergänzung zu den Daten der Parlamentarier

&rarr; `input/Missing Data Parlamentarians - Sheet1.csv`

Ergänzung des obigen Datensatzes durch eigene Recherche. 99 Parlamentarier wurden per Mail (Code für den automatisierten Mailversand weiter unten) angefragt, fehlende Daten zu ergänzen. Davon haben 64 Parlamentarier geantwortet.

#### Ständige Wohnbevölkerung nach Alter

&rarr; `input/je-d-01.02.03.02.xlsx`

Die Daten zur ständigen Wohnbevölkerung nach Alter haben wir von der [Webseite](https://www.bfs.admin.ch/bfs/de/home/statistiken/bevoelkerung/stand-entwicklung/alter-zivilstand-staatsangehoerigkeit.assetdetail.5866882.html) des Bundesamts für Statistik (BfS) heruntergeladen.

#### Ständige Wohnbevölkerung nach Religionszugehörigkeit

&rarr; `input/je-d-01.08.02.01.xlsx`

Die Daten zur ständigen Wohnbevölkerung ab 15 Jahren nach Religionszugehörigkeit haben wir von der [Webseite](https://www.bfs.admin.ch/bfs/de/home/statistiken/bevoelkerung/sprachen-religionen/religionen.assetdetail.7226715.html) des BfS heruntergeladen.

#### Ständige Wohnbevölkerung nach Zivilstand

&rarr; `input/su-d-01.02.03.03.xlsx`

Die Daten zur ständigen Wohnbevölkerung nach Zivilstand haben wir von der [Webseite](https://www.bfs.admin.ch/bfs/de/home/statistiken/kataloge-datenbanken/tabellen.assetdetail.5886132.html) des BfS heruntergeladen.

#### Ständige Wohnbevölkerung nach Bildung

&rarr; `input/su-d-40.02.15.08.01-2017.xlsx`

Die Daten zur ständigen Wohnbevölkerung ab 15 Jahren nach Bildung haben wir von der [Webseite](https://www.bfs.admin.ch/bfs/de/home/statistiken/kataloge-datenbanken/tabellen.assetdetail.7226522.html) des BfS heruntergeladen.

####  Ständige Wohnbevölkerung nach Alter und Gemeinde (Stand 31.12.2017)

&rarr; `input/su-d-01.02.03.06.xlsx`

Die Daten zur ständigen Wohnbevölkerung nach Alter und Gemeinde haben wir von der [Webseite](https://www.bfs.admin.ch/bfs/de/home/statistiken/kataloge-datenbanken/tabellen.assetdetail.5886142.html) des BfS heruntergeladen.

####  Raumgliederung

&rarr; `input/Raumgliederungen.xlsx`

Die Einteilung der Wohnorte der Parlamentarier in urban, periurban und rural haben wir der Raumgliederung des BfS entnommen (Gemeindetypologie 2012, 25 Typen, 9 Kategorien und Stadt/Land-Typologie). Die Tabelle haben wir aus der [Applikation der Schweizer Gemeinden](https://www.agvchapp.bfs.admin.ch/de/typologies/query) des BfS exportiert. Wir haben den offiziellen Gemeindestand vom 02.04.2017 verwendet mit 2240 Einträgen.