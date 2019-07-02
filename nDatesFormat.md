# Formats de dates

Outils

https://github.com/inukshuk/edtf.js

https://github.com/nicompte/edtfy

http://www.loc.gov/standards/datetime/implementations.html

## ISO DIS 8601, Data elements and interchange formats -- Information interchange -- Representation of dates and times

La révision de l’ISO 8601-2004 intègre diverses fonctionnalités développées par la bibliothèque du congrès avec l’Extended Date/Time Format (EDTF) mais avec des modifications de syntaxe. Cette spécification se compose de deux parties.

En 2018, la révision de la norme était soumise au vote.

- Part 1: Basic rules https://www.iso.org/standard/70907.html
- Part 2: Extensions https://www.iso.org/standard/70908.html

cf. Brouillons :

- https://web.archive.org/web/20171020084445/https://www.loc.gov/standards/datetime/ISO_DIS%208601-1.pdf
- https://web.archive.org/web/20171020085148/https://www.loc.gov/standards/datetime/ISO_DIS%208601-2.pdf

## Extended Date/Time Format (EDTF)

https://www.loc.gov/standards/datetime/

L’Extended Date/Time Format définit des fonctionnalités concernant le format des dates plus expressives que celles spécifiées dans le standard international pour la représentation des dates et du temps (ISO 8601-2004). 

Fonctionnalités prises en charge

Un profil de ISO 8601

- les mentions de mois, année, jour

  2001-02-03, 2008-12, 2008

- les précisions temporelles

  2001-02-03T09:30:01, 2004-01-01T10:10:10Z, 2004-01-01T10:10:10+05:00 : Date ‘T’ time   followed by either nothing, “Z” or zone offset. Zone-offset:   '+' or '-' followed by a 2-digit hour, followed optionally by a colon and the 2-digit minutes 

- les intervales de dates

  1964/2008, 2004-06/2006-08, 2004-02-01/2005-02-08, précision différente pour les dates de début et de fin : 2004-02-01/2005-02, 2004-02-01/2005, 2005/2006-02

Extensions proposées

- les incertitudes (?)

  1984?, 2004-06?, 2004-06-11?

- les approximations (~)

  1984~, 2004-06~, 2004-06-11~

- les éléments non spécifiés (u)

  une année non spécifiée dans les années 1990 : 199u, des années non spécifiées au 20e siècle : 19uu, un mois de 1999 : 1999-uu, un jour de janvier 1999 : 1999-01-uu, un jour de 1999 : 1999-uu-uu

- les intervales étendus

  début inconnu : unknown/2006, fin inconnue : 2004-04-01/unknown, pas de date de fin : 2004-01-01/open, 1984~/2004-06, 1984-06-02?/2004-08-08~

- années de plus de 4 digits

  y1700002, y-1700002 

- saisons

  printemps 2001-21, été 2003-22, automne 2000-23, hiver 2010-24

Extension plus complexes

- 2004?-06-11,  uncertain year; month, day known 
- 2004-06~-11,  year and month  approximate; day known
- 2004-06-(11)~, day approximate; year, month known
- 2004-(06)~-11, month approximate, year and day known
- 15uu-12-25, December 25 sometime during the 1500s
- y17e7 the year 170000000 (contrast with y170000000 of level 1)
- y-17e7   the year -170000000
- y17101e4p3   Some year between 171000000 and 171999999, estimated to be 171010000 ('p3' indicates a precision of 3 significant digits.)

Un premier [brouillon de recommandation](https://www.loc.gov/standards/datetime/pre-submission.html) a été publié en 2012 et il existe plusieurs [implémentations](https://www.loc.gov/standards/datetime/implementations.html). La spécification prend la forme d’un profil ou d’une extension de l’ISO 8601-2004. Les fonctionnalités de EDTF ont été intégrées dans le brouillon de la révision de l’ISO 8601 qui devait être publiée en 2018.

Présentation powerpoint https://web.archive.org/web/20170131100720/https://www.loc.gov/standards/datetime/edtf.pptx

## XML Schema Data Language

https://www.w3.org/TR/xmlschema11-2/#dateTime

## ISO 8601-2004, Data elements and interchange formats -- Information interchange -- Representation of dates and times

https://www.iso.org/standard/40874.html

ISO 8601:2004 is applicable whenever representation of dates in the Gregorian calendar, times in the 24-hour timekeeping system, time intervals and recurring time intervals or of the formats of these representations are included in information interchange. It includes

- calendar dates expressed in terms of calendar year, calendar month and calendar day of the month;
- ordinal dates expressed in terms of calendar year and calendar day of the year;
- week dates expressed in terms of calendar year, calendar week number and calendar day of the week;
- local time based upon the 24-hour timekeeping system;
- Coordinated Universal Time of day;
- local time and the difference from Coordinated Universal Time;
- combination of date and time of day;
- time intervals;
- recurring time intervals.

ISO 8601:2004 does not cover dates and times where words are used in the representation and dates and times where characters are not used in the representation.

ISO 8601:2004 does not assign any particular meaning or interpretation to any data element that uses representations in accordance with ISO 8601:2004. Such meaning will be determined by the context of the application.



Soyons progressifs