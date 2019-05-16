# Skripte für Junos On-Box-Automatisierung

Junos unterscheidet zwischen op-, Commit- und Event-Scripts. Syntaktisch sind diese gleich, jedoch werden op-Skripte im operational mode via ```op skript-name``` manuell ausgeführt, Commit-Skripte automatisch beim Start eines Commits und Event-Skripte beim Auftreten eines bestimmten Ereignisses, welches in einer Event-Policy konfiguriert wird.

Juniper Dokumentation: https://www.juniper.net/documentation/en_US/junos/information-products/pathway-pages/config-guide-automation/config-guide-automation.html


## Voraussetzungen & Skriptsprachen

Junos Devices ab Version 16.1 unterstützen Python on-box; frühere Versionen unterstützen nur XLST und SLAX. Devices bis 14.1 unterstützen nur SLAX Version 1.0.


## Installation & Aktivierung

Skripte müssen sich unter ```/var/db/scripts/op|commit|event``` befinden und müssen in der Konfiguration aktiviert werden:

    # set system scripts commit file filename.slax
    # set system scripts op file filename.slax alias commandname
    # set event-options event-script file filename.slax

Für die Ausführung eines Event-Skripts muss zusätzlich noch eine Policy konfiguriert werden, z.B.:

    # set event-options policy auto-rollback events ui_commit_completed then event-script filename.slax

(Mit dem obigen Beispiel-Event ```ui_commit_completed``` wird eine Aktion erst mit Beendigung eines Commits ausgeführt, nicht bei Beginn wie im Falle eines Commit-Skripts)


## Junos XML RPCs

RPC für eine bestimmte Junos-Operation oder Konfiguration anzeigen:

    > ping 10.1.1.1 count 5 | display xml rpc


## SLAX Syntax

### Variablen

In SLAX Version 1.0 gibt es nur 'immutable' Variablen, d.h. nachdem eine Variable deklariert wurde, kann ihr Wert nicht mehr verändert werden.

    var $variable-name = value;


### Strings

Strings können in einfache oder doppelte Anführungszeichen eingeschlossen werden. String concatenation erfolt durch underscore (_).


### Kommentare

    /* This is a comment. */


### Line Temination

SLAX Statements werden mit Semikolon terminiert.


### Boilerplate code

    version 1.0;
    ns junos = "http://xml.juniper.net/junos/*/junos";
    ns xnm = "http://xml.juniper.net/xnm/1.1/xnm";
    ns jcs = "http://xml.juniper.net/junos/commit-scripts/1.0";
    import "../import/junos.xsl";

    match / {

        /* your code here */

    }
