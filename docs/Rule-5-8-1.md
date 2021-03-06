# Rule 5.8.1
## Summary

This test consists in checking whether each layout table does not use
elements used for data tables.

## Business description

### Criterion

[5.8](http://references.modernisation.gouv.fr/sites/default/files/RGAA3_RC2-1/referentiel_technique.htm#crit-5-8)

### Test

[5.8.1](http://references.modernisation.gouv.fr/sites/default/files/RGAA3_RC2-1/referentiel_technique.htm#test-5-8-1)

### Description

Chaque <a href="http://references.modernisation.gouv.fr/sites/default/files/RGAA3_RC2-1/glossaire.htm#mTabMiseForme">tableau de mise en forme</a> (balise `table`) v&eacute;rifie-t-il ces conditions ? 
 
 *  Le <a href="http://references.modernisation.gouv.fr/sites/default/files/RGAA3_RC2-1/glossaire.htm#mTabMiseForme">tableau de mise en forme</a> (balise `table`) ne poss&egrave;de pas de balises `caption`, `th`, `thead`, `tfoot` 
 *  Les cellules du <a href="http://references.modernisation.gouv.fr/sites/default/files/RGAA3_RC2-1/glossaire.htm#mTabMiseForme">tableau de mise en forme</a> (balise `td`) ne poss&egrave;dent pas d'attributs `scope`, `headers`, `colgroup`, `axis`. 


### Level

**A**

## Technical description

### Scope

**page**

### Decision level

**semidecidable**

## Algorithm

### Selection

**Set1 (table tags identified as presentation table from html markers)**

All the <table\> tags with an "id" attribute or a "class" attribute or a
"role" attribute that matches one of the values set by the user through
the "PRESENTATION\_TABLE\_MARKER" parameter

**Set2 (table tags not identified as data table or presentation table
from html markers)**

All the <table\> tags that don't have an "id" attribute or a "class"
attribute or a "role" attribute that matches one the values set by the
user through the "PRESENTATION\_TABLE\_MARKER" parameter or the
"DATA\_TABLE\_MARKER" parameter. That means select all the table tags of
the page when the parameters are empty.

### Process

**Test1 :**

For each element of Set1, test the absence of one the following tags as
children tag :

-   caption
-   th
-   thead
-   tfoot
-   colgroup
-   td[scope]
-   td[headers]
-   td[axis]

For each occurence of false-result of Test1, raise a MessageA

**Test2 :**

For each element of Set2, test the absence of one the following tags as
children tag :

-   caption
-   th
-   thead
-   tfoot
-   colgroup
-   td[scope]
-   td[headers]
-   td[axis]

For each occurence of false-result of Test2, raise a MessageB

For each occurence of true-result of Test2, raise a MessageC

###### MessageA : Presentation table with forbidden markup

-   code :PresentationTableWithForbiddenMarkup
-   status: Failed
-   parameter : Snippet
-   present in source : yes

###### MessageB : Check the table is a data table

-   code :CheckTableIsDataTable
-   status: NMI
-   parameter : Snippet
-   present in source : yes

###### MessageC : Check the table is a presentation table

-   code :CheckTableIsPresentationTable
-   status: NMI
-   parameter : Snippet
-   present in source : yes

### Analysis

**Passed : \
**

Test1 returns true for all elements and Set2 is empty (all the tables of
the page are identified by marker and none of the presentation ones
contain forbidden child element)

**Failed : \
**

Test1 returns false for at least one element (at least one table
identified as presentation table by marker contains forbidden child
element) **\
**

**NA : \
**

Set1 and Set2 are empty (the page has no table tags or only data table
identified by marker)

#### Pre-qualified :

Set1 is empty or Test1 returns true for all elements AND Set2 is not
empty (the page contains not identified tables that need to be manually
checked and no table identified as presentation contain forbidden child
element)

## Notes

No notes yet for that rule
