# Skripte für Junos On-Box-Automatisierung

Junos Devices ab Version 16.1 unterstützen Python on-box; frühere Versionen unterstützen XLST und SLAX. Devices bis 14.1 unterstützen nur SLAX Version 1.0.

Junos unterscheidet zwischen op- und commit-Skripten. Syntaktisch sind diese gleich, jedoch werden op-Skripte im operational mode via ```op skript-name``` manuell ausgeführt und commit-Skripte automatisch während eines Commits.

Juniper Dokumentation: https://www.juniper.net/documentation/en_US/junos/information-products/pathway-pages/config-guide-automation/config-guide-automation.html


## Junos XML RPCs

RPC für eine bestimmte Junos-Operation oder Konfiguration anzeigen:

    ipb@lr1.b5-1> ping 10.1.1.1 count 5 | display xml rpc


## SLAX Syntax

### Boilerplate code

    version 1.0;
    ns junos = "http://xml.juniper.net/junos/*/junos";
    ns xnm = "http://xml.juniper.net/xnm/1.1/xnm";
    ns jcs = "http://xml.juniper.net/junos/commit-scripts/1.0";
    import "../import/junos.xsl";

    match / {

        /* your code here */

    }


### Comments

    /* This is a comment. */


### Line Temination

SLAX statements are terminated with a semicolon.


### Strings

Strings can be enclosed in either single quotes or double quotes. Strings can be concatenated together using an underscore (_).


