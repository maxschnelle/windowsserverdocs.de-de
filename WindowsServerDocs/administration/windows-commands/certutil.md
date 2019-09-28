---
title: certutil
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c264ccf0-ba1e-412b-9dd3-d77dd9345ad9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 45c9946cc53fe3a901c3f6ee53f082a5b3d086c0
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71379651"
---
# <a name="certutil"></a>certutil

Certutil. exe ist ein Befehlszeilenprogramm, das als Teil der Zertifikat Dienste installiert wird. Mithilfe von "Certutil. exe" können Sie Konfigurationsinformationen der Zertifizierungsstelle (Certification Authority, ca) sichern und anzeigen, Zertifikat Dienste konfigurieren, ZS-Komponenten sichern und Wiederherstellen und Zertifikate, Schlüsselpaare und Zertifikat Ketten überprüfen.

Wenn certutil auf einer Zertifizierungsstelle ohne zusätzliche Parameter ausgeführt wird, wird die aktuelle Zertifizierungsstellen Konfiguration angezeigt. Wenn cerutil auf einer nicht Zertifizierungsstelle ausgeführt wird, wird für den Befehl standardmäßig das "Certutil [-Dump"-](#-dump) Verb ausgeführt.

> [!WARNING]
> Frühere Versionen von certutil bieten möglicherweise nicht alle Optionen, die in diesem Dokument beschrieben werden. Sie können alle Optionen anzeigen, die eine bestimmte Version von certutil bereitstellt, indem Sie die im Abschnitt [Syntax Notations](#syntax-notations) aufgeführten Befehle ausführen.

## <a name="menu"></a>Menü

Die Hauptabschnitte in diesem Dokument lauten:

- [Verbund](#verbs)
- [Syntax Notationen](#syntax-notations)
- [Options](#options)
- [Weitere certutil-Beispiele](#additional-certutil-examples)

## <a name="verbs"></a>Verben

In der folgenden Tabelle werden die Verben beschrieben, die mit dem certutil-Befehl verwendet werden können.

|Verben|Beschreibung|
|-----|-----------|
|[-Dump](#-dump)|Konfigurationsinformationen oder Dateien sichern|
|[-ASN](#-asn)|Analysieren der ASN. 1-Datei|
|[-decodehex](#-decodehex)|Hexadezimal codierte Datei decodieren|
|[-Decodieren](#-decode)|Decodieren einer Base64-codierten Datei|
|[-Codieren](#-encode)|Codieren einer Datei in Base64|
|[-verweigern](#-deny)|Ablehnen einer ausstehenden Zertifikat Anforderung|
|[-erneut übermitteln](#-resubmit)|Ausstehende Zertifikat Anforderung erneut übermitteln|
|[-----Tributes](#-setattributes)|Festlegen von Attributen für eine ausstehende Zertifikat Anforderung|
|[-abtextension](#-setextension)|Festlegen einer Erweiterung für eine ausstehende Zertifikat Anforderung|
|[-widerrufen](#-revoke)|Sperren eines Zertifikats|
|[-IsValid](#-isvalid)|Anzeigen der Disposition des aktuellen Zertifikats|
|[-GetConfig](#-getconfig)|Standard Konfigurations Zeichenfolge erhalten|
|[-Ping](#-ping)|Versuch, eine Verbindung mit der Active Directory-Zertifikat Dienste-Anforderungs Schnittstelle aufzunehmen|
|-pingadmin|Es wurde versucht, die Administrator Oberfläche der Active Directory Zertifikat Dienste zu kontaktieren.|
|[-Cainfo](#-cainfo)|Anzeigen von Informationen zur Zertifizierungsstelle|
|[-ca. cert](#-cacert)|Abrufen des Zertifikats für die Zertifizierungsstelle|
|[-ca. Chain](#-cachain)|Abrufen der Zertifikat Kette für die Zertifizierungsstelle|
|[-Getcrl](#-getcrl)|Rufen Sie eine Zertifikat Sperr Liste (CRL) ab.|
|[-CRL](#-crl)|Neue Zertifikat Sperr Listen (CRLs) [oder nur Delta-CRLs] veröffentlichen|
|[-Herunterfahren](#-shutdown)|Herunterfahren Active Directory Zertifikat Dienste|
|[-installCert](#-installcert)|Installieren eines Zertifizierungsstellen Zertifikats|
|[-verläncert](#-renewcert)|Erneuern eines Zertifizierungsstellen Zertifikats|
|[-Schema](#-schema)|Sichern Sie das Schema für das Zertifikat.|
|[-Ansicht](#-view)|Zertifikat Ansicht sichern|
|[-DB](#-db)|Sichern der rohdatenbankdatenbank|
|[-deleteRow](#-deleterow)|Löschen einer Zeile aus der Server Datenbank|
|[-Sicherung](#-backup)|Backup Active Directory-Zertifikat Dienste|
|[-backupDB](#-backupdb)|Sichern der Active Directory-Zertifikat Dienst Datenbank|
|[-backupkey](#-backupkey)|Sichern der Active Directory Zertifikat Dienst Zertifikats und des privaten Schlüssels|
|[-Wiederherstellen](#-restore)|Active Directory Zertifikat Dienste wiederherstellen|
|[-restoreDB](#-restoredb)|Wiederherstellen der Active Directory-Zertifikat Dienst Datenbank|
|[-restorekey](#-restorekey)|Wiederherstellen des Zertifikats für die Active Directory Zertifikat Dienste und des privaten Schlüssels|
|[-importpfx](#-importpfx)|Importieren von Zertifikaten und privatem Schlüssel|
|[-dynamicfilelist](#-dynamicfilelist)|Dynamische Datei Liste anzeigen|
|[-databaselocations](#-databaselocations)|Daten Bank Speicherorte anzeigen|
|[-Hashdatei](#-hashfile)|Generieren und Anzeigen eines kryptografischen Hashs über eine Datei|
|[-Store](#-store)|Zertifikat Speicher sichern|
|[-addstore](#-addstore)|Hinzufügen eines Zertifikats zum Speicher|
|[-Delta Store](#-delstore)|Löschen eines Zertifikats aus dem Speicher|
|[-verifystore](#-verifystore)|Überprüfen eines Zertifikats im Speicher|
|[-repairren Store](#-repairstore)|Reparieren einer Schlüssel Zuordnung oder Aktualisieren der Zertifikat Eigenschaften oder der Schlüssel Sicherheits Beschreibung|
|[-Viewstore](#-viewstore)|Sichern des Zertifikat Speichers|
|[-viewdelta Store](#-viewdelstore)|Löschen eines Zertifikats aus dem Speicher|
|[-dspublish](#-dspublish)|Veröffentlichen eines Zertifikats oder einer Zertifikat Sperr Liste (CRL) zum Active Directory|
|[-Adtemplate](#-adtemplate)|Anzeigen von AD-Vorlagen|
|[-Vorlage](#-template)|Anzeigen von Zertifikat Vorlagen|
|[-Templatecas](#-templatecas)|Anzeigen der Zertifizierungsstellen (CAS) für eine Zertifikat Vorlage|
|[-| Emplates](#-catemplates)|Anzeigen von Vorlagen für die Zertifizierungsstelle|
|[-Setcasites](#-setcasites)|Verwalten von Website Namen für Zertifizierungsstellen|
|[-enrollmentServerURL](#-enrollmentserverurl)|Anzeigen, hinzufügen oder Löschen von mit einer Zertifizierungsstelle verknüpften Registrierungs Server-URLs|
|[-ADCA](#-adca)|Anzeigen von AD CAS|
|[-CA](#-ca)|Registrierungsrichtlinien-CAS anzeigen|
|[-Richtlinie](#-policy)|Registrierungs Richtlinie anzeigen|
|[-PolicyCache](#-policycache)|Registrierungsrichtlinien-Cache Einträge anzeigen oder löschen|
|[--Datenspeicher](#-credstore)|Anzeigen, hinzufügen oder Löschen von Anmelde Informationsspeicher Einträgen|
|[-Installdefaulttemplates](#-installdefaulttemplates)|Installieren von Standard Zertifikat Vorlagen|
|[-Urlcache](#-urlcache)|URL-Cache Einträge anzeigen oder löschen|
|[-Pulse](#-pulse)|Automatische Pulse-Registrierungs Ereignisse|
|[-Machineinfo](#-machineinfo)|Anzeigen von Informationen zum Active Directory Machine-Objekt|
|[-Dcinfo](#-dcinfo)|Anzeigen von Informationen zum Domänen Controller|
|[-Entinfo](#-entinfo)|Anzeigen von Informationen zu einer Unternehmens Zertifizierungsstelle|
|[-Tcainfo](#-tcainfo)|Anzeigen von Informationen zur Zertifizierungsstelle|
|[-Scinfo](#-scinfo)|Anzeigen von Informationen über die Smartcard|
|[-Scroots](#-scroots)|Verwalten von Smartcard-Stamm Zertifikaten|
|[-verifykeys](#-verifykeys)|Überprüfen eines öffentlichen oder privaten Schlüssel Satzes|
|[-Überprüfen](#-verify)|Überprüfen eines Zertifikats, einer Zertifikat Sperr Liste (CRL) oder einer Zertifikat Kette|
|[-verifyctl](#-verifyctl)|Überprüfen der CTL für AuthRoot oder unzulässige Zertifikate|
|[-Sign](#-sign)|Erneutes Signieren einer Zertifikat Sperr Liste (CRL) oder eines Zertifikats|
|[-vroot](#-vroot)|Erstellen oder Löschen von virtuellen Webstamm-und Dateifreigaben|
|[-vocsproot](#-vocsproot)|Erstellen oder Löschen von virtuellen webressourps für einen OCSP-WebProxy|
|[-addenrollmentserver](#-addenrollmentserver)|Hinzufügen einer Registrierungs Server Anwendung|
|[-deleteenrollmentserver](#-deleteenrollmentserver)|Löschen einer Registrierungs Server Anwendung|
|[-addpolicyserver](#-addpolicyserver)|Hinzufügen einer Richtlinien Server Anwendung|
|[-deletepolicyserver](#-deletepolicyserver)|Löschen einer Richtlinien Server Anwendung|
|[-OID](#-oid)|Anzeigen des Objekt Bezeichners oder Festlegen eines anzeigen Amens|
|[-Fehler](#-error)|Anzeigen des einem Fehlercode zugeordneten Meldungs Texts|
|[-getreg](#-getreg)|Anzeigen eines Registrierungs Werts|
|[-Eing](#-setreg)|Festlegen eines Registrierungs Werts|
|[-Delta reg](#-delreg)|Löschen eines Registrierungs Werts|
|[-Importkms](#-importkms)|Importieren von Benutzer Schlüsseln und Zertifikaten in die Server Datenbank für die Schlüssel Archivierung|
|[-Import CERT](#-importcert)|Importieren einer Zertifikatsdatei in die Datenbank|
|[-GetKey](#-getkey)|Abrufen eines archivierten BLOBs für die private Schlüsselwiederherstellung|
|[-Recoverkey](#-recoverkey)|Wiederherstellen eines archivierten privaten Schlüssels|
|[-MergePFX](#-mergepfx)|PFX-Dateien zusammenführen|
|[-Convertepf](#-convertepf)|Konvertieren einer PFX-Datei in eine EPF-Datei|
|-?|Zeigt die Liste der Verben an.|
|-Verb >-?  *\<*|Zeigt die Hilfe für das angegebene Verb an.|
|-? -v|Zeigt eine vollständige Liste der Verben und|

Zurück zum [Menü](#menu)

## <a name="syntax-notations"></a>Syntax Notationen

- Führen Sie für die grundlegende Befehlszeilen Syntax aus.`certutil -?`
- Führen Sie **certutil**  *\<-Verb >* **-?** aus, um die Syntax für die Verwendung von certutil mit einem bestimmten Verb zu verwenden.
- Um die gesamte certutil-Syntax in eine Textdatei zu senden, führen Sie die folgenden Befehle aus:  
  - `certutil -v -? > certutilhelp.txt`
  - `notepad certutilhelp.txt`

In der folgenden Tabelle wird die Notation beschrieben, mit der die Befehlszeilen Syntax angegeben wird.


|            Angabe             |                  Beschreibung                  |
|---------------------------------|-----------------------------------------------|
| Text ohne eckige Klammern oder geschweifte Klammern |         Elemente, die Sie eingeben müssen, wie gezeigt          |
|  \<Text in spitzen Klammern >  | Platzhalter, für den Sie einen Wert angeben müssen |
|  [Text in eckigen Klammern]  |                Optionale Elemente                 |
|      {Text in geschweiften Klammern}       |       Satz erforderlicher Elemente; Wählen Sie einen aus       |
|         Senkrechter Strich (          |                       )                       |
|          Auslassungspunkte (…)           |          Elemente, die wiederholt werden können           |

Zurück zum [Menü](#menu)

## <a name="-dump"></a>-Dump

Certutil [Optionen] [-Dump]

Certutil [Optionen] [-Dump] Datei

Konfigurationsinformationen oder Dateien sichern

[-f] [-silent] [-Split] [-p Kennwort] [-t Timeout]

Zurück zum [Menü](#menu)

## <a name="-asn"></a>-ASN

Certutil [Optionen]-ASN-Datei [Typ]

Analysieren der ASN. 1-Datei

Type: numeric Crypt\_Zeichen\_ \* folgen-decodetyp

Zurück zum [Menü](#menu)

## <a name="-decodehex"></a>-decodehex

Certutil [Optionen]-decodehex INFILE outfile [Type]

Type: numeric Crypt\_-\_ Zeichen\* folgen Codierungstyp

[-f]

Zurück zum [Menü](#menu)

## <a name="-decode"></a>-Decodieren

Certutil [Optionen]-Decodieren der Dateiausgabe Datei

Base64-codierte Datei decodieren

[-f]

Zurück zum [Menü](#menu)

## <a name="-encode"></a>-Codieren

Certutil [Optionen]-Codieren der Dateiausgabe Datei

Datei in Base64 codieren

[-f] [-UnicodeText]

Zurück zum [Menü](#menu)

## <a name="-deny"></a>-verweigern

Certutil [Optionen]-Deny RequestId

Ausstehende Anforderung ablehnen

[-config machine\caname]

Zurück zum [Menü](#menu)

## <a name="-resubmit"></a>-erneut übermitteln

Certutil [Optionen]-erneutes Senden von RequestId

Ausstehende Anforderung erneut übermitteln

[-config machine\caname]

Zurück zum [Menü](#menu)

## <a name="-setattributes"></a>-----Tributes

Certutil [Optionen]-SetAttributes RequestId AttributeString

Attribute für ausstehende Anforderung festlegen

RequestId--numerische Anforderungs-ID der ausstehenden Anforderung

AttributeString--Anforderungs Attribut Name-Wert-Paare

- Namen und Werte sind durch Doppelpunkte getrennt.
- Mehrere Name-Wert-Paare sind zeilenweise getrennt.
- Beispiel: "CertificateTemplate:User\nEMail:User@Domain.com"
- Jede "\n"-Sequenz wird in ein Zeilen Trennzeichen konvertiert.

[-config machine\caname]

Zurück zum [Menü](#menu)

## <a name="-setextension"></a>-abtextension

Certutil [Optionen]-setextension RequestId ExtensionName Flags {Long | Datum | Zeichenfolge | \@infile}

Erweiterung für ausstehende Anforderung festlegen

RequestId--numerische Anforderungs-ID einer ausstehenden Anforderung

ExtensionName--ObjectID String der Erweiterung

Flags--0 wird empfohlen.  1 macht die Erweiterung kritisch, 2 deaktiviert Sie, 3 führt beides aus.

Wenn der letzte Parameter numerisch ist, wird er als Long-Wert angenommen.

Wenn Sie als Datum analysiert werden kann, wird Sie als Datum angenommen.

Wenn Sie mit "\@" beginnt, ist der Rest des Tokens der Dateiname, der Binärdaten enthält, oder ein hexadezimal hexadezimal.

Alles andere wird als Zeichenfolge übernommen.

[-config machine\caname]

Zurück zum [Menü](#menu)

## <a name="-revoke"></a>-widerrufen

Certutil [Optionen]-widerrufen von "SerialNumber" [Reason]

Zertifikat widerrufen

SerialNumber Durch Trennzeichen getrennte Liste der zu wider rufenden Zertifikat Seriennummern

Grund: numerischer oder symbolischer Sperr Grund

- 0: CRL_REASON_UNSPECIFIED: Nicht angegeben (Standard)
- 1: CRL_REASON_KEY_COMPROMISE: Wichtiger Kompromiss
- 2: CRL_REASON_CA_COMPROMISE: Gefährdung der Zertifizierungsstelle
- 3: CRL_REASON_AFFILIATION_CHANGED: Zuordnung geändert
- 4\.30 CRL_REASON_SUPERSEDED: Abgelöst
- 17.25 CRL_REASON_CESSATION_OF_OPERATION: Beendigung des Vorgangs
- 18.40 CRL_REASON_CERTIFICATE_HOLD: Zertifikat Aufbewahrung
- 20.10 CRL_REASON_REMOVE_FROM_CRL: Aus CRL entfernen
- -1 Sperre Sperre

[-config machine\caname]

Zurück zum [Menü](#menu)

## <a name="-isvalid"></a>-IsValid

Certutil [Optionen]-IsValid serialNumber | CertHash

Aktuelle Zertifikat Disposition anzeigen

[-config machine\caname]

Zurück zum [Menü](#menu)

## <a name="-getconfig"></a>-GetConfig

Certutil [Optionen]-GetConfig

Standard Konfigurations Zeichenfolge erhalten

[-config machine\caname]

Zurück zum [Menü](#menu)

## <a name="-ping"></a>-Ping

Certutil [Optionen]-Ping [maxsecondstowait | Camachinelist]

Ping Active Directory-Anforderungs Schnittstelle für Zertifikat Dienste

Camachinelist: Liste der durch Trennzeichen getrennten Zertifizierungsstellen-Computernamen

1. Verwenden Sie für einen einzelnen Computer ein abschließendes Komma.
2. Zeigt die Standortkosten für die einzelnen Zertifizierungsstellen Computer an.

[-config machine\caname]

Zurück zum [Menü](#menu)

## <a name="-cainfo"></a>-Cainfo

Certutil [Optionen]-cainfo [Infoname [Index | ErrorCode]]

Anzeigen der Zertifizierungsstellen Informationen

Infoname: gibt die anzuzeigende ZS-Eigenschaft an (siehe unten). Verwenden Sie\*"" für alle Eigenschaften.

Index--optionaler NULL basierter Eigenschafts Index

ErrorCode--numerischer Fehlercode

[-f] [-Split] [-config machine\caname]

Syntax des Infoname-Arguments:

- Datei Dateiversion
- Product Produktversion
- exitcount: Anzahl der Beendigungs Module
- Exit [index]: Beschreibung des Beendigungs Moduls
- Policy Beschreibung des Richtlinien Moduls
- Benennen Zertifizierungsstellen Name
- bertizedname: Name der bereinigen Zertifizierungsstelle
- dsname Name der bereinigen Zertifizierungsstelle (DS-Name)
- Freigabe Ordner Frei gegebener Ordner
- Error1 errorCode: Fehlermeldungs Text
- error2 errorCode: Fehlermeldungs Text und Fehlercode
- Sorte Zertifizierungs Stellentyp
- Opo CA-Informationen
- übergeordneten Übergeordnete Zertifizierungsstelle
- certcount: Anzahl der Zertifizierungsstellen Zertifikate
- xchgcount: Zertifikat Anzahl für ca-Exchange
- kracount: Kra-CERT-Anzahl
- kraused: Anzahl verwendeter KRA-Zertifikate
- propidmax: Maximale Zertifizierungsstellen-PROPID
- certstate [index]: Zertifizierungsstellen Zertifikat
- certversion [index]: ZS-CERT-Version
- certstatus Code [index]: Zertifizierungsstellen-CERT-Status
- crlstate [index]: CRL
- krastate [index]: Kra-Zertifikat
- crossstate + [index]: Weiterleiten von Cross CERT
- crossstate-[index]: Abwärts Kreuz Zertifikat
- CERT [index]: Zertifizierungsstellen Zertifikat
- certchain [index]: Zertifizierungsstellen-Zertifikat Kette
- certcrlchain [index]: Zertifizierungsstellen-Zertifikat Kette mit CRLs
- xchg [index]: Zertifikat der Zertifizierungsstelle
- xchgchain [index]: Exchange-Zertifikat Kette der Zertifizierungsstelle
- xchgcrlchain [index]: CA Exchange-Zertifikat Kette mit CRLs
- Kra [index]: Kra-Zertifikat
- Cross + [index]: Weiterleiten von Cross CERT
- Cross-[index]: Abwärts Kreuz Zertifikat
- CRL [index]: Basis-CRL
- Delta [index]: Delta-CRL
- crlstatus [index]: Status der CRL-Veröffentlichung
- Delta-Status [index]: Veröffentlichungs Status der Delta-CRL
- DNS- DNS-Name
- spielen Rollentrennung
- Teams Advanced Server
- betrachtet Vorlagen
- CSP [index]: OCSP-URLs
- AIA [index]: AIA-URLs
- CDP [index]: CDP-URLs
- localename ZS-Gebiets Schema Name
- subjettemplateoids: Subjekt Vorlage OIDs

Zurück zum [Menü](#menu)

## <a name="-cacert"></a>-ca. cert

Certutil [Optionen]-ca. cert outcacertfile [index]

Abrufen des Zertifikats der Zertifizierungsstelle

Outcacertfile: Ausgabedatei

Sin Index für Zertifizierungsstellen-Zertifikat Erneuerung (Standardwert für den neuesten Wert)

[-f] [-Split] [-config machine\caname]

Zurück zum [Menü](#menu)

## <a name="-cachain"></a>-ca. Chain

Certutil [Optionen]-ca. Chain outcacertchainfile [index]

Abrufen der Zertifikat Kette der Zertifizierungsstelle

Outcacertchainfile: Ausgabedatei

Sin Index für Zertifizierungsstellen-Zertifikat Erneuerung (Standardwert für den neuesten Wert)

[-f] [-Split] [-config machine\caname]

Zurück zum [Menü](#menu)

## <a name="-getcrl"></a>-Getcrl

Certutil [Optionen]-getcrl outfile [index] [Delta]

CRL erhalten

Sin CRL-Index oder Schlüssel Index (Standardwert ist CRL für den neuesten Schlüssel)

Delta: Delta-CRL (Standardwert ist Basis-CRL)

[-f] [-Split] [-config machine\caname]

Zurück zum [Menü](#menu)

## <a name="-crl"></a>-CRL

Certutil [Optionen]-CRL [DD: hh | erneut veröffentlichen] [Delta]

Neue CRLs veröffentlichen [oder nur Delta-CRLs]

DD: hh--neue Gültigkeitsdauer der Zertifikat Sperr Liste in Tagen und Stunden

erneut veröffentlichen--letzte CRLs erneut veröffentlichen

Delta--Delta-CRLs (Standardwert: Basis-und Delta-CRLs)

[-Split] [-config machine\caname]

Zurück zum [Menü](#menu)

## <a name="-shutdown"></a>-Herunterfahren

Certutil [Optionen]-Herunterfahren

Herunterfahren Active Directory Zertifikat Dienste

[-config machine\caname]

Zurück zum [Menü](#menu)

## <a name="-installcert"></a>-installCert

Certutil [Optionen]-installCert [CACertFile]

Zertifizierungsstellen Zertifikat installieren

[-f] [-silent] [-config machine\caname]

Zurück zum [Menü](#menu)

## <a name="-renewcert"></a>-verläncert

Certutil [Optionen]-erneuercert [reusekeys] [machine\parametricaname]

Zertifizierungsstellen Zertifikat erneuern

Verwenden Sie-f, um eine ausstehende Erneuerungs Anforderung zu ignorieren und eine neue Anforderung zu generieren.

[-f] [-silent] [-config machine\caname]

Zurück zum [Menü](#menu)

## <a name="-schema"></a>-Schema

Certutil [Optionen]-Schema [ext | Attrb | CRL

Zertifikat Schema sichern

Standardmäßig Anforderungs-und Zertifikat Tabelle

Antrags Erweiterungs Tabelle

Attrib Attribut Tabelle

CRL CRL-Tabelle

[-Split] [-config machine\caname]

Zurück zum [Menü](#menu)

## <a name="-view"></a>-Ansicht

Certutil [Optionen]-Ansicht [Warteschlange | Protokoll | Logfail | Widerrufen | Ext | Attrb | CRL] [csv]

Zertifikat Ansicht sichern

Warteschlange: Anforderungs Warteschlange

Protokoll: Ausgestellte oder widerrufene Zertifikate sowie fehlerhafte Anforderungen

Logfail: Fehlerhafte Anforderungen

Aufzuheben Widerrufene Zertifikate

Antrags Erweiterungs Tabelle

Attrib Attribut Tabelle

CRL CRL-Tabelle

CSV Ausgabe als durch Trennzeichen getrennte Werte

So zeigen Sie die Spalte "Statuscode" für alle Einträge an:-Out Statuscode

So zeigen Sie alle Spalten für den letzten Eintrag an: beschränken Sie "RequestId = = $"

So zeigen Sie RequestId und Disposition für drei Anforderungen an: beschränken Sie "RequestId > = 37, RequestId\<40"-out "RequestId, Disposition"

So zeigen Sie Zeilen-IDs und CRL-Nummern für alle Basis-CRLs an:-einschränken "crlminbase = 0"-out "crlrowid, CRLNumber" CRL

Zum Anzeigen der CRL-Nummer 3:-v-Limit "crlminbase = 0, CRLNumber = 3"-out "crlrawcrl" CRL

So zeigen Sie die gesamte CRL-Tabelle an: CRL

Verwenden Sie "Date [+ |-DD: hh]" für Datums Einschränkungen.

"Now + DD: hh" für ein Datum in Bezug auf die aktuelle Uhrzeit verwenden

[-silent] [-Split] [-config machine\caname] [-RestrictionList einschränken] [-out ColumnList]

Zurück zum [Menü](#menu)

## <a name="-db"></a>-DB

Certutil [Optionen]-DB

Rohdatenbankdump sichern

[-config machine\caname] [-RestrictionList einschränken] [-out ColumnList]

Zurück zum [Menü](#menu)

## <a name="-deleterow"></a>-deleteRow

Certutil [Optionen]-deleteRow ROWID | Datum [Anforderung | CERT | Ext | Attrb | CRL

Zeile der Server Datenbank löschen

Anforderung Fehlgeschlagene und ausstehende Anforderungen (Übermittlungs Datum)

Cert: Abgelaufene und widerrufene Zertifikate (Ablaufdatum)

Antrags Erweiterungs Tabelle

Attrib Attribut Tabelle

CRL CRL-Tabelle (Ablaufdatum)

Zum Löschen von fehlgeschlagenen und ausstehenden Anforderungen, die vom 22. Januar 2001 gesendet wurden: 1/22/2001-Anforderung

So löschen Sie alle Zertifikate, die bis zum 22. Januar 2001 abgelaufen sind: 1/22/2001-Zertifikat

So löschen Sie die Zertifikats Zeile, Attribute und Erweiterungen für RequestId 37: 37

So löschen Sie CRLs, die bis zum 22. Januar 2001 abgelaufen sind: 1/22/2001 CRL

[-f] [-config machine\caname]

Zurück zum [Menü](#menu)

## <a name="-backup"></a>-Sicherung

Certutil [Optionen]-Backup BackupDirectory [inkrementell] [keeplog]

Backup Active Directory-Zertifikat Dienste

BackupDirectory: Verzeichnis zum Speichern der gesicherten Daten

Inkrementell: nur inkrementelle Sicherung

Keeplog: Daten Bank Protokolldateien beibehalten (Standardeinstellung ist das Abschneiden von Protokolldateien)

[-f] [-config machine\caname] [-p Kennwort]

Zurück zum [Menü](#menu)

## <a name="-backupdb"></a>-backupDB

Certutil [Optionen]-backupDB-BackupDirectory [inkrementell] [keeplog]

Datenbank für Sicherungs Active Directory Zertifikat Dienste

BackupDirectory: Verzeichnis zum Speichern der gesicherten Datenbankdateien

Inkrementell: nur inkrementelle Sicherung

Keeplog: Daten Bank Protokolldateien beibehalten (Standardeinstellung ist das Abschneiden von Protokolldateien)

[-f] [-config machine\caname]

Zurück zum [Menü](#menu)

## <a name="-backupkey"></a>-backupkey

Certutil [Optionen]-backupkey BackupDirectory

Zertifikat Dienst Zertifikat für Sicherung Active Directory und privater Schlüssel

BackupDirectory: Verzeichnis zum Speichern der gesicherten PFX-Datei

[-f] [-config machine\caname] [-p Kennwort] [-t Timeout]

Zurück zum [Menü](#menu)

## <a name="-restore"></a>-Wiederherstellen

Certutil [Optionen]-Restore BackupDirectory

Active Directory Zertifikat Dienste wiederherstellen

BackupDirectory: Verzeichnis mit wiederherzustellenden Daten

[-f] [-config machine\caname] [-p Kennwort]

Zurück zum [Menü](#menu)

## <a name="-restoredb"></a>-restoreDB

Certutil [Optionen]-restoreDB BackupDirectory

Datenbank für Active Directory Zertifikat Dienste wiederherstellen

BackupDirectory: Verzeichnis mit wiederherzustellenden Datenbankdateien

[-f] [-config machine\caname]

Zurück zum [Menü](#menu)

## <a name="-restorekey"></a>-restorekey

Certutil [Optionen]-restorekey BackupDirectory | Pfxfile

Wiederherstellen Active Directory Zertifikat Dienst Zertifikats und des privaten Schlüssels

BackupDirectory: Verzeichnis mit PFX-Datei, die wieder hergestellt werden soll

Pfxfile: PFX-Datei, die wieder hergestellt werden soll

[-f] [-config machine\caname] [-p Kennwort]

Zurück zum [Menü](#menu)

## <a name="-importpfx"></a>-importpfx

Certutil [Optionen]-importpfx [certifikatestorename] pfxfile [Modifier]

Importieren von Zertifikaten und privatem Schlüssel

Certifikatestorename: Der Zertifikat Speicher Name.  Siehe [-Store](#-store).

Pfxfile: Zu importierende PFX-Datei

Modifizierer Durch Trennzeichen getrennte Liste mit einem oder mehreren der folgenden:

1. AT_SIGNATURE: KeySpec in Signatur ändern
2. AT_KEYEXCHANGE: Ändern von KeySpec in Key Exchange
3. Noexport: Festlegen, dass der private Schlüssel nicht exportierbar ist
4. Nocert: Importieren Sie das Zertifikat nicht.
5. Nochain: Importieren Sie die Zertifikat Kette nicht.
6. Noroot: Importieren Sie das Stamm Zertifikat nicht.
7. Schützen Schlüssel durch Kennwort schützen
8. Noprotect: Schlüssel nicht Kenn Wort Schutz

Der Standardwert ist der persönliche Computerspeicher.

[-f] [-user] [-p Kennwort] [-CSP-Anbieter]

Zurück zum [Menü](#menu)

## <a name="-dynamicfilelist"></a>-dynamicfilelist

Certutil [Optionen]-dynamicfilelist

Dynamische Datei Liste anzeigen

[-config machine\caname]

Zurück zum [Menü](#menu)

## <a name="-databaselocations"></a>-databaselocations

Certutil [Optionen]-databaselocations

Daten Bank Speicherorte anzeigen

[-config machine\caname]

Zurück zum [Menü](#menu)

## <a name="-hashfile"></a>-Hashdatei

Certutil [Optionen]-Hashdatei-Eingabedatei [HashAlgorithm]

Generieren und Anzeigen von kryptografiehash über eine Datei

Zurück zum [Menü](#menu)

## <a name="-store"></a>-Store

Certutil [Optionen]-Store [certifikatestorename [CertID [OutputFile]]]

Zertifikat Speicher sichern

Certifikatestorename: Der Zertifikat Speicher Name. Beispiele:

- "My", "ca" (Standard), "root",
- "LDAP:///CN=Certification Autoritäten, CN = Public Key Services, CN = Services, CN = Configuration, DC = CPANDL, DC = com? cACertificate? One? objectClass = CertificationAuthority" (Stamm Zertifikate anzeigen)
- "LDAP:///CN=CAName,CN=Certification Authority, CN = Public Key Services, CN = Services, CN = Configuration, DC = CPANDL, DC = com? cACertificate? Base? objectClass = CertificationAuthority" (Modify Root-Zertifikate)
- "LDAP:///CN=CAName,CN=MachineName,CN=CDP,CN=Public Key Services, CN = Services, CN = Configuration, DC = CPANDL, DC = com? CertificateRevocationList? Base? objectClass = CRLDistributionPoint" (CRLs anzeigen)
- "LDAP:///CN=NTAuthCertificates,CN=Public Key Services, CN = Services, CN = Configuration, DC = CPANDL, DC = com? cACertificate? Base? objectClass = CertificationAuthority" (Unternehmens Zertifizierungsstellen-Zertifikate)
- standardi (AD-Computer Objekt Zertifikate)
- -Benutzer-LDAP: (AD-Benutzerobjekt Zertifikate)

CertId Das Zertifikat oder CRL-Übereinstimmungs Token.  Hierbei kann es sich um eine Seriennummer, ein SHA-1-Zertifikat, eine CRL, einen CTL-oder einen öffentlichen Schlüssel Hash, einen numerischen Zertifikat Index (0, 1 usw.), einen numerischen CRL-Index (0, 1 usw.), einen numerischen CTL-Index (.. 0,.. 1 usw.), einen öffentlichen Schlüssel, eine Signatur oder eine Erweiterungs Objekt-ID, einen allgemeinen Namen für den Zertifikat Antragsteller, eine e-Mail-Adresse, einen UPN-oder DNS-Namen, einen Schlüssel Container Namen oder einen CSP-Namen, einen Vorlagen Namen oder eine ObjectID, eine EKU-oder Anwendungsrichtlinien-ObjectID oder einen allgemeinen CRL-Aussteller Viele davon können zu mehreren Übereinstimmungen führen.

OutputFile: Datei zum Speichern eines übereinstimmenden Zertifikats

Verwenden Sie-User, um auf einen Benutzerspeicher anstelle eines Computerspeicher zuzugreifen.

Verwenden Sie-Enterprise, um auf einen Computer im Enterprise Store zuzugreifen

Verwenden Sie-Service, um auf einen Computerdienst Speicher zuzugreifen.

Verwenden Sie-GroupPolicy, um auf einen Computer Gruppenrichtlinien Speicher zuzugreifen.

Beispiele:

- -Enterprise NTAuth
- -Enterprise root 37
- -Benutzer My 26e0aaaf000000000004
- CA. 11

[-f] [-Enterprise] [-user] [-GroupPolicy] [-silent] [-Split] [-DC DCNAME]

Zurück zum [Menü](#menu)

## <a name="-addstore"></a>-addstore

Certutil [Optionen]-addstore certifikatestorename INFILE

Zertifikat zum Speicher hinzufügen

Certifikatestorename: Der Zertifikat Speicher Name.  Siehe [-Store](#-store).

Eingabedatei Zertifikat oder CRL-Datei, die dem Speicher hinzugefügt werden soll.

[-f] [-Enterprise] [-user] [-GroupPolicy] [-DC DCNAME]

Zurück zum [Menü](#menu)

## <a name="-delstore"></a>-Delta Store

Certutil [Optionen]-Delta Zertifikat certifikatestorename CertID

Zertifikat aus dem Speicher löschen

Certifikatestorename: Der Zertifikat Speicher Name.  Siehe [-Store](#-store).

CertId Das Zertifikat oder CRL-Übereinstimmungs Token.  Siehe [-Store](#-store).

[-Enterprise] [-user] [-GroupPolicy] [-DC DCNAME]

Zurück zum [Menü](#menu)

## <a name="-verifystore"></a>-verifystore

Certutil [Optionen]-verifystore certifikatestorename [CertID]

Zertifikat im Speicher überprüfen

Certifikatestorename: Der Zertifikat Speicher Name.  Siehe [-Store](#-store).

CertId Das Zertifikat oder CRL-Übereinstimmungs Token.  Siehe [-Store](#-store).

[-Enterprise] [-user] [-GroupPolicy] [-silent] [-Split] [-DC DCNAME] [-t Timeout]

Zurück zum [Menü](#menu)

## <a name="-repairstore"></a>-repairren Store

Certutil [Optionen]-repaunstore certifikatestorename certidlist [propertyinffile | Sddlsecuritydescriptor]

Reparieren der Schlüssel Zuordnung oder Aktualisieren der Zertifikat Eigenschaften oder der Schlüssel Sicherheits Beschreibung

Certifikatestorename: Der Zertifikat Speicher Name.  Siehe [-Store](#-store).

Certidlist: durch Trennzeichen getrennte Liste von Zertifikat-oder CRL-abgleichstoken. Siehe [-Store](#-store) CertID Description.

Propertyinffile--INF-Datei mit externen Eigenschaften:

```
[Properties]
     19 = Empty ; Add archived property, OR:
     19 =       ; Remove archived property

     11 = "{text}Friendly Name" ; Add friendly name property

     127 = "{hex}" ; Add custom hexadecimal property
         _continue_ = "00 01 02 03 04 05 06 07 08 09 0a 0b 0c 0d 0e 0f"
         _continue_ = "10 11 12 13 14 15 16 17 18 19 1a 1b 1c 1d 1e 1f"

     2 = "{text}" ; Add Key Provider Information property
       _continue_ = "Container=Container Name&"
       _continue_ = "Provider=Microsoft Strong Cryptographic Provider&"
       _continue_ = "ProviderType=1&"
       _continue_ = "Flags=0&"
       _continue_ = "KeySpec=2"

     9 = "{text}" ; Add Enhanced Key Usage property
       _continue_ = "1.3.6.1.5.5.7.3.2,"
       _continue_ = "1.3.6.1.5.5.7.3.1,"
```

[-f] [-Enterprise] [-user] [-GroupPolicy] [-silent] [-Split] [-CSP-Anbieter]

Zurück zum [Menü](#menu)

## <a name="-viewstore"></a>-Viewstore

Certutil [Optionen]-Viewstore [certifikatestorename [CertID [OutputFile]]]

Zertifikat Speicher sichern

Certifikatestorename: Der Zertifikat Speicher Name. Beispiele:

- "My", "ca" (Standard), "root",
- "LDAP:///CN=Certification Autoritäten, CN = Public Key Services, CN = Services, CN = Configuration, DC = CPANDL, DC = com? cACertificate? One? objectClass = CertificationAuthority" (Stamm Zertifikate anzeigen)
- "LDAP:///CN=CAName,CN=Certification Authority, CN = Public Key Services, CN = Services, CN = Configuration, DC = CPANDL, DC = com? cACertificate? Base? objectClass = CertificationAuthority" (Modify Root-Zertifikate)
- "LDAP:///CN=CAName,CN=MachineName,CN=CDP,CN=Public Key Services, CN = Services, CN = Configuration, DC = CPANDL, DC = com? CertificateRevocationList? Base? objectClass = CRLDistributionPoint" (CRLs anzeigen)
- "LDAP:///CN=NTAuthCertificates,CN=Public Key Services, CN = Services, CN = Configuration, DC = CPANDL, DC = com? cACertificate? Base? objectClass = CertificationAuthority" (Unternehmens Zertifizierungsstellen-Zertifikate)
- standardi (AD-Computer Objekt Zertifikate)
- -Benutzer-LDAP: (AD-Benutzerobjekt Zertifikate)

CertId Das Zertifikat oder CRL-Übereinstimmungs Token. Hierbei kann es sich um eine Seriennummer, ein SHA-1-Zertifikat, eine CRL, einen CTL-oder einen öffentlichen Schlüssel Hash, einen numerischen Zertifikat Index (0, 1 usw.), einen numerischen CRL-Index (0, 1 usw.), einen numerischen CTL-Index (.. 0,.. 1 usw.), einen öffentlichen Schlüssel, eine Signatur oder eine Erweiterungs Objekt-ID, einen allgemeinen Namen für den Zertifikat Antragsteller, eine e-Mail-Adresse, einen UPN-oder DNS-Namen, einen Schlüssel Container Namen oder einen CSP-Namen, einen Vorlagen Namen oder eine ObjectID, eine EKU-oder Anwendungsrichtlinien-ObjectID oder einen allgemeinen CRL-Aussteller Viele davon können zu mehreren Übereinstimmungen führen.

OutputFile: Datei zum Speichern eines übereinstimmenden Zertifikats

Verwenden Sie-User, um auf einen Benutzerspeicher anstelle eines Computerspeicher zuzugreifen.

Verwenden Sie-Enterprise, um auf einen Computer im Enterprise Store zuzugreifen

Verwenden Sie-Service, um auf einen Computerdienst Speicher zuzugreifen.

Verwenden Sie-GroupPolicy, um auf einen Computer Gruppenrichtlinien Speicher zuzugreifen.

Beispiele:

1. -Enterprise NTAuth
2. -Enterprise root 37
3. -Benutzer My 26e0aaaf000000000004
4. CA. 11

[-f] [-Enterprise] [-user] [-GroupPolicy] [-DC DCNAME]

Zurück zum [Menü](#menu)

## <a name="-viewdelstore"></a>-viewdelta Store

Certutil [Optionen]-viewdelta Store [certifikatestorename [CertID [OutputFile]]]

Zertifikat aus dem Speicher löschen

Certifikatestorename: Der Zertifikat Speicher Name. Beispiele:

- "My", "ca" (Standard), "root",
- "LDAP:///CN=Certification Autoritäten, CN = Public Key Services, CN = Services, CN = Configuration, DC = CPANDL, DC = com? cACertificate? One? objectClass = CertificationAuthority" (Stamm Zertifikate anzeigen)
- "LDAP:///CN=CAName,CN=Certification Authority, CN = Public Key Services, CN = Services, CN = Configuration, DC = CPANDL, DC = com? cACertificate? Base? objectClass = CertificationAuthority" (Modify Root-Zertifikate)
- "LDAP:///CN=CAName,CN=MachineName,CN=CDP,CN=Public Key Services, CN = Services, CN = Configuration, DC = CPANDL, DC = com? CertificateRevocationList? Base? objectClass = CRLDistributionPoint" (CRLs anzeigen)
- "LDAP:///CN=NTAuthCertificates,CN=Public Key Services, CN = Services, CN = Configuration, DC = CPANDL, DC = com? cACertificate? Base? objectClass = CertificationAuthority" (Unternehmens Zertifizierungsstellen-Zertifikate)
- standardi (AD-Computer Objekt Zertifikate)
- -Benutzer-LDAP: (AD-Benutzerobjekt Zertifikate)

CertId Das Zertifikat oder CRL-Übereinstimmungs Token. Hierbei kann es sich um eine Seriennummer, ein SHA-1-Zertifikat, eine CRL, einen CTL-oder einen öffentlichen Schlüssel Hash, einen numerischen Zertifikat Index (0, 1 usw.), einen numerischen CRL-Index (0, 1 usw.), einen numerischen CTL-Index (.. 0,.. 1 usw.), einen öffentlichen Schlüssel, eine Signatur oder eine Erweiterungs Objekt-ID, einen allgemeinen Namen für den Zertifikat Antragsteller, eine e-Mail-Adresse, einen UPN-oder DNS-Namen, einen Schlüssel Container Namen oder einen CSP-Namen, einen Vorlagen Namen oder eine ObjectID, eine EKU-oder Anwendungsrichtlinien-ObjectID oder einen allgemeinen CRL-Aussteller Viele davon können zu mehreren Übereinstimmungen führen.

OutputFile: Datei zum Speichern eines übereinstimmenden Zertifikats

Verwenden Sie-User, um auf einen Benutzerspeicher anstelle eines Computerspeicher zuzugreifen.

Verwenden Sie-Enterprise, um auf einen Computer im Enterprise Store zuzugreifen

Verwenden Sie-Service, um auf einen Computerdienst Speicher zuzugreifen.

Verwenden Sie-GroupPolicy, um auf einen Computer Gruppenrichtlinien Speicher zuzugreifen.

Beispiele:

1. -Enterprise NTAuth
2. -Enterprise root 37
3. -Benutzer My 26e0aaaf000000000004
4. CA. 11

[-f] [-Enterprise] [-user] [-GroupPolicy] [-DC DCNAME]

Zurück zum [Menü](#menu)

## <a name="-dspublish"></a>-dspublish

Certutil [Optionen]-dspublish CertFile [ntauthca | Rootca | Subca | Crossca | Kra | Benutzer | Computer

Certutil [Optionen]-dspublish crlfile [dscdpcontainer [dscdpcn]]

Zertifikat oder CRL zum Active Directory veröffentlichen

CertFile: zu veröffentlichende Zertifikatsdatei

Ntauthca: Zertifikat in DS Enterprise Store veröffentlichen

RootCA Zertifikat in DS vertrauenswürdigem Stamm Speicher veröffentlichen

SubCA Zertifizierungsstellen Zertifikat in DS-ca-Objekt veröffentlichen

Crossca: Kreuz Zertifikat in DS-ca-Objekt veröffentlichen

KRA Zertifikat in DS-Schlüsselwiederherstellungs-Agentobjekt veröffentlichen

Benutzer: Zertifikat für Benutzer-DS-Objekt veröffentlichen

Computer Zertifikat auf Computer-DS-Objekt veröffentlichen

Crldatei Zu veröffentlichende CRL-Datei

Dscdpcontainer: DS CDP Container CN, normalerweise der Name der Zertifizierungsstellen Maschine

DSCDPCN: DS-CDP-Objekt CN, normalerweise basierend auf dem Kurznamen und Schlüssel Index der bereinigen Zertifizierungsstelle

Verwenden Sie-f zum Erstellen eines DS-Objekts.

[-f] [-user] [-DC DCNAME]

Zurück zum [Menü](#menu)

## <a name="-adtemplate"></a>-Adtemplate

Certutil [Optionen]-adtemplate [Vorlage]

Anzeigen von AD-Vorlagen

[-f] [-user] [-ut] [-MT] [-DC DCNAME]

## <a name="-template"></a>-Vorlage

Certutil [Optionen]-Vorlage [Vorlage]

Anzeigen von Registrierungsrichtlinien Vorlagen

[-f] [-user] [-silent] [-Policyserver urlorid] [-Anonymous] [-Kerberos] [-ClientCertificate clientcertid] [-Username username] [-p Kennwort]

Zurück zum [Menü](#menu)

## <a name="-templatecas"></a>-Templatecas

Certutil [Optionen]-Vorlage "templatecas"

CAS für Vorlage anzeigen

[-f] [-user] [-DC DCNAME]

Zurück zum [Menü](#menu)

## <a name="-catemplates"></a>-| Emplates

Certutil [Optionen]-| emplates [Vorlage]

Anzeigen von Vorlagen für die Zertifizierungsstelle

[-f] [-user] [-ut] [-MT] [-config machine\caname] [-DC DCNAME]

Zurück zum [Menü](#menu)

## <a name="-setcasites"></a>-Setcasites

Certutil [Optionen]-setcasites [Set] [SiteName]

Certutil [Optionen]-setcasites-Überprüfung [SiteName]

Certutil [Optionen]-setcasites löschen

Festlegen, überprüfen oder Löschen von Zertifizierungsstellen-Standortnamen

- Verwenden Sie die Option "-config", um eine einzelne Zertifizierungsstelle als Ziel zu verwenden
- *Sitename* ist nur zulässig, wenn eine einzelne Zertifizierungsstelle als Ziel verwendet wird
- Verwenden Sie-f, um Validierungs Fehler für den angegebenen *Sitename* zu überschreiben.
- Verwenden Sie-f, um alle ZS-Standortnamen zu löschen.

[-f] [-config machine\caname] [-DC DCNAME]

> [!NOTE]
> Weitere Informationen zum Konfigurieren von CAS für Active Directory Domain Services (AD DS) Standortinformationen finden Sie unter [AD DS Site Awareness for AD CS and PKI Clients](https://social.technet.microsoft.com/wiki/contents/articles/14106.ad-ds-site-awareness-for-ad-cs-and-pki-clients.aspx).

Zurück zum [Menü](#menu)

## <a name="-enrollmentserverurl"></a>-enrollmentServerURL

Certutil [Optionen]-enrollmentServerURL [URL AuthenticationType [Priority] [Modifier]]

Certutil [Optionen]-enrollmentServerURL URL DELETE

Anzeigen, hinzufügen oder Löschen von mit einer Zertifizierungsstelle verknüpften Registrierungs Server-URLs

AuthenticationType Geben Sie beim Hinzufügen einer URL eine der folgenden Client Authentifizierungsmethoden an.

1. Kerberos Kerberos-SSL-Anmelde Informationen verwenden
2. User Benanntes Konto für SSL-Anmelde Informationen verwenden
3. ClientCertificate SSL-Anmelde Informationen für X. 509-Zertifikate verwenden
4. Anonymous: Anonyme SSL-Anmelde Informationen verwenden

Löschen: Löscht die angegebene URL, die der Zertifizierungsstelle zugeordnet ist.

Priorität: Standardwert ist "1", wenn dieser beim Hinzufügen einer URL nicht angegeben wird.

Modifiziererer: durch Trennzeichen getrennte Liste mit einem oder mehreren der folgenden Werte:

1. Allowrenewalsonly: Nur Erneuerungs Anforderungen können über diese URL an diese Zertifizierungsstelle übermittelt werden.
2. Allowkeybasedrenewal: Ermöglicht die Verwendung eines Zertifikats, das über kein zugeordnetes Konto in der AD-Verbindung verfügt. Dies gilt nur für den Modus "ClientCertificate" und "allowrenewalsonly".

[-config machine\caname] [-DC DCNAME]

Zurück zum [Menü](#menu)

## <a name="-adca"></a>-ADCA

Certutil [Optionen]-ADCA [CAName]

Anzeigen von AD CAS

[-f] [-Split] [-DC DCNAME]

Zurück zum [Menü](#menu)

## <a name="-ca"></a>-CA

Certutil [Optionen]-ca [CAName | TemplateName

Registrierungsrichtlinien-CAS anzeigen

[-f] [-user] [-silent] [-Split] [-Policyserver urlorid] [-Anonymous] [-Kerberos] [-ClientCertificate clientcertid] [-Username username] [-p Kennwort]

Zurück zum [Menü](#menu)

## <a name="-policy"></a>-Richtlinie

Registrierungs Richtlinie anzeigen

[-f] [-user] [-silent] [-Split] [-Policyserver urlorid] [-Anonymous] [-Kerberos] [-ClientCertificate clientcertid] [-Username username] [-p Kennwort]

Zurück zum [Menü](#menu)

## <a name="-policycache"></a>-PolicyCache

Certutil [Optionen]-PolicyCache [löschen]

Registrierungsrichtlinien-Cache Einträge anzeigen oder löschen

DELETE: Richtlinien Server-Cache Einträge löschen

-f: Verwenden Sie-f, um alle Cache Einträge zu löschen.

[-f] [-user] [-Policyserver urlorid]

Zurück zum [Menü](#menu)

## <a name="-credstore"></a>--Datenspeicher

Certutil [Optionen]-Datenspeicher [URL]

Certutil [Optionen]-buildspeicher-URL hinzufügen

Certutil [Optionen]-URL zum Löschen des buildstores

Anzeigen, hinzufügen oder Löschen von Anmelde Informationsspeicher Einträgen

URL: die Ziel-URL.  Verwenden \* Sie, um alle Einträge abzugleichen. Verwenden https://machine\ Sie *, um ein URL-Präfix zuzuordnen.

hinzufügen: Fügen Sie einen Anmelde Informationsspeicher Eintrag hinzu. SSL-Anmelde Informationen müssen ebenfalls angegeben werden.

DELETE: Anmelde Informationsspeicher-Einträge löschen

-f: Verwenden Sie-f, um einen Eintrag zu überschreiben oder mehrere Einträge zu löschen.

[-f] [-user] [-silent] [-Anonymous] [-Kerberos] [-ClientCertificate clientcertid] [-Username username] [-p Kennwort]

Zurück zum [Menü](#menu)

## <a name="-installdefaulttemplates"></a>-Installdefaulttemplates

Certutil [Optionen]-installdefaulttemplates

Installieren von Standard Zertifikat Vorlagen

[-DC DCNAME]

Zurück zum [Menü](#menu)

## <a name="-urlcache"></a>-Urlcache

Certutil [Optionen]-Urlcache [URL | CRL | \* [löschen]]

URL-Cache Einträge anzeigen oder löschen

URL: zwischengespeicherte URL

CRL: nur für alle zwischengespeicherten CRL-URLs ausführen

\*: Arbeiten mit allen zwischengespeicherten URLs

DELETE: relevante URLs aus dem lokalen Cache des aktuellen Benutzers löschen

Verwenden Sie-f, um das Abrufen einer bestimmten URL und das Aktualisieren des Caches zu erzwingen.

[-f] [-Split]

Zurück zum [Menü](#menu)

## <a name="-pulse"></a>-Pulse

Certutil [Optionen]-Pulse

Ereignisse für automatische Pulse-Registrierung

[-user]

Zurück zum [Menü](#menu)

## <a name="-machineinfo"></a>-Machineinfo

Certutil [Optionen]-machineinfo DomainName\MachineName $

Anzeigen Active Directory Computer Objektinformationen

Zurück zum [Menü](#menu)

## <a name="-dcinfo"></a>-Dcinfo

Certutil [Optionen]-dcinfo [Domäne] [überprüfen | Deletebad | DeleteAll

Anzeigen von Domänen Controller Informationen

Standardmäßig werden Domänen Controller ohne Überprüfung angezeigt.

[-f] [-user] [-urlfetch] [-DC DCNAME] [-t Timeout]

> [!TIP]
> Die Möglichkeit, eine Active Directory Domain Services (AD DS)-Domäne **[Domäne]** anzugeben und einen Domänen Controller ( **-DC**) anzugeben, wurde in Windows Server 2012 hinzugefügt. Um den Befehl erfolgreich auszuführen, müssen Sie ein Konto verwenden, das Mitglied der Gruppe " **Domänen-Admins** " oder "Organisations- **Admins**" ist. Die Verhaltensänderungen dieses Befehls lauten wie folgt:</br>> 1.  Wenn keine Domäne angegeben ist und kein bestimmter Domänen Controller angegeben ist, wird mit dieser Option eine Liste von Domänen Controllern zurückgegeben, die vom Standard Domänen Controller verarbeitet werden sollen.</br>> 2.  Wenn keine Domäne angegeben ist, aber ein Domänen Controller angegeben ist, wird ein Bericht der Zertifikate auf dem angegebenen Domänen Controller generiert.</br>> 3.  Wenn eine Domäne angegeben ist, jedoch kein Domänen Controller angegeben ist, wird eine Liste mit Domänen Controllern zusammen mit Berichten zu den Zertifikaten für die einzelnen Domänen Controller in der Liste generiert.</br>> 4.  Wenn die Domäne und der Domänen Controller angegeben sind, wird eine Liste der Domänen Controller vom Zieldomänen Controller generiert. Ein Bericht der Zertifikate für jeden Domänen Controller in der Liste wird ebenfalls generiert.

Nehmen wir beispielsweise an, dass eine Domäne mit dem Namen CPANDL mit einem Domänen Controller namens CPANDL-DC1 vorhanden ist. Sie können den folgenden Befehl ausführen, um eine Liste von Domänen Controllern und deren Zertifikaten aus CPANDL-DC1: certutil-DC CPANDL-DC1-dcinfo CPANDL abzurufen.

Zurück zum [Menü](#menu)

## <a name="-entinfo"></a>-Entinfo

Certutil [Optionen]-entinfo DomainName\MachineName $

[-f] [-user]

Zurück zum [Menü](#menu)

## <a name="-tcainfo"></a>-Tcainfo

Certutil [Optionen]-tcainfo [domaindn |-]

Anzeigen der Zertifizierungsstellen Informationen

[-f] [-Enterprise] [-user] [-urlfetch] [-DC DCNAME] [-t Timeout]

Zurück zum [Menü](#menu)

## <a name="-scinfo"></a>-Scinfo

Certutil [Optionen]-scinfo [readername [CRYPT_DELETEKEYSET]]

Smartcardinformationen anzeigen

CRYPT_DELETEKEYSET: Alle Schlüssel auf der Smartcard löschen

[-silent] [-Split] [-urlfetch] [-t Timeout]

Zurück zum [Menü](#menu)

## <a name="-scroots"></a>-Scroots

Certutil [Optionen]-scrootupdate [+] [inputrootfile] [readername]

Certutil [Optionen]-scrootspeichern \@outputrootfile [readername]

Certutil [Optionen]-scroots-Sicht [inputrootfile | Readername]

Certutil [Optionen]-scroots delete [readername]

Verwalten von Smartcard-Stamm Zertifikaten

[-f] [-Split] [-p Kennwort]

Zurück zum [Menü](#menu)

## <a name="-verifykeys"></a>-verifykeys

Certutil [Optionen]-verifykeys [KeyContainerName CACertFile]

Öffentlichen/privaten Schlüsselsatz überprüfen

KeyContainerName: Schlüssel Container Name des zu überprüfenden Schlüssels. Standardmäßig werden die Computer Schlüssel verwendet.  Verwenden Sie-User für Benutzerschlüssel.

CACertFile: Signatur-oder Verschlüsselungs Zertifikat Datei

Wenn keine Argumente angegeben werden, wird jedes Zertifikat der Signatur Zertifizierungsstelle anhand des privaten Schlüssels überprüft.

Dieser Vorgang kann nur für lokale Zertifizierungsstellen oder lokale Schlüssel ausgeführt werden.

[-f] [-user] [-silent] [-config machine\caname]

Zurück zum [Menü](#menu)

## <a name="-verify"></a>-Überprüfen

Certutil [Optionen]-Verify CertFile [applicationpolicylist |-[issuancepolicylist]]

Certutil [Optionen]-Verify CertFile [CACertFile [crossedcacertfile]]

Certutil [Optionen]-Überprüfen der crlfile-CACertFile [issuedcertfile]

Certutil [Optionen]-Überprüfen der crlfile-CACertFile [Delta-Datei]

Zertifikat, CRL oder Kette überprüfen

CertFile Zu überprüfende Zertifikat

Applicationpolicylist: optionale durch Trennzeichen getrennte Liste erforderlicher Anwendungsrichtlinien-ObjectIDs

Issuancepolicylist: optionale durch Trennzeichen getrennte Liste der erforderlichen Ausstellungs Richtlinien-ObjectIDs

CACertFile: Optionales ausstell Endes Zertifizierungsstellen Zertifikat für die Überprüfung

Crossedcacertfile: Optionales Zertifikat von CertFile Cross-Certified

Crldatei Zu überprüfende CRL

Issuedcertfile: Optionales ausgestelltes Zertifikat, das von crlfile abgedeckt wird.

Deltacrlfile: optionale Delta-CRL

Wenn applicationpolicylist angegeben wird, ist die Ketten Bildung auf die für die angegebenen Anwendungsrichtlinien gültigen Ketten beschränkt.

Wenn issuancepolicylist angegeben wird, ist die Ketten Erstellung auf die für die angegebenen Ausstellungs Richtlinien gültigen Ketten beschränkt.

Wenn "CACertFile" angegeben ist, werden Felder in CACertFile anhand von "CertFile" oder "crlfile" überprüft.

Wenn CACertFile nicht angegeben wird, wird CertFile verwendet, um eine vollständige Kette zu erstellen und zu überprüfen.

Wenn "CACertFile" und "crossedcacertfile" angegeben sind, werden die Felder in "CACertFile" und "crossedcacertfile" anhand von "CertFile" überprüft.

Wenn issuedcertfile angegeben wird, werden die Felder in issuedcertfile anhand von crlfile überprüft.

Wenn Delta Server File angegeben ist, werden Felder in der Delta-Datei mit crlfile überprüft.

[-f] [-Enterprise] [-user] [-silent] [-Split] [-urlfetch] [-t Timeout]

Zurück zum [Menü](#menu)

## <a name="-verifyctl"></a>-verifyctl

Certutil [Optionen]-verifyctl ctlobject [certdir] [CertFile]

Überprüfen der CTL für AuthRoot oder unzulässige Zertifikate

Ctlobject: Identifiziert die zu überprüfende CTL:

- Authrootwu: Lesen Sie das AuthRoot-CAB und übereinstimmende Zertifikate aus dem URL-Cache. Verwenden Sie-f, um stattdessen aus Windows Update herunterzuladen.
- Diszuweisung wedwu: Lese-und unzulässige Zertifikat Speicherdateien aus dem URL-Cache lesen.  Verwenden Sie-f, um stattdessen aus Windows Update herunterzuladen.
- AuthRoot: Lesen der Registrierungs zwischengespeicherten AuthRoot-CTL.  Verwenden Sie with-f und eine CertFile, die noch nicht vertrauenswürdig ist, um das Aktualisieren der Registrierung zwischengespeicherten AuthRoot-und unzulässigen Zertifikat-CTLs zu erzwingen.
- Nicht zulässig: Lesen der von der Registrierung zwischengespeicherten, nicht zulässigen Zertifikate in CTL. -f hat das gleiche Verhalten wie bei AuthRoot.
- Ctlfilename: File oder http: Pfad zu CTL oder CAB

Certdir: Ordner mit Zertifikaten, die mit CTL-Einträgen übereinstimmen. Ein http:-Ordner Pfad muss mit einem Pfad Trennzeichen enden. Wenn ein Ordner nicht mit AuthRoot oder nicht zulässig angegeben wird, werden mehrere Speicherorte nach übereinstimmenden Zertifikaten gesucht: lokale Zertifikat Speicher, crypt32. dll-Ressourcen und der lokale URL-Cache. Verwenden Sie-f, um bei Bedarf von Windows Update herunterzuladen. Andernfalls entspricht der Standardwert dem gleichen Ordner oder der gleichen Website wie das ctlobject.

CertFile: die Datei, die die zu überprüfende Zertifikate enthält. Zertifikate werden mit CTL-Einträgen abgeglichen, und die angezeigten Ergebnisse werden abgeglichen. Unterdrückt den größten Teil der Standardausgabe.

[-f] [-user] [-Split]

Zurück zum [Menü](#menu)

## <a name="-sign"></a>-Sign

Certutil [Optionen]-Signieren von infilelist | SerialNumber | CRL outfilelist [StartDate + DD: hh] [+ serialzahllist |-serialnumlist |-objectidlist | \@extensionfile]

Certutil [Optionen]-Signieren von infilelist | SerialNumber | CRL outfilelist [#HashAlgorithm] [+-Alternative </> >

Erneutes Signieren der CRL oder des Zertifikats

Infilelist: durch Trennzeichen getrennte Liste der Zertifikat-oder CRL-Dateien, die geändert und neu signiert werden sollen.

SerialNumber Seriennummer des zu erstellenden Zertifikats. Der Gültigkeits Zeitraum und andere Optionen dürfen nicht vorhanden sein.

CRL Erstellen Sie eine leere CRL. Der Gültigkeits Zeitraum und andere Optionen dürfen nicht vorhanden sein.

Outfilelist: durch Trennzeichen getrennte Liste der geänderten Zertifikats-oder CRL-Ausgabedateien. Die Anzahl der Dateien muss mit "infilelist" verglichen werden.

StartDate + DD: hh: neue Gültigkeitsdauer: Optionales Datum plus; optionale Gültigkeitsdauer für Tage und Stunden; Wenn beide angegeben sind, verwenden Sie ein Pluszeichen Trennzeichen (+). Verwenden Sie "Now [+ DD: hh]", um zum aktuellen Zeitpunkt zu starten. Verwenden Sie "Never" nicht für das Ablaufdatum (nur für CRLs).

Serialzahllist: durch Trennzeichen getrennte Liste mit durch Trennzeichen getrennten Seriennummern

Objectidlist: durch Trennzeichen getrennte Erweiterung ObjectID List to Remove

\@Extensionfile: INF-Datei mit Erweiterungen zum Aktualisieren oder entfernen:

```
[Extensions]
     2.5.29.31 = ; Remove CRL Distribution Points extension
     2.5.29.15 = "{hex}" ; Update Key Usage extension
     _continue_="03 02 01 86"
```

HashAlgorithm Der Name des Hash Algorithmus, dem ein #-Zeichen vorangestellt ist.

Alternate-SignatureAlgorithm: alternativer Signatur Algorithmus-Spezifizierer

Ein Minuszeichen bewirkt, dass Seriennummern und Erweiterungen entfernt werden. Ein Pluszeichen bewirkt, dass Seriennummern zu einer CRL hinzugefügt werden. Beim Entfernen von Elementen aus einer Zertifikat Sperr Liste enthält die Liste möglicherweise sowohl Seriennummern als auch ObjectIDs. Ein Minuszeichen vor dem Wert von "Alternative-SignatureAlgorithm" bewirkt, dass das Legacy Signatur Format verwendet wird. Ein Pluszeichen vor dem "Alternativen"-Wert von "Alternative" bewirkt, dass das alternature-Signatur Format verwendet wird. Wenn die Angabe von "Alternative-SignatureAlgorithm" nicht angegeben wird, wird das Signatur Format im Zertifikat oder der CRL verwendet.

[-nullsign] [-f] [-silent] [-CERT CertID]

Zurück zum [Menü](#menu)

## <a name="-vroot"></a>-vroot

Certutil [Optionen]-vroot [löschen]

Erstellen/Löschen von virtuellen Webstamm-und Dateifreigaben

Zurück zum [Menü](#menu)

## <a name="-vocsproot"></a>-vocsproot

Certutil [Optionen]-vocsproot [löschen]

Erstellen/Löschen von virtuellen Web-Stamm Stämmen für OCSP-WebProxy

Zurück zum [Menü](#menu)

## <a name="-addenrollmentserver"></a>-addenrollmentserver

Certutil [options]-addenrollmentserver Kerberos | Benutzername | ClientCertificate [allowrenewalsonly] [allowkeybasedrenewal]

Hinzufügen einer Registrierungs Server Anwendung

Fügen Sie ggf. eine Registrierungs Server Anwendung und einen Anwendungs Pool für die angegebene Zertifizierungsstelle hinzu. Mit diesem Befehl werden keine Binärdateien oder Pakete installiert. Eine der folgenden Authentifizierungsmethoden, mit denen der Client eine Verbindung mit einem Zertifikat Registrierungs Server herstellt.

- Kerberos Kerberos-SSL-Anmelde Informationen verwenden
- User Benanntes Konto für SSL-Anmelde Informationen verwenden
- ClientCertificate SSL-Anmelde Informationen für X. 509-Zertifikate verwenden
- Allowrenewalsonly: Nur Erneuerungs Anforderungen können über diese URL an diese Zertifizierungsstelle übermittelt werden.
- Allowkeybasedrenewal: ermöglicht die Verwendung eines Zertifikats, das über kein zugeordnetes Konto in der AD-Verbindung verfügt. Dies gilt nur für den Modus "ClientCertificate" und "allowrenewalsonly".

[-config machine\caname]

Zurück zum [Menü](#menu)

## <a name="-deleteenrollmentserver"></a>-deleteenrollmentserver

Certutil [Optionen]-deleteenrollmentserver Kerberos | Benutzername | ClientCertificate

Löschen einer Registrierungs Server Anwendung

Löschen Sie ggf. eine Registrierungs Server Anwendung und einen Anwendungs Pool für die angegebene Zertifizierungsstelle. Mit diesem Befehl werden keine Binärdateien oder Pakete entfernt. Eine der folgenden Authentifizierungsmethoden, mit denen der Client eine Verbindung mit einem Zertifikat Registrierungs Server herstellt.

1. Kerberos Kerberos-SSL-Anmelde Informationen verwenden
2. User Benanntes Konto für SSL-Anmelde Informationen verwenden
3. ClientCertificate SSL-Anmelde Informationen für X. 509-Zertifikate verwenden

[-config machine\caname]

Zurück zum [Menü](#menu)

## <a name="-addpolicyserver"></a>-addpolicyserver

Certutil [Optionen]-addpolicyserver Kerberos | Benutzername | ClientCertificate [keybasedrenewal]

Hinzufügen einer Richtlinien Server Anwendung

Fügen Sie ggf. eine Richtlinien Server Anwendung und einen Anwendungs Pool hinzu. Mit diesem Befehl werden keine Binärdateien oder Pakete installiert. Eine der folgenden Authentifizierungsmethoden, mit denen der Client eine Verbindung mit einem Zertifikat Richtlinien Server herstellt:

- Kerberos Kerberos-SSL-Anmelde Informationen verwenden
- User Benanntes Konto für SSL-Anmelde Informationen verwenden
- ClientCertificate SSL-Anmelde Informationen für X. 509-Zertifikate verwenden
- Keybasedrenewal: Nur Richtlinien, die keybasedrenewal-Vorlagen enthalten, werden an den Client zurückgegeben. Dieses Flag gilt nur für die Benutzername-und ClientCertificate-Authentifizierung.

Zurück zum [Menü](#menu)

## <a name="-deletepolicyserver"></a>-deletepolicyserver

Certutil [Optionen]-deletepolicyserver Kerberos | Benutzername | ClientCertificate [keybasedrenewal]

Löschen einer Richtlinien Server Anwendung

Löschen Sie ggf. eine Richtlinien Server Anwendung und einen Anwendungs Pool. Mit diesem Befehl werden keine Binärdateien oder Pakete entfernt. Eine der folgenden Authentifizierungsmethoden, mit denen der Client eine Verbindung mit einem Zertifikat Richtlinien Server herstellt:

1. Kerberos Kerberos-SSL-Anmelde Informationen verwenden
2. User Benanntes Konto für SSL-Anmelde Informationen verwenden
3. ClientCertificate SSL-Anmelde Informationen für X. 509-Zertifikate verwenden
4. Keybasedrenewal: Keybasedrenewal-Richtlinien Server

Zurück zum [Menü](#menu)

## <a name="-oid"></a>-OID

Certutil [Optionen]-OID objectid [Display Name | delete [LanguageID [Type]]]

Certutil [Optionen]-OID groupID

Certutil [Optionen]-OID algid | AlgorithmName [GroupID]

Anzeigen von ObjectID oder Festlegen des anzeigen Amens

- ObjectID--ObjectID zum Anzeigen oder anzeigen Amen hinzufügen
- GroupID--Dezimalzahl der groupid für ObjectIDs zum Aufzählen
- Algid--hexadezimale algid für ObjectID für die Suche
- AlgorithmName: Algorithmusname für ObjectID, der gesucht werden soll.
- Display Name: Anzeige Name, der in DS gespeichert werden soll
- DELETE--Anzeige Name löschen
- LanguageID--Sprach-ID (standardmäßig aktuell): 1033)
- Typ--DS Objekttyp, der erstellt werden soll: 1 für Vorlage (Standard), 2 für Ausstellungs Richtlinie, 3 für Anwendungs Richtlinie
- Verwenden Sie-f zum Erstellen eines DS-Objekts.

[-f]

Zurück zum [Menü](#menu)

## <a name="-error"></a>-Fehler

Certutil [Optionen]-Fehler ErrorCode

Text der Fehlercode Meldung anzeigen

Zurück zum [Menü](#menu)

## <a name="-getreg"></a>-getreg

Certutil [Optionen]-getreg [{ca | Restore | Policy | Exit | Template | ENROLL | Chain | Policyservers} \[progid @ no__t-1] [registryvaluename]

Registrierungs Wert anzeigen

etwa Registrierungsschlüssel der Zertifizierungsstelle verwenden

zurück Registrierungsschlüssel für die Wiederherstellung der Zertifizierungsstelle verwenden

Policy Registrierungsschlüssel des Richtlinien Moduls verwenden

Abstiegs Registrierungsschlüssel des ersten Beendigungs Moduls verwenden

fungiert Verwenden Sie den Vorlagen Registrierungsschlüssel (use-User für Benutzervorlagen).

Registrieren Registrierungsschlüssel für Registrierung verwenden (Benutzer für Benutzer Kontext verwenden)

Ketten Registrierungsschlüssel für die Ketten Konfiguration verwenden

Policyservers: Registrierungsschlüssel für Richtlinien Server verwenden

ProgID ProgID der Richtlinie oder des Beendigungs Moduls (Name des Registrierungs unter Schlüssels) verwenden

Registryvaluename: Name des Registrierungs Werts (verwenden Sie\*"Name", um eine Entsprechung zu erreichen)

Wert: neuer numerischer Wert, Zeichen folgen-oder Datums Registrierungs Wert oder Dateiname. Wenn ein numerischer Wert mit "+" oder "-" beginnt, werden die im neuen Wert angegebenen Bits im vorhandenen Registrierungs Wert festgelegt oder gelöscht.

Wenn ein Zeichen folgen Wert mit "+" oder "-" beginnt und der vorhandene Wert ein REG_MULTI_SZ-Wert ist, wird die Zeichenfolge dem vorhandenen Registrierungs Wert hinzugefügt oder daraus entfernt. Um die Erstellung eines REG_MULTI_SZ-Werts zu erzwingen, fügen Sie am Ende des Zeichen folgen Werts "\n" ein.

Wenn der Wert mit "\@" beginnt, ist der restliche Wert der Name der Datei, die die hexadezimale Textdarstellung eines binären Werts enthält. Wenn Sie nicht auf eine gültige Datei verweist, wird Sie stattdessen als [Date] [+ |-] [DD: hh] (ein optionales Datum plus oder minus optionale Tage und Stunden) analysiert. Wenn beide angegeben sind, verwenden Sie ein Pluszeichen (+) oder Minuszeichen (-). Verwenden Sie "now + DD: hh" für ein Datum relativ zum aktuellen Zeitpunkt.

Verwenden Sie "chain\chaincacheresyncfiletime \@Now", um zwischengespeicherte CRLs effektiv zu leeren.

[-f] [-user] [-GroupPolicy] [-config machine\caname]

Zurück zum [Menü](#menu)

## <a name="-setreg"></a>-Eing

Certutil [Optionen]-setreg [{ca | Restore | Policy | Exit | Template | ENROLL | Chain | Policyservers} \[progid @ no__t-1] registryvaluename-Wert

Registrierungs Wert festlegen

etwa Registrierungsschlüssel der Zertifizierungsstelle verwenden

zurück Registrierungsschlüssel für die Wiederherstellung der Zertifizierungsstelle verwenden

Policy Registrierungsschlüssel des Richtlinien Moduls verwenden

Abstiegs Registrierungsschlüssel des ersten Beendigungs Moduls verwenden

fungiert Verwenden Sie den Vorlagen Registrierungsschlüssel (use-User für Benutzervorlagen).

Registrieren Registrierungsschlüssel für Registrierung verwenden (Benutzer für Benutzer Kontext verwenden)

Ketten Registrierungsschlüssel für die Ketten Konfiguration verwenden

Policyservers: Registrierungsschlüssel für Richtlinien Server verwenden

ProgID ProgID der Richtlinie oder des Beendigungs Moduls (Name des Registrierungs unter Schlüssels) verwenden

Registryvaluename: Name des Registrierungs Werts (verwenden Sie\*"Name", um eine Entsprechung zu erreichen)

Wert: neuer numerischer Wert, Zeichen folgen-oder Datums Registrierungs Wert oder Dateiname. Wenn ein numerischer Wert mit "+" oder "-" beginnt, werden die im neuen Wert angegebenen Bits im vorhandenen Registrierungs Wert festgelegt oder gelöscht.

Wenn ein Zeichen folgen Wert mit "+" oder "-" beginnt und der vorhandene Wert ein REG_MULTI_SZ-Wert ist, wird die Zeichenfolge dem vorhandenen Registrierungs Wert hinzugefügt oder daraus entfernt. Um die Erstellung eines REG_MULTI_SZ-Werts zu erzwingen, fügen Sie am Ende des Zeichen folgen Werts "\n" ein.

Wenn der Wert mit "\@" beginnt, ist der restliche Wert der Name der Datei, die die hexadezimale Textdarstellung eines binären Werts enthält. Wenn Sie nicht auf eine gültige Datei verweist, wird Sie stattdessen als [Date] [+ |-] [DD: hh] (ein optionales Datum plus oder minus optionale Tage und Stunden) analysiert. Wenn beide angegeben sind, verwenden Sie ein Pluszeichen (+) oder Minuszeichen (-). Verwenden Sie "now + DD: hh" für ein Datum relativ zum aktuellen Zeitpunkt.

Verwenden Sie "chain\chaincacheresyncfiletime \@Now", um zwischengespeicherte CRLs effektiv zu leeren.

[-f] [-user] [-GroupPolicy] [-config machine\caname]

Zurück zum [Menü](#menu)

## <a name="-delreg"></a>-Delta reg

Certutil [Optionen]-Delta [{ca | Restore | Policy | Exit | Template | ENROLL | Chain | Policyservers} \[progid @ no__t-1] [registryvaluename]

Registrierungs Wert löschen

etwa Registrierungsschlüssel der Zertifizierungsstelle verwenden

zurück Registrierungsschlüssel für die Wiederherstellung der Zertifizierungsstelle verwenden

Policy Registrierungsschlüssel des Richtlinien Moduls verwenden

Abstiegs Registrierungsschlüssel des ersten Beendigungs Moduls verwenden

fungiert Verwenden Sie den Vorlagen Registrierungsschlüssel (use-User für Benutzervorlagen).

Registrieren Registrierungsschlüssel für Registrierung verwenden (Benutzer für Benutzer Kontext verwenden)

Ketten Registrierungsschlüssel für die Ketten Konfiguration verwenden

Policyservers: Registrierungsschlüssel für Richtlinien Server verwenden

ProgID ProgID der Richtlinie oder des Beendigungs Moduls (Name des Registrierungs unter Schlüssels) verwenden

Registryvaluename: Name des Registrierungs Werts (verwenden Sie\*"Name", um eine Entsprechung zu erreichen)

Wert: neuer numerischer Wert, Zeichen folgen-oder Datums Registrierungs Wert oder Dateiname. Wenn ein numerischer Wert mit "+" oder "-" beginnt, werden die im neuen Wert angegebenen Bits im vorhandenen Registrierungs Wert festgelegt oder gelöscht.

Wenn ein Zeichen folgen Wert mit "+" oder "-" beginnt und der vorhandene Wert ein REG_MULTI_SZ-Wert ist, wird die Zeichenfolge dem vorhandenen Registrierungs Wert hinzugefügt oder daraus entfernt. Um die Erstellung eines REG_MULTI_SZ-Werts zu erzwingen, fügen Sie am Ende des Zeichen folgen Werts "\n" ein.

Wenn der Wert mit "\@" beginnt, ist der restliche Wert der Name der Datei, die die hexadezimale Textdarstellung eines binären Werts enthält. Wenn Sie nicht auf eine gültige Datei verweist, wird Sie stattdessen als [Date] [+ |-] [DD: hh] (ein optionales Datum plus oder minus optionale Tage und Stunden) analysiert. Wenn beide angegeben sind, verwenden Sie ein Pluszeichen (+) oder Minuszeichen (-). Verwenden Sie "now + DD: hh" für ein Datum relativ zum aktuellen Zeitpunkt.

Verwenden Sie "chain\chaincacheresyncfiletime \@Now", um zwischengespeicherte CRLs effektiv zu leeren.

[-f] [-user] [-GroupPolicy] [-config machine\caname]

Zurück zum [Menü](#menu)

## <a name="-importkms"></a>-Importkms

Certutil [Optionen]-importkms userkeyandcertfile [CertID]

Importieren von Benutzer Schlüsseln und Zertifikaten in die Server Datenbank für die Schlüssel Archivierung

Userkeyandcertfile: die Datendatei mit den privaten Schlüsseln und Zertifikaten, die für den Benutzer verwendet werden sollen.  Dabei kann es sich um Folgendes handeln:

- Exportdatei für Exchange Key Management Server (KMS)
- PFX-Datei

CertId Verbindungs Token für das KMS-Exportdatei-Entschlüsselungs Zertifikat.  Siehe [-Store](#-store).

Verwenden Sie-f zum Importieren von Zertifikaten, die nicht von der Zertifizierungsstelle ausgestellt wurden.

[-f] [-silent] [-Split] [-config machine\caname] [-p Kennwort] [-symkeyalg symmetrickeyalgorithmus [, keylength]]

Zurück zum [Menü](#menu)

## <a name="-importcert"></a>-Import CERT

Certutil [Optionen]-importcert CertFile [existingrow]

Importieren einer Zertifikatsdatei in die Datenbank

Verwenden Sie "existingrow", um das Zertifikat anstelle einer ausstehenden Anforderung für denselben Schlüssel zu importieren.

Verwenden Sie-f zum Importieren von Zertifikaten, die nicht von der Zertifizierungsstelle ausgestellt wurden.

Die Zertifizierungsstelle muss möglicherweise auch für die Unterstützung von Importieren von fremd Zertifikaten konfiguriert werden: certutil-setreg ca\kraflags + KRAF_ENABLEFOREIGN

[-f] [-config machine\caname]

Zurück zum [Menü](#menu)

## <a name="-getkey"></a>-GetKey

Certutil [Optionen]-GetKey searchtoken [wiederherstellungsbloboutfile]

Certutil [Optionen]-GetKey searchtoken-Skript outputScriptFile

Certutil [Optionen]-GetKey searchtoken abrufen | "outputfilebasename" Wiederherstellen

Abrufen von archivierten BLOBs für die Wiederherstellung von privaten Schlüsseln, Generieren eines Wiederherstellungs Skripts oder Wiederherstellen von

Skript: Generieren Sie ein Skript zum Abrufen und Wiederherstellen von Schlüsseln (Standardverhalten, wenn mehrere übereinstimmende Wiederherstellungs Kandidaten gefunden werden oder wenn die Ausgabedatei nicht angegeben ist).

abrufen: Abrufen eines oder mehrerer schlüsselwiederherstellungsblobwerte (Standardverhalten, wenn genau ein entsprechender Wiederherstellungs Kandidat gefunden wird und wenn die Ausgabedatei angegeben ist)

Wiederherstellung: Abrufen und Wiederherstellen privater Schlüssel in einem Schritt (erfordert Schlüssel Wiederherstellungs-Agentzertifikate und private Schlüssel)

Searchtoken: Wird verwendet, um die Schlüssel und Zertifikate auszuwählen, die wieder hergestellt werden sollen.

Folgende Aktionen sind möglich:

1. Allgemeiner Name des Zertifikats
2. Seriennummer des Zertifikats
3. SHA-1-Hash Hash (Fingerabdruck)
4. Zertifikat-keyid SHA-1-Hash (Subjekt Schlüssel Bezeichner)
5. Requestname (Domäne \ Benutzer)
6. UPN (Benutzer\@Domäne)

Wiederherstellungsbloboutfile: die Ausgabedatei mit einer Zertifikat Kette und einem zugeordneten privaten Schlüssel ist weiterhin in einem oder mehreren Schlüsselwiederherstellungs-Agent-Zertifikaten verschlüsselt.

OutputScriptFile: Ausgabedatei mit einem Batch Skript zum Abrufen und Wiederherstellen privater Schlüssel.

Outputfilebasename: Basis Name der Ausgabedatei. Zum Abrufen werden alle Erweiterungen abgeschnitten, und für jedes Schlüsselwiederherstellungs-BLOB wird eine Zertifikat spezifische Zeichenfolge und die Erweiterung ". Rec" angehängt.  Jede Datei enthält eine Zertifikat Kette und einen zugeordneten privaten Schlüssel, die weiterhin in einem oder mehreren Schlüsselwiederherstellungs-Agent-Zertifikaten verschlüsselt sind. Bei der Wiederherstellung wird jede Erweiterung abgeschnitten, und die Erweiterung ". p12" wird angehängt.  Enthält die wiederhergestellten Zertifikat Ketten und zugeordneten privaten Schlüssel, die als PFX-Datei gespeichert werden.

[-f] [-UnicodeText] [-silent] [-config machine\caname] [-p Kennwort] [-Protectto samnameandsidlist] [-CSP-Anbieter]

Zurück zum [Menü](#menu)

## <a name="-recoverkey"></a>-Recoverkey

Certutil [Optionen]-recoverkey wiederherstellungblobindatei [pfxoutfile [Empfänger Index]]

Wiederherstellen von archivierten privaten Schlüsseln

[-f] [-user] [-silent] [-Split] [-p Kennwort] [-Protectto samnameandsidlist] [-CSP-Anbieter] [-t Timeout]

Zurück zum [Menü](#menu)

## <a name="-mergepfx"></a>-MergePFX

Certutil [Optionen]-MergePFX pfxinfilelist pfxoutfile [ExtendedProperties]

Pfxinfilelist: Durch Trennzeichen getrennte Liste der PFX-Eingabedateien

Pfxoutfile: PFX-Ausgabedatei

Collectionobjekte Erweiterte Eigenschaften einschließen

Das in der Befehlszeile angegebene Kennwort ist eine durch Trennzeichen getrennte Kenn Wort Liste.  Wenn mehr als ein Kennwort angegeben wird, wird das letzte Kennwort für die Ausgabedatei verwendet.  Wenn nur ein Kennwort angegeben wird, oder wenn das letzte Kennwort "\*" lautet, wird der Benutzer zur Eingabe des Kennworts für die Ausgabedatei aufgefordert.

[-f] [-user] [-Split] [-p Kennwort] [-Protectto samnameandsidlist] [-CSP-Anbieter]

Zurück zum [Menü](#menu)

## <a name="-convertepf"></a>-Convertepf

Certutil [Optionen]-convertepf pfxinfilelist epfoutfile [Cast | Cast-] [V3CACertId] [, Salt]

Konvertieren von PFX-Dateien in eine EPF-Datei

Pfxinfilelist: Durch Trennzeichen getrennte Liste der PFX-Eingabedateien

EPF: EPF-Ausgabedatei

Darsteller Verwenden der CAST 64-Verschlüsselung

Umwandlung: Verwenden von CAST 64 Encryption (Export)

V3CACertId: V3-Zertifikat Übereinstimmungs Token.  Siehe [-Store](#-store) CertID Description.

Burgern EPF-Ausgabedatei, Salt-Zeichenfolge

Das in der Befehlszeile angegebene Kennwort ist eine durch Trennzeichen getrennte Kenn Wort Liste. Wenn mehr als ein Kennwort angegeben wird, wird das letzte Kennwort für die Ausgabedatei verwendet.  Wenn nur ein Kennwort angegeben wird, oder wenn das letzte Kennwort "\*" lautet, wird der Benutzer zur Eingabe des Kennworts für die Ausgabedatei aufgefordert.

[-f] [-silent] [-Split] [-DC DCNAME] [-p Kennwort] [-CSP-Anbieter]

Zurück zum [Menü](#menu)

## <a name="options"></a>Optionen

In diesem Abschnitt werden die Optionen definiert, die Sie mit dem Befehl angeben können.

|Optionen|Beschreibung|
|-------|-----------|
|-nullsign|Hash der Daten als Signatur verwenden|
|-f|Überschreiben erzwingen|
|-Enterprise|Zertifikat Speicher für die Unternehmens Registrierung des lokalen Computers verwenden|
|-Benutzer|HKEY_CURRENT_USER-Schlüssel oder Zertifikat Speicher verwenden|
|-GroupPolicy|Gruppenrichtlinie Zertifikat Speicher verwenden|
|-UT|Anzeigen von Benutzervorlagen|
|-MT|Anzeigen von Maschinen Vorlagen|
|-Unicode|Umgeleitete Ausgabe in Unicode schreiben|
|-UnicodeText|Ausgabedatei in Unicode schreiben|
|-GMT|Anzeige Zeiten als GMT|
|-Sekunden|Anzeige Zeiten mit Sekunden und Millisekunden|
|-unbeaufsichtigt|Verwenden des automatischen Flags zum Abrufen des Crypt-Kontexts|
|-Teilen|Eingebettete ASN. 1-Elemente aufteilen und in Dateien speichern|
|-v|Verbose-Vorgang|
|-PrivateKey|Anzeigen von Daten zum Kennwort und zum privaten Schlüssel|
|-PIN anheften|Smartcard-PIN|
|-urlfetch|Abrufen und Überprüfen von AIA certs und CDP-CRLs|
|-config machine\caname|Zeichenfolge für ZS und Computername|
|-Policyserver urlorid|URL oder ID des Richtlinien Servers. Verwenden Sie für Auswahl-U/I-policyserver. Verwenden Sie für alle Richtlinien Server "-policyserver".\*|
|-Anonym|Anonyme SSL-Anmelde Informationen verwenden|
|-Kerberos|Kerberos-SSL-Anmelde Informationen verwenden|
|-ClientCertificate clientcertid|SSL-Anmelde Informationen des X. 509-Zertifikats verwenden. Verwenden Sie für Auswahl-U/I die Option-ClientCertificate.|
|-Username username|Verwenden Sie das benannte Konto für SSL-Anmelde Informationen. Verwenden Sie für Auswahl-U/I den-Benutzernamen.|
|-CERT CertID|Signaturzertifikat|
|-DC DCNAME|Ziel eines bestimmten Domänen Controllers|
|-Einschränkungs Liste einschränken|Durch Trennzeichen getrennte Einschränkungs Liste. Jede Einschränkung besteht aus einem Spaltennamen, einem relationalen Operator und einer Konstanten Ganzzahl, einer Zeichenfolge oder einem Datum. Einem Spaltennamen kann ein Plus-oder Minuszeichen vorangestellt werden, um die Sortierreihenfolge anzugeben. Beispiele:</br>"RequestId = 47"</br>"+ Requestername > = a, requestername < b"</br>"-Requestername > Domäne, Disposition = 21"|
|-Out ColumnList|Durch Trennzeichen getrennte Spaltenliste|
|-p Kennwort|Kennwort|
|-Protectto samnameandsidlist|Durch Trennzeichen getrennte SAM-Name/sid-Liste|
|-CSP-Anbieter|Anbieter|
|-t Timeout|URL-Abruf Timeout in Millisekunden|
|-symkeyalg symmetrickeyalgorithmus [, keylength]|Name des symmetrischen Schlüssel Algorithmus mit optionaler Schlüssellänge, Beispiel: AES, 128 oder 3DES|

Zurück zum [Menü](#menu)

## <a name="additional-certutil-examples"></a>Weitere certutil-Beispiele

Einige Beispiele für die Verwendung dieses Befehls finden Sie unter.

1. [Certutil-Beispiele für die Verwaltung von Active Directory Zertifikat Diensten (AD CS) über die Befehlszeile](https://social.technet.microsoft.com/wiki/contents/articles/3063.certutil-examples-for-managing-active-directory-certificate-services-ad-cs-from-the-command-line.aspx)
2. [Certutil-Aufgaben für die Verwaltung von Zertifikaten](https://technet.microsoft.com/library/cc772898.aspx)
3. [Binärer Anforderungs Export mithilfe des Befehlszeilen Tools "Certutil. exe" Exemplarische Vorgehensweise](https://social.technet.microsoft.com/wiki/contents/articles/7573.active-directory-certificate-services-pki-key-archival-and-management.aspx)
4. [Zertifikat Erneuerung der Stamm Zertifizierungsstelle](https://social.technet.microsoft.com/wiki/contents/articles/2016.root-ca-certificate-renewal.aspx)
5. [Certutil](https://msdn.microsoft.com/subscriptions/cc773087.aspx)

Zurück zum [Menü](#menu)
