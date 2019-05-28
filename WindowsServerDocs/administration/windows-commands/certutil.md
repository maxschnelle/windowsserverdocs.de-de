---
title: certutil
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: faaf936e4c23579e908e12543c07d0764a2cdcc1
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192621"
---
# <a name="certutil"></a>certutil

Certutil.exe ist ein Befehlszeilenprogramm, das als Teil der Zertifikatdienste installiert wird. Können Sie Certutil.exe speichern und Anzeigen von Zertifizierungsstellen (ZS)-Konfigurationsinformationen, konfigurieren, Zertifikatdienste, Sichern und Wiederherstellen von Komponenten der Zertifizierungsstelle und stellen Sie sicher, Zertifikaten, Schlüsselpaaren und Zertifikatketten.

Wenn Certutil auf einer Zertifizierungsstelle ohne zusätzliche Parameter ausgeführt wird, wird die aktuelle Zertifizierungsstellenkonfiguration angezeigt. Wenn Cerutil auf einer Zertifizierungsstelle ausgeführt wird, standardmäßig der Befehl mit dem Certutil [-Dump](#-dump) Verb.

> [!WARNING]
> Frühere Versionen von Certutil möglicherweise keine aller Optionen bereit, die in diesem Dokument beschrieben werden. Sehen Sie alle Optionen, die eine bestimmte Version von Certutil bereitstellt, durch Ausführen der Befehle angezeigt, der [Syntax Notationen](#syntax-notations) Abschnitt.

## <a name="menu"></a>Menü

Sind die wichtigsten Abschnitte in diesem Dokument:

- [Verbs](#verbs)
- [Die Syntax Notationen](#syntax-notations)
- [Options](#options)
- [Zusätzliche Certutil-Beispiele](#additional-certutil-examples)

## <a name="verbs"></a>Verben

Die folgende Tabelle beschreibt die Verben, die mit den Certutil-Befehl verwendet werden können.

|Verben|Beschreibung|
|-----|-----------|
|[-dump](#-dump)|Speichern von Konfigurationsinformationen oder Dateien|
|[-asn](#-asn)|Analysieren Sie die ASN. 1-Datei|
|[-decodehex](#-decodehex)|Decodiert eine hexadezimal codierte Datei.|
|[-decode](#-decode)|Decodiert eine Base64-codierte Datei|
|[-encode](#-encode)|Eine Datei in Base64 codieren|
|[-deny](#-deny)|Ablehnen einer ausstehenden zertifikatanforderung|
|[-resubmit](#-resubmit)|Erneut übermitteln einer ausstehenden zertifikatanforderung|
|[-setattributes](#-setattributes)|Festlegen von Attributen für einer ausstehenden zertifikatanforderung|
|[-setextension](#-setextension)|Legen Sie eine Erweiterung für einer ausstehenden zertifikatanforderung|
|[-revoke](#-revoke)|Sperren eines Zertifikats|
|[-isvalid](#-isvalid)|Die Disposition des aktuellen Zertifikats anzeigen|
|[-getconfig](#-getconfig)|Die Standardzeichenfolge für die Konfiguration abrufen|
|[-ping](#-ping)|Versucht, die Active Directory Certificate Services anfordern-Schnittstelle zu kontaktieren.|
|-pingadmin|Versucht, die Schnittstelle für die Active Directory Certificate Services-Administrator zu kontaktieren.|
|[-CAInfo](#-cainfo)|Anzeigen von Informationen zu der Zertifizierungsstelle|
|[-ca.cert](#-cacert)|Rufen Sie das Zertifikat der Zertifizierungsstelle|
|[-ca.chain](#-cachain)|Abrufen der Zertifikatkette für die Zertifizierungsstelle|
|[-GetCRL](#-getcrl)|Abrufen einer Zertifikatsperrliste (CRL)|
|[-CRL](#-crl)|Veröffentlichen Sie neue Zertifikatsperrlisten (CRLs) [oder nur Delta-CRLs]|
|[-shutdown](#-shutdown)|Herunterfahren von Active Directory-Zertifikatdienste|
|[-installCert](#-installcert)|Installieren Sie ein Zertifikat der Zertifizierungsstelle|
|[-renewCert](#-renewcert)|Erneuern Sie ein Zertifikat der Zertifizierungsstelle|
|[-schema](#-schema)|Sichern Sie das Schema für das Zertifikat|
|[-view](#-view)|Sichern Sie die Zertifikatsansicht|
|[-db](#-db)|Sichern Sie den raw-Datenbank|
|[-deleterow](#-deleterow)|Löschen einer Zeile aus der Datenbank|
|[-backup](#-backup)|Sicherung von Active Directory-Zertifikatdienste|
|[-backupDB](#-backupdb)|Sichern Sie die Active Directory Certificate Services-Datenbank|
|[-backupKey](#-backupkey)|Sichern Sie die Active Directory-Zertifikatdienste-Zertifikat und den privaten Schlüssel|
|[-restore](#-restore)|Wiederherstellen von Active Directory-Zertifikatdienste|
|[-restoreDB](#-restoredb)|Stellen Sie die Active Directory Certificate Services-Datenbank|
|[-restoreKey](#-restorekey)|Wiederherstellen der Active Directory-Zertifikatdienste-Zertifikat und den privaten Schlüssel|
|[-importPFX](#-importpfx)|Importieren von Zertifikaten und privaten Schlüsseln|
|[-dynamicfilelist](#-dynamicfilelist)|Eine dynamische Dateiliste anzeigen|
|[-databaselocations](#-databaselocations)|Anzeigen von Datenbankspeicherorten|
|[-hashfile](#-hashfile)|Generieren und einen kryptografischen Hash über eine Datei anzeigen|
|[-store](#-store)|Sichern Sie den Zertifikatspeicher|
|[-addstore](#-addstore)|Hinzufügen eines Zertifikats zum Zertifikatspeicher|
|[-delstore](#-delstore)|Löschen eines Zertifikats aus dem store|
|[-verifystore](#-verifystore)|Überprüfen Sie ein Zertifikat im Speicher|
|[-repairstore](#-repairstore)|Reparieren Sie eine wichtige Zuordnung, oder Aktualisieren von Zertifikateigenschaften und die wichtigsten Sicherheitsbeschreibung|
|[-viewstore](#-viewstore)|Sichern Sie den Zertifikatspeicher|
|[-viewdelstore](#-viewdelstore)|Löschen eines Zertifikats aus dem store|
|[-dsPublish](#-dspublish)|Veröffentlichen Sie ein Zertifikat oder die Zertifikatsperrliste (CRL) in Active Directory|
|[-ADTemplate](#-adtemplate)|Anzeigevorlagen AD|
|[-Template](#-template)|Anzeigen von Zertifikatvorlagen|
|[-TemplateCAs](#-templatecas)|Zeigen Sie die Zertifizierungsstellen (CAs) für eine Zertifikatvorlage|
|[-CATemplates](#-catemplates)|Vorlagen für Kanada anzuzeigen.|
|[-SetCASites](#-setcasites)|Verwalten von Standortnamen für Zertifizierungsstellen|
|[-enrollmentServerURL](#-enrollmentserverurl)|Anzeigen, hinzufügen oder Löschen von einer Zertifizierungsstelle zugeordnete Registrierungs-Server-URLs|
|[-ADCA](#-adca)|Anzeigen von AD-Zertifizierungsstellen|
|[-CA](#-ca)|Anzeigen der Registrierung Richtlinien-Zertifizierungsstellen|
|[-Policy](#-policy)|Anzeigen der Enrollment-Richtlinie|
|[-PolicyCache](#-policycache)|Anzeigen oder Löschen von Enrollment-Richtlinie Cacheeinträge|
|[-CredStore](#-credstore)|Anzeigen, hinzufügen oder Credential Store Einträge löschen|
|[-InstallDefaultTemplates](#-installdefaulttemplates)|Installieren Sie Standardzertifikatvorlagen|
|[-URLCache](#-urlcache)|Zeigen Sie an oder löschen Sie Einträge für URL-cache|
|[-pulse](#-pulse)|Pulse-automatische Registrierung Ereignisse|
|[-MachineInfo](#-machineinfo)|Anzeigen von Informationen zu den Active Directory-Computer-Objekt|
|[-DCInfo](#-dcinfo)|Anzeigen von Informationen zu den Domänencontroller|
|[-EntInfo](#-entinfo)|Anzeigen von Informationen zu einer Unternehmens-ZS|
|[-TCAInfo](#-tcainfo)|Anzeigen von Informationen zu der Zertifizierungsstelle|
|[-SCInfo](#-scinfo)|Informationen über die Smartcard anzeigen|
|[-SCRoots](#-scroots)|Verwalten von Smartcard-Stammzertifikate|
|[-verifykeys](#-verifykeys)|Vergewissern Sie sich einen öffentlichen oder privaten Schlüsselsatz|
|[-verify](#-verify)|Überprüfen Sie, ob ein Zertifikat, die Zertifikatsperrliste (CRL) oder die Zertifikatkette|
|[-verifyCTL](#-verifyctl)|Stellen Sie sicher AuthRoot oder Unzulässiger Zertifikate CTL|
|[-sign](#-sign)|Signieren Sie erneut eine Zertifikatsperrliste (CRL) oder ein Zertifikat|
|[-vroot](#-vroot)|Erstellen Sie oder löschen Sie virtueller Webstammverzeichnisse und Dateifreigaben|
|[-vocsproot](#-vocsproot)|Erstellen oder Löschen von Web virtuelle Stammverzeichnisse für ein OCSP-Web-proxy|
|[-addEnrollmentServer](#-addenrollmentserver)|Hinzufügen einer Anwendung Registrierungsserver|
|[-deleteEnrollmentServer](#-deleteenrollmentserver)|Löschen einer Anwendung Registrierungsserver|
|[-addPolicyServer](#-addpolicyserver)|Hinzufügen einer Anwendung der Richtlinien-Server|
|[-deletePolicyServer](#-deletepolicyserver)|Löschen einer Richtlinie von Server-Anwendung|
|[-oid](#-oid)|Die Objekt-ID angezeigt, oder legen Sie einen Anzeigenamen|
|[-error](#-error)|Zeigt den Meldungstext, der einen Fehlercode zugeordnet|
|[-getreg](#-getreg)|Anzeigen eines Registrierungswerts|
|[-setreg](#-setreg)|Festlegen eines Registrierungswerts|
|[-delreg](#-delreg)|Einen Registrierungswert löschen|
|[-ImportKMS](#-importkms)|Importieren von Benutzerschlüssel und Zertifikate in der Serverdatenbank für die schlüsselarchivierung|
|[-ImportCert](#-importcert)|Importieren eines Zertifikats in die Datenbank|
|[-GetKey](#-getkey)|Einen Blob archivierte Wiederherstellung von privaten Schlüsseln abrufen|
|[-RecoverKey](#-recoverkey)|Einen archivierten privaten Schlüssel wiederherstellen|
|[-MergePFX](#-mergepfx)|PFX-Dateien zusammenführen|
|[-ConvertEPF](#-convertepf)|Konvertieren Sie eine PFX-Datei in eine Datei EPF|
|-?|Zeigt die Liste der Verben|
|- *\<verb>* -?|Zeigt die Hilfe für das angegebene Verb.|
|-? -v|Zeigt eine vollständige Liste der Verben und|

Wechseln Sie zurück zur [Menü](#menu)

## <a name="syntax-notations"></a>Die Syntax Notationen

- Führen Sie für grundlegende Befehlszeilensyntax `certutil -?`
- Führen Sie die Syntax zum Verwenden von Certutil mit der ein bestimmtes Verb **Certutil**  *\<Verb >* **-?**
- Um die Certutil-Syntax in eine Textdatei zu senden, führen Sie die folgenden Befehle aus:  
  - `certutil -v -? > certutilhelp.txt`
  - `notepad certutilhelp.txt`

Die folgende Tabelle beschreibt die Notation verwendet, um die Syntax der Befehlszeile anzugeben.

|Notation|Beschreibung|
|--------|-----------|
|Text ohne eckigen oder geschweiften Klammern|Elemente, die Sie eingeben müssen, siehe|
|\<Text in spitzen Klammern >|Platzhalter für die Sie einen Wert angeben muss|
|[Text innerhalb der eckigen Klammern]|Optionale Elemente|
|{Text in geschweiften Klammern}|Der Satz von erforderlichen Elemente; Wählen Sie eine|
|Senkrechter Strich ()|)|Trennzeichen für sich gegenseitig ausschließende Elemente Wählen Sie eine|
|Auslassungspunkte (…)|Elemente, die wiederholt werden kann|

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-dump"></a>-Dumps

CertUtil [Optionen] [-Dump]

CertUtil [Optionen] [-Dump] Datei

Speichern von Konfigurationsinformationen oder Dateien

[-f]. [-silent] [-Teilen] [--p Kennwort] [-t Timeout]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-asn"></a>-asn

CertUtil [Optionen] - Asn-Datei [Typ]

Analysieren Sie die ASN. 1-Datei

Typ: numerisch CRYPT\_Zeichenfolge\_ \* Typ-Decodierung

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-decodehex"></a>-decodehex

CertUtil [Optionen] - Decodehex Eingabedatei OutFile [Typ]

Typ: numerisch CRYPT\_Zeichenfolge\_ \* Codierungstyp

[-f]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-decode"></a>-Decodierung

CertUtil [Optionen] - Decodierung Eingabedatei Ausgabedatei

Decodiert Base64-codierte Datei

[-f]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-encode"></a>-Codierung

CertUtil [Optionen] - Codierung der Eingabedatei Ausgabedatei

Codieren in Base64-Datei

[-f]. [-UnicodeText]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-deny"></a>-Verweigern

CertUtil [Optionen] - deny Anforderungs-ID

Ausstehende Anforderung verweigern

[-Config Machine\CAName]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-resubmit"></a>-erneut übermitteln

CertUtil [Optionen] - erneut übermitteln Anforderungs-ID

Ausstehende Anforderung erneut senden

[-Config Machine\CAName]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-setattributes"></a>-setattributes

CertUtil [Optionen] - Setattributes RequestId Attributzeichenfolge

Festlegen von Attributen für die ausstehende Anforderung

Anforderungs-ID – numerische Anforderungs-Id der ausstehenden Anforderung

Attributzeichenfolge – Fordern Sie Attributname-Wert-Paare an

- Namen und Werte sind Semikolons getrennt.
- Mehrere Name--Wert-Paare sind die Zeilenumbruchzeichen voneinander getrennt.
- Beispiel: "CertificateTemplate:User\nEMail:User@Domain.com"
- Jeder Sequenz "\n" wird in einem Newline-Trennzeichen konvertiert.

[-Config Machine\CAName]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-setextension"></a>-setextension

CertUtil [Options] -setextension RequestId ExtensionName Flags {Long | Date | String | @InFile}

Set-Erweiterung für die ausstehende Anforderung

Anforderungs-ID – numerische Anforderungs-Id über eine ausstehende Anforderung

ExtensionName: Objekt-ID-Zeichenfolge mit der Erweiterung

Flags: 0 wird empfohlen.  1 stellt die Erweiterung kritisch, 2 wird deaktiviert, 3 ist beides.

Wenn der letzte Parameter numerisch ist, wird diese als Long-Wert übernommen.

Wenn sie als Datum analysiert werden kann, wird es als Datum übernommen.

Wenn es anfängt, mit ' @', der Rest des Tokens ist der Dateiname, der binäre Daten oder eine Ascii-Text Hexdump enthält.

Alles wird als Zeichenfolge erstellt.

[-Config Machine\CAName]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-revoke"></a>-widerrufen

CertUtil [Optionen] - widerrufen SerialNumber [Reason]

Zertifikat widerrufen

SerialNumber: Durch Trennzeichen getrennte Liste mit Zertifikatsseriennummern widerrufen

Ursache: numerischen oder symbolischen Sperrungsgrund

- 0: CRL_REASON_UNSPECIFIED: Unbekannter (Standard)
- 1: CRL_REASON_KEY_COMPROMISE: Schlüsselgefährdung
- 2: CRL_REASON_CA_COMPROMISE: Stellengefährdung
- 3: CRL_REASON_AFFILIATION_CHANGED: Zuordnung geändert
- 4: CRL_REASON_SUPERSEDED: Abgelöst
- 5: CRL_REASON_CESSATION_OF_OPERATION: Beschäftigungsende
- 6: CRL_REASON_CERTIFICATE_HOLD: Zertifikat blockieren
- 8: CRL_REASON_REMOVE_FROM_CRL: Aus Sperrliste entfernen
- -1: Sperrung aufheben: Sperrung aufheben

[-Config Machine\CAName]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-isvalid"></a>-isvalid

CertUtil [Optionen]-"IsValid" SerialNumber | CertHash

Aktuelle Display-zertifikatverfügbarkeit

[-Config Machine\CAName]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-getconfig"></a>-getconfig

CertUtil [Optionen] - GetConfig zum Abrufen

Abrufen der Standard-Konfigurationszeichenfolge

[-Config Machine\CAName]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-ping"></a>-Ping

CertUtil [Optionen] - Ping [MaxSecondsToWait | CAMachineList]

Ping Active Directory Certificate Services anfordern-Schnittstelle

CAMachineList--CA durch Trennzeichen getrennte Computerliste

1. Verwenden Sie für einen einzelnen Computer ein abschließendes Komma
2. Zeigt die Standortkosten für jeden Computer der Zertifizierungsstelle an

[-Config Machine\CAName]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-cainfo"></a>-CAInfo

CertUtil [Optionen] - CAInfo [InfoName [Index | ErrorCode]]

Zertifizierungsstellen-Informationen anzeigen

InfoName – gibt an, die CA-Eigenschaft (siehe unten) angezeigt wird. Mit "\*" für alle Eigenschaften.

Index – optionaler nullbasierter Property-index

ErrorCode – numerischen Fehlercode.

[-f]. [-Teilen] [-Config Machine\CAName]

InfoName Argumentsyntax:

- Datei: Dateiversion
- Produkt: Produktversion
- exitcount: Modulanzahl beenden
- [Index] zu beenden: Modulbeschreibung beenden
- Richtlinie: Richtlinienbeschreibung-Modul
- Name: Name der Zertifizierungsstelle
- Sanitizedname: Sicheres ZS-name
- %dsname: Sicheres Zertifizierungsstelle Kurznamen (DS)
- Freigabeordner: Freigegebene Ordner
- error1 ErrorCode: Fehlermeldungstext
- error2 ErrorCode: Text der Fehlermeldung und der Fehlercode
- Typ: CA-Typ
- Info: CA-Informationen
- Übergeordnetes Element: Übergeordnete Zertifizierungsstelle
- Certcount: Die Anzahl der CA-Zertifikat
- xchgcount: Anzahl der Zertifizierungsstelle Exchange-Zertifikat
- Kracount: Die Anzahl der KRA-Zertifikat
- Kraused: KRA-Zertifikat verwendete Anzahl von
- propidmax: Maximum CA PropId
- Certstate [Index]: Zertifikat der Zertifizierungsstelle
- Certversion [Index]: CA-Cert-version
- Certstatuscode [Index]: Zertifikat der Zertifizierungsstelle den Status überprüfen
- Crlstate [Index]: CRL
- Krastate [Index]: KRA-Zertifikat
- Crossstate + [Index]: Vorwärts-Kreuzzertifikat
- Crossstate-[Index]: Rückwärts-Kreuzzertifikat
- CERT [Index]: Zertifikat der Zertifizierungsstelle
- Certchain [Index]: Zertifizierungsstellen-Zertifikatkette
- Certcrlchain [Index]: Zertifizierungsstellen-Zertifikatkette mit Zertifikatsperrlisten
- xchg [Index]: Exchange-Zertifikat
- Xchgchain [Index]: Zertifizierungsstellen-Zertifikatkette für exchange
- Xchgcrlchain [Index]: CA-Exchange-Zertifikatkette mit Zertifikatsperrlisten
- kra [Index]: KRA-Zertifikat
- Cross + [Index]: Vorwärts-Kreuzzertifikat
- Cross-[Index]: Rückwärts-Kreuzzertifikat
- CRL [Index]: Base CRL
- deltacrl [Index]: Delta CRL
- Crlstatus [Index]: Zertifikatsperrliste veröffentlichen, Status
- Deltacrlstatus [Index]: Status von Delta-CRL veröffentlichen
- DNS: DNS-Name
- Rolle: Rollentrennung
- anzeigen: Advanced Server
- Vorlagen: Vorlagen
- CSP [Index]: OCSP-URLs
- AIA [Index]: AIA-URLs
- CDP [Index]: CDP-URLs
- Localename: CA-Gebietsschema-Namen
- Subjecttemplateoids: Die Vorlage OIDs Betreff

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-cacert"></a>-ca.cert

CertUtil [Optionen] - ca.cert OutCACertFile [Index]

Abrufen des Zertifikats der Zertifizierungsstelle

OutCACertFile: Ausgabedatei

Index: CA-Zertifikat Erneuerungsindex (standardmäßig die letzte)

[-f]. [-Teilen] [-Config Machine\CAName]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-cachain"></a>-ca.chain

CertUtil [Optionen] - ca.chain OutCACertChainFile [Index]

Abrufen der ZS-Zertifikatkette

OutCACertChainFile: Ausgabedatei

Index: CA-Zertifikat Erneuerungsindex (standardmäßig die letzte)

[-f]. [-Teilen] [-Config Machine\CAName]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-getcrl"></a>-GetCRL

CertUtil [Optionen] - GetCRL OutFile [Index] [Delta]

Abrufen von Zertifikatsperrlisten

Index: Zertifikatsperrliste Index oder Schlüssel Index (Standardwert: für den neuesten Schlüssel CRL)

Delta: Delta-CRL (der Standardwert ist Basis-CRL)

[-f]. [-Teilen] [-Config Machine\CAName]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-crl"></a>-CRL

[Optionen]-CertUtil - CRL [tt: hh | erneut veröffentlichen] [Delta]

Veröffentlichen Sie neue CRLs [oder nur die Delta-CRLs]

tt: hh: neue Zertifikatsperrlisten-Gültigkeitsdauer in Tagen und Stunden

Erneutes Veröffentlichen – aktuellste Sperrlisten erneut veröffentlichen

Delta: nur die Delta-CRLs (der Standardwert ist Basis- und Delta-CRLs)

[-Teilen] [-Config Machine\CAName]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-shutdown"></a>-Herunterfahren

CertUtil [Optionen] - Herunterfahren

Herunterfahren von Active Directory-Zertifikatdienste

[-Config Machine\CAName]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-installcert"></a>-installCert

CertUtil [Optionen] - installCert ab [Zertifizierungsstellen-Zertifikatdatei]

Zertifikat der Zertifizierungsstelle installieren

[-f]. [-silent] [-Config Machine\CAName]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-renewcert"></a>-renewCert

CertUtil [Optionen] - RenewCert [Schlüssel wiederverwenden] [Machine\ParentCAName]

Zertifikat erneuern

Verwenden Sie -f, um eine ausstehende erneuerungsanforderung zu ignorieren, und generieren Sie eine neue Anforderung.

[-f]. [-silent] [-Config Machine\CAName]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-schema"></a>-schema

CertUtil [Optionen] - Schema [Ext | Attrib | ZERTIFIKATSPERRLISTE]

Dump Certificate-Schema

Der Standardwert ist-Anforderung und das Zertifikat-Tabelle

Ext: Erweiterungstabelle

Attrib: Attributtabelle

CRL: CRL-Tabelle

[-Teilen] [-Config Machine\CAName]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-view"></a>-Ansicht

CertUtil [Optionen] - Sicht [Warteschlange | Log | LogFail | Widerrufen | Ext | Attrib | Zertifikatsperrliste] [Csv]

Zertifikatsansicht

Warteschlange: Request-Warteschlange

Protokoll: Ausgestellte oder gesperrte Zertifikate und Anforderungen mit Fehlern

LogFail: Anforderungsfehler

Gesperrt: Widerrufene Zertifikate

Ext: Erweiterungstabelle

Attrib: Attributtabelle

CRL: CRL-Tabelle

csv: Ausgabe als Werte kommagetrennte

Zum Anzeigen der StatusCode-Spalte für alle Einträge:-Sie StatusCode

Zum Anzeigen aller Spalten für den letzten Eintrag:-einschränken "Anforderungs-ID == $"

Anforderungs-ID und die Löschung aus, die für die drei Anforderungen angezeigt werden soll:-einschränken "Anforderungs-ID > = 37, RequestId\<40"-out "Anforderungs-ID, Disposition"

Zum Anzeigen von Zeilen-Ids und die CRL-Zahlen für alle Basis-Zertifikatsperrlisten:-einschränken "CRLMinBase = 0"-out "CRLRowId, CRLNumber" Zertifikatsperrlisten

Zum Anzeigen von Basis-CRL Nummer 3: - V-einschränken "CRLMinBase = 0, CRLNumber = 3"-out "CRLRawCRL" Zertifikatsperrlisten

So zeigen Sie die gesamte Tabelle für die Zertifikatsperrliste an: CRL

Mit "Datum [+ |-tt: hh]" für die Date-Einschränkungen

Verwenden Sie "jetzt + TT: hh" für ein Datum in Bezug auf die aktuelle Uhrzeit

[-silent] [-Teilen] [-Config Machine\CAName] [-einschränken RestrictionList] [-out ColumnList]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-db"></a>-db

CertUtil [Optionen] - db

Raw-Datenbank sichern

[-Config Machine\CAName] [-einschränken RestrictionList] [-out ColumnList]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-deleterow"></a>Deleterow-

CertUtil [Optionen] - Deleterow RowId | Datum [Request | CERT | Ext | Attrib | ZERTIFIKATSPERRLISTE]

Server-Datenbank-Zeile löschen

Anforderung: Fehler und ausstehende Anforderungen (Sendedatum)

Cert: Abgelaufene und gesperrte Zertifikate (Ablaufdatum)

Ext: Erweiterungstabelle

Attrib: Attributtabelle

CRL: CRL-Tabelle (Ablaufdatum)

So löschen Sie die fehlgeschlagenen und ausstehende Anforderungen, die vom 22. Januar 2001 übermittelt werden: 1/22/2001 Anforderung

So löschen Sie alle Zertifikate, die abgelaufen am 22. Januar 2001: 1/22/2001 cert

So löschen Sie die zertifikatzeile, Attribute und Erweiterungen für RequestId 37: 37

Um Zertifikatsperrlisten zu löschen, die abgelaufen am 22. Januar 2001: 1/22/2001 CRL

[-f]. [-Config Machine\CAName]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-backup"></a>-backup

CertUtil [Optionen] - Sicherungsverzeichnis [inkrementelle] [KeepLog] sichern

Sicherung von Active Directory-Zertifikatdienste

Sicherungsverzeichnis: Verzeichnis zum Speichern von gesicherten Daten

Inkrementelle: Führen Sie nur inkrementelle Sicherung (Standardeinstellung ist für vollständige Sicherung)

KeepLog: Beibehalten der Protokolldateien der Datenbank (der Standardwert ist zum Abschneiden von Protokolldateien)

[-f]. [-Config Machine\CAName] [--p Kennwort]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-backupdb"></a>-backupDB

[Optionen]-CertUtil – BackupDB BackupDirectory [inkrementelle] [KeepLog]

Active Directory Certificate Services-Datenbank sichern

Sicherungsverzeichnis: Verzeichnis zum Speichern von gesichert wird, werden die Datenbankdateien

Inkrementelle: Führen Sie nur inkrementelle Sicherung (Standardeinstellung ist für vollständige Sicherung)

KeepLog: Beibehalten der Protokolldateien der Datenbank (der Standardwert ist zum Abschneiden von Protokolldateien)

[-f]. [-Config Machine\CAName]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-backupkey"></a>-backupKey

CertUtil [Optionen] – BackupKey BackupDirectory

Active Directory Certificate Services sicherungszertifikat und den privaten Schlüssel

Sicherungsverzeichnis: Verzeichnis zum Speichern von PFX-Datei gesichert

[-f]. [-Config Machine\CAName] [--p Kennwort] [-t Timeout]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-restore"></a>-Wiederherstellen

CertUtil [Optionen] - Sicherungsverzeichnis wiederherstellen

Wiederherstellen von Active Directory-Zertifikatdienste

Sicherungsverzeichnis: Verzeichnis, die Daten wiederhergestellt werden

[-f]. [-Config Machine\CAName] [--p Kennwort]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-restoredb"></a>-restoreDB

CertUtil [Optionen] - RestoreDB BackupDirectory

Wiederherstellen von Active Directory Certificate Services-Datenbank

Sicherungsverzeichnis: Verzeichnis, in die Datenbankdateien wiederhergestellt werden

[-f]. [-Config Machine\CAName]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-restorekey"></a>-restoreKey

CertUtil [Optionen] - RestoreKey BackupDirectory | PFX-Datei

Wiederherstellen von Active Directory Certificate Services, Zertifikaten und privaten Schlüsseln

Sicherungsverzeichnis:-Verzeichnis, die mit der PFX-Datei, die wiederhergestellt werden

PFX-Datei: PFX-Datei, die wiederhergestellt werden

[-f]. [-Config Machine\CAName] [--p Kennwort]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-importpfx"></a>-importPFX

[Optionen]-CertUtil - ImportPFX [Zertifikatspeichername] PFX-Datei [Modifizierer]

Importieren von Zertifikaten und privaten Schlüsseln

CertificateStoreName: Name des Zertifikatspeichers.  Finden Sie unter [-speichern](#-store).

PFX-Datei: PFX-Datei importiert werden

Modifizierer: Durch Trennzeichen getrennte Liste von mindestens einer der folgenden:

1. AT_SIGNATURE: Ändern Sie die Signatur KeySpec
2. AT_KEYEXCHANGE: Ändern Sie die KeySpec in den Schlüsselaustausch
3. NoExport: Machen Sie den privaten Schlüssel nicht exportiert
4. NoCert: Das Zertifikat nicht importieren
5. NoChain: Nicht im Rahmen der Zertifikatvertrauenskette importieren
6. NoRoot: Importieren Sie das Stammzertifikat nicht
7. Schützen: Schlüssel mit einem Kennwort schützen
8. NoProtect: Führen Sie kein Kennwort schützen Schlüssel

Der Standardwert ist privaten Computerspeicher.

[-f]. [-Benutzer] [--p Kennwort] [-Csp-Anbieter]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-dynamicfilelist"></a>-dynamicfilelist

CertUtil [Optionen] - dynamicfilelist

Dynamische Datei Liste anzuzeigen

[-Config Machine\CAName]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-databaselocations"></a>-databaselocations

CertUtil [Optionen] - databaselocations

Anzeigen von Datenbankspeicherorten

[-Config Machine\CAName]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-hashfile"></a>-hashfile

[Optionen]-CertUtil - Hashfile Eingabedatei [HashAlgorithm]

Generieren und Anzeigen von kryptografischen Hash über eine Datei

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-store"></a>– Speichern

CertUtil [Optionen]-[Zertifikatspeichername [CertId [Ausgabedatei]]] speichern

Dump-Zertifikatspeicher

CertificateStoreName: Name des Zertifikatspeichers. Beispiele:

- "My", "CA" (default), "Root",
- "Ldap: / / / CN Zertifizierungsstellen, CN = Public Key Services, CN = Services, CN = Configuration, DC = Cpandl, DC = com =? Zertifikat? eine?" objectClass "CertificationAuthority =" (Stammzertifikate anzeigen)
- "Ldap: / / / CN CAName, CN = Zertifizierungsstellen, CN = Public Key Services, CN = Services, CN = Configuration, DC = Cpandl, DC = com =? Zertifikat? Basis?" objectClass "CertificationAuthority =" (Ändern der Stammzertifikate)
- "Ldap: / / / CN CAName, CN = Computername, CN = CDP, CN = Public Key Services, CN = Services, CN = Configuration, DC = Cpandl, DC = = com? CertificateRevocationList? Basis?" objectClass "cRLDistributionPoint =" (Ansicht CRLs)
- "Ldap: / / / CN = NTAuthCertificates, CN = Public Key Services, CN = Services, CN = Configuration, DC Cpandl, DC = = com? Zertifikat? Basis?" objectClass "CertificationAuthority =" (Enterprise CA-Zertifikate)
- LDAP: (Zertifikate für AD-Computer-Objekt)
- -Benutzer-Ldap: (Zertifikate für AD-Benutzer-Objekt)

CertId: Das Zertifikat oder die CRL-Match-Token.  Kann es sich eine Seriennummer, einen SHA-1-Zertifikat, Zertifikatsperrlisten, CTL oder Hash für öffentliche Schlüssel, einen numerischen Cert-Index (0, 1, usw.), einen numerischen Index für die Zertifikatsperrlisten (. 0,.1 und So weiter), einen numerischen Index für die CTL (.. 0... 1, usw.), einen öffentlichen Schlüssel, Signatur oder Erweiterung Objekt-ID, einen Antragsteller des Zertifikats allgemeiner Name, eine e-Mail-Adresse, UPN oder DNS-Namen, einen Schlüsselcontainernamen oder CSP-Namen, einen Vorlagennamen oder Objekt-ID, ein EKU-Element oder Anwendung Richtlinien ObjectId oder einen Zertifikatsperrlisten-Aussteller allgemeiner Name. Viele dieser können dazu führen, dass mehrere Übereinstimmungen.

OutputFile:-Datei, um übereinstimmende Zertifikat zu speichern.

Verwenden Sie - Benutzer ein Benutzerspeichers ein Computerspeicher anstelle von den Zugriff auf.

Verwenden Sie - Unternehmen den Zugriff auf eine Computer-Enterprise-Store.

Verwenden Sie - Dienst auf einen Computer-Service-Speicher zugreifen.

Verwenden Sie - Grouppolicy auf einem Computer Group-Richtlinienspeicher.

Beispiele:

- -enterprise NTAuth
- -enterprise Root 37
- -user My 26e0aaaf000000000004
- ZERTIFIZIERUNGSSTELLE.11

[-f]. [– Enterprise] [-Benutzer] [-GroupPolicy] [-silent] [-Teilen] [-dc DCName]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-addstore"></a>-addstore

CertUtil [Optionen] - Addstore Zertifikatspeichername Eingabedatei

Hinzufügen des Zertifikats zum Speicher

CertificateStoreName: Name des Zertifikatspeichers.  Finden Sie unter [-speichern](#-store).

Eingabedatei: Zertifikat oder die CRL-Datei hinzufügen, um zu speichern.

[-f]. [– Enterprise] [-Benutzer] [-GroupPolicy] [-dc DCName]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-delstore"></a>-delstore

CertUtil [Optionen] - Delstore Zertifikatspeichername CertId

Zertifikat aus dem Speicher löschen

CertificateStoreName: Name des Zertifikatspeichers.  Finden Sie unter [-speichern](#-store).

CertId: Das Zertifikat oder die CRL-Match-Token.  Finden Sie unter [-speichern](#-store).

[– Enterprise] [-Benutzer] [-GroupPolicy] [-dc DCName]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-verifystore"></a>-verifystore

CertUtil [Optionen] - Verifystore Zertifikatspeichername [Zert.]

Überprüfen von Zertifikat im Speicher

CertificateStoreName: Name des Zertifikatspeichers.  Finden Sie unter [-speichern](#-store).

CertId: Das Zertifikat oder die CRL-Match-Token.  Finden Sie unter [-speichern](#-store).

[– Enterprise] [-Benutzer] [-GroupPolicy] [-silent] [-Teilen] [-dc DCName] [-t Timeout]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-repairstore"></a>– repairstore

CertUtil [Options] -repairstore CertificateStoreName CertIdList [PropertyInfFile | SDDLSecurityDescriptor]

Reparieren Sie wichtige Zuordnung und Aktualisieren von Eigenschaften oder Schlüssel die Sicherheitsbeschreibung von Zertifikat

CertificateStoreName: Name des Zertifikatspeichers.  Finden Sie unter [-speichern](#-store).

CertIdList: durch Trennzeichen getrennte Liste von Zertifikat- oder Match-Token. Finden Sie unter [-speichern](#-store) CertId-Beschreibung.

PropertyInfFile – INF-Datei, die Eigenschaften des externe enthält:

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

[-f]. [– Enterprise] [-Benutzer] [-GroupPolicy] [-silent] [-Teilen] [-Csp-Anbieter]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-viewstore"></a>-viewstore

[Optionen]-CertUtil - Viewstore [Zertifikatspeichername [CertId [Ausgabedatei]]]

Dump-Zertifikatspeicher

CertificateStoreName: Name des Zertifikatspeichers. Beispiele:

- "My", "CA" (default), "Root",
- "Ldap: / / / CN Zertifizierungsstellen, CN = Public Key Services, CN = Services, CN = Configuration, DC = Cpandl, DC = com =? Zertifikat? eine?" objectClass "CertificationAuthority =" (Stammzertifikate anzeigen)
- "Ldap: / / / CN CAName, CN = Zertifizierungsstellen, CN = Public Key Services, CN = Services, CN = Configuration, DC = Cpandl, DC = com =? Zertifikat? Basis?" objectClass "CertificationAuthority =" (Ändern der Stammzertifikate)
- "Ldap: / / / CN CAName, CN = Computername, CN = CDP, CN = Public Key Services, CN = Services, CN = Configuration, DC = Cpandl, DC = = com? CertificateRevocationList? Basis?" objectClass "cRLDistributionPoint =" (Ansicht CRLs)
- "Ldap: / / / CN = NTAuthCertificates, CN = Public Key Services, CN = Services, CN = Configuration, DC Cpandl, DC = = com? Zertifikat? Basis?" objectClass "CertificationAuthority =" (Enterprise CA-Zertifikate)
- LDAP: (Zertifikate für AD-Computer-Objekt)
- -Benutzer-Ldap: (Zertifikate für AD-Benutzer-Objekt)

CertId: Das Zertifikat oder die CRL-Match-Token. Kann es sich eine Seriennummer, einen SHA-1-Zertifikat, Zertifikatsperrlisten, CTL oder Hash für öffentliche Schlüssel, einen numerischen Cert-Index (0, 1, usw.), einen numerischen Index für die Zertifikatsperrlisten (. 0,.1 und So weiter), einen numerischen Index für die CTL (.. 0... 1, usw.), einen öffentlichen Schlüssel, Signatur oder Erweiterung Objekt-ID, einen Antragsteller des Zertifikats allgemeiner Name, eine e-Mail-Adresse, UPN oder DNS-Namen, einen Schlüsselcontainernamen oder CSP-Namen, einen Vorlagennamen oder Objekt-ID, ein EKU-Element oder Anwendung Richtlinien ObjectId oder einen Zertifikatsperrlisten-Aussteller allgemeiner Name. Viele dieser können dazu führen, dass mehrere Übereinstimmungen.

OutputFile:-Datei, um übereinstimmende Zertifikat zu speichern.

Verwenden Sie - Benutzer ein Benutzerspeichers ein Computerspeicher anstelle von den Zugriff auf.

Verwenden Sie - Unternehmen den Zugriff auf eine Computer-Enterprise-Store.

Verwenden Sie - Dienst auf einen Computer-Service-Speicher zugreifen.

Verwenden Sie - Grouppolicy auf einem Computer Group-Richtlinienspeicher.

Beispiele:

1. -enterprise NTAuth
2. -enterprise Root 37
3. -user My 26e0aaaf000000000004
4. ZERTIFIZIERUNGSSTELLE.11

[-f]. [– Enterprise] [-Benutzer] [-GroupPolicy] [-dc DCName]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-viewdelstore"></a>-viewdelstore

CertUtil [Optionen] - Viewdelstore [Zertifikatspeichername [CertId [Ausgabedatei]]]

Zertifikat aus dem Speicher löschen

CertificateStoreName: Name des Zertifikatspeichers. Beispiele:

- "My", "CA" (default), "Root",
- "Ldap: / / / CN Zertifizierungsstellen, CN = Public Key Services, CN = Services, CN = Configuration, DC = Cpandl, DC = com =? Zertifikat? eine?" objectClass "CertificationAuthority =" (Stammzertifikate anzeigen)
- "Ldap: / / / CN CAName, CN = Zertifizierungsstellen, CN = Public Key Services, CN = Services, CN = Configuration, DC = Cpandl, DC = com =? Zertifikat? Basis?" objectClass "CertificationAuthority =" (Ändern der Stammzertifikate)
- "Ldap: / / / CN CAName, CN = Computername, CN = CDP, CN = Public Key Services, CN = Services, CN = Configuration, DC = Cpandl, DC = = com? CertificateRevocationList? Basis?" objectClass "cRLDistributionPoint =" (Ansicht CRLs)
- "Ldap: / / / CN = NTAuthCertificates, CN = Public Key Services, CN = Services, CN = Configuration, DC Cpandl, DC = = com? Zertifikat? Basis?" objectClass "CertificationAuthority =" (Enterprise CA-Zertifikate)
- LDAP: (Zertifikate für AD-Computer-Objekt)
- -Benutzer-Ldap: (Zertifikate für AD-Benutzer-Objekt)

CertId: Das Zertifikat oder die CRL-Match-Token. Kann es sich eine Seriennummer, einen SHA-1-Zertifikat, Zertifikatsperrlisten, CTL oder Hash für öffentliche Schlüssel, einen numerischen Cert-Index (0, 1, usw.), einen numerischen Index für die Zertifikatsperrlisten (. 0,.1 und So weiter), einen numerischen Index für die CTL (.. 0... 1, usw.), einen öffentlichen Schlüssel, Signatur oder Erweiterung Objekt-ID, einen Antragsteller des Zertifikats allgemeiner Name, eine e-Mail-Adresse, UPN oder DNS-Namen, einen Schlüsselcontainernamen oder CSP-Namen, einen Vorlagennamen oder Objekt-ID, ein EKU-Element oder Anwendung Richtlinien ObjectId oder einen Zertifikatsperrlisten-Aussteller allgemeiner Name. Viele dieser können dazu führen, dass mehrere Übereinstimmungen.

OutputFile:-Datei, um übereinstimmende Zertifikat zu speichern.

Verwenden Sie - Benutzer ein Benutzerspeichers ein Computerspeicher anstelle von den Zugriff auf.

Verwenden Sie - Unternehmen den Zugriff auf eine Computer-Enterprise-Store.

Verwenden Sie - Dienst auf einen Computer-Service-Speicher zugreifen.

Verwenden Sie - Grouppolicy auf einem Computer Group-Richtlinienspeicher.

Beispiele:

1. -enterprise NTAuth
2. -enterprise Root 37
3. -user My 26e0aaaf000000000004
4. ZERTIFIZIERUNGSSTELLE.11

[-f]. [– Enterprise] [-Benutzer] [-GroupPolicy] [-dc DCName]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-dspublish"></a>-dsPublish

[Optionen]-CertUtil - DsPublish CertFile [NTAuthCA | Stammzertifizierungsstelle | SubCA | CrossCA | KRA | Benutzer | Computer]

[Optionen]-CertUtil - DsPublish CRLFile [DSCDPContainer [DSCDPCN]]

Zertifikat- oder in Active Directory veröffentlichen

Zertifikatdatei: Zertifikatdatei veröffentlichen

NTAuthCA: DS-Enterprise-Store Cert veröffentlichen

RootCA: Cert in DS vertrauenswürdigen Stammspeicher veröffentlichen

SubCA: Zertifikat der Zertifizierungsstelle in DS CA-Objekt veröffentlichen

CrossCA: Cross-Zertifikats in den DS-CA-Objekt veröffentlichen

KRA: Veröffentlichen von Cert DS Key Recovery Agent-Objekt

Benutzer: Cert auf Benutzer-DS-Objekt veröffentlichen

Computer: Cert-Computer-DS-Objekt veröffentlichen

CRLFile: CRL-Datei veröffentlichen

DSCDPContainer: CN, in der Regel den Zertifizierungsstellennamen Computer der DS-CDP-container

DSCDPCN: DS CDP Objekt CN, in der Regel auf Basis der kurzen Zertifizierungsstellennamen und Schlüsselindex

Verwenden Sie -f, um die DS-Objekt zu erstellen.

[-f]. [-Benutzer] [-dc DCName]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-adtemplate"></a>-ADTemplate

CertUtil [Optionen] - ADTemplate [Vorlagen]

Anzeigevorlagen AD

[-f]. [-Benutzer] [-Ut] [-Mt] [-dc DCName]

## <a name="-template"></a>-Vorlage

CertUtil [Optionen] - Vorlagen [Vorlagen]

Richtlinie für die Vorlagen anzeigen

[-f]. [-Benutzer] [-silent] [-PolicyServer URLOrId] [-Anonymous] [-Kerberos] [-ClientCertificate ClientCertId] [-Benutzername Benutzername] [--p Kennwort]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-templatecas"></a>-TemplateCAs

CertUtil [Optionen] TemplateCAs - Vorlage

Anzeigen von CAs für Vorlage

[-f]. [-Benutzer] [-dc DCName]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-catemplates"></a>-CATemplates

CertUtil [Optionen] – CATemplates [Vorlagen]

Vorlagen für Kanada anzuzeigen.

[-f]. [-Benutzer] [-Ut] [-Mt] [-Config Machine\CAName] [-dc DCName]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-setcasites"></a>-SetCASites

CertUtil [Optionen] - SetCASites [Set] [Websitename]

CertUtil [Optionen] - SetCASites überprüfen [Websitename]

CertUtil [Optionen] - SetCASites löschen

Festlegen, stellen Sie sicher oder Löschen von CA-Standortnamen

- Verwenden Sie die Option "- Config" als Ziel eine einzelne Zertifizierungsstelle (der Standardwert ist alle Zertifizierungsstellen)
- *SiteName* ist nur zulässig, wenn auf einer einzelnen Zertifizierungsstelle
- Verwenden Sie zum Überschreiben der Validierungsfehler für das angegebene-f *SiteName*
- Verwenden Sie -f, um alle Namen von CA-Website löschen

[-f]. [-Config Machine\CAName] [-dc DCName]

> [!NOTE]
> Weitere Informationen zum Konfigurieren von Zertifizierungsstellen, Active Directory Domain Services (AD DS) Awareness Site finden Sie unter [AD DS-Standortinformationen für AD CS- und PKI-Clients](https://social.technet.microsoft.com/wiki/contents/articles/14106.ad-ds-site-awareness-for-ad-cs-and-pki-clients.aspx).

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-enrollmentserverurl"></a>-enrollmentServerURL

CertUtil [Optionen] - EnrollmentServerURL [URL AuthenticationType [Priorität] [Modifizierer]]

CertUtil [Optionen] - EnrollmentServerURL URL löschen

Anzeigen, hinzufügen oder Löschen von einer Zertifizierungsstelle zugeordnete Registrierungs-Server-URLs

AuthenticationType: Geben Sie einen der folgenden Authentifizierungsmethoden aus Client beim Hinzufügen einer URL

1. Kerberos: Verwenden Sie Kerberos SSL-Anmeldeinformationen
2. Benutzername: Verwenden Sie benanntes Konto wird für SSL-Anmeldeinformationen.
3. ClientCertificate: X. 509-Zertifikats SSL-Anmeldeinformationen verwenden
4. Anonymous: Verwenden Sie anonyme Anmeldedaten für SSL

Löschen: Löscht die angegebene URL mit der Zertifizierungsstelle verknüpft ist

Priorität: der Standardwert ist "1", wenn nicht angegeben wird, wenn Sie eine URL hinzufügen

Modifizierer: Kommagetrennte Liste von mindestens einer der folgenden:

1. AllowRenewalsOnly: Nur erneuerungsanforderungen können an diese Zertifizierungsstelle über diese URL übermittelt werden
2. AllowKeyBasedRenewal: Ermöglicht die Verwendung eines Zertifikats, das über kein zugeordnetes Konto in AD verfügt. Dies gilt nur für ClientCertificate und AllowRenewalsOnly-Modus

[-Config Machine\CAName] [-dc DCName]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-adca"></a>-ADCA

CertUtil [Optionen] - ADCA [CAName]

Anzeigen von AD-Zertifizierungsstellen

[-f]. [-Teilen] [-dc DCName]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-ca"></a>-CA

CertUtil [Optionen] -CA [CAName | TemplateName]

Anzeigen der Registrierung Richtlinien-Zertifizierungsstellen

[-f]. [-Benutzer] [-silent] [-Teilen] [-PolicyServer URLOrId] [-Anonymous] [-Kerberos] [-ClientCertificate ClientCertId] [-Benutzername Benutzername] [--p Kennwort]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-policy"></a>-Policy

Anzeigen der Enrollment-Richtlinie

[-f]. [-Benutzer] [-silent] [-Teilen] [-PolicyServer URLOrId] [-Anonymous] [-Kerberos] [-ClientCertificate ClientCertId] [-Benutzername Benutzername] [--p Kennwort]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-policycache"></a>-PolicyCache

CertUtil [Optionen] - PolicyCache [löschen]

Anzeigen oder Löschen von Enrollment-Richtlinie Cacheeinträge

Löschen:-Richtlinienserver Einträge im Cache löschen

-f: verwenden -f, um alle Einträge im Cache zu löschen.

[-f]. [-Benutzer] [-PolicyServer URLOrId]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-credstore"></a>-CredStore

CertUtil [Optionen] - CredStore [URL]

CertUtil [Optionen] - CredStore URL hinzufügen

CertUtil [Optionen] - CredStore URL löschen

Anzeigen, hinzufügen oder Credential Store Einträge löschen

URL: Ziel-URL.  Verwendung \* entsprechend alle Einträge. Verwendung https://machine\* ein URL-Präfix entsprechend.

Fügen Sie hinzu: Fügen Sie eine Anmeldeinformationen-Store-Eintrag hinzu. SSL-Anmeldeinformationen müssen ebenfalls angegeben werden.

Löschen: Credential Store Einträge löschen

-f: verwenden -f, um einen Eintrag zu überschreiben oder Löschen mehrere Einträge.

[-f]. [-Benutzer] [-silent] [-Anonymous] [-Kerberos] [-ClientCertificate ClientCertId] [-Benutzername Benutzername] [--p Kennwort]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-installdefaulttemplates"></a>-InstallDefaultTemplates

[Optionen]-CertUtil – InstallDefaultTemplates

Installieren Sie Standardzertifikatvorlagen

[-dc DCName]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-urlcache"></a>-URLCache

[Optionen]-CertUtil - URLCache [URL | ZERTIFIKATSPERRLISTE | \* [delete]]

Zeigen Sie an oder löschen Sie Einträge für URL-cache

-URL: zwischengespeicherte URL

Zertifikatsperrliste:, die für alle zwischengespeicherten Zertifikatsperrliste URLs nur verwendet werden

\*: für alle zwischengespeicherten URLs verwendet werden

Löschen: Löschen von relevanten URLs aus dem lokalen Cache des aktuellen Benutzers

Verwenden Sie -f, um das Abrufen einer bestimmten URL, und Aktualisieren des Caches zu erzwingen.

[-f]. [-Teilen]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-pulse"></a>– Pulse

CertUtil [Optionen] - Impuls

Pulse-automatische Registrierung-Ereignisse

[-Benutzer]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-machineinfo"></a>-MachineInfo

CertUtil [Optionen] - MachineInfo DomainName\MachineName$

Anzeigen von Informationen in Active Directory-Computer-Objekt

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-dcinfo"></a>-DCInfo

CertUtil [Optionen] - DCInfo [Domain] [überprüfen | DeleteBad | DeleteAll]

Anzeigen von Informationen des Domänencontrollers

Standardmäßig werden Domänencontroller Zertifikaten ohne Überprüfung angezeigt.

[-f]. [-Benutzer] [-Urlfetch] [-dc DCName] [-t Timeout]

> [!TIP]
> Die Option zum Angeben einer Active Directory Domain Services (AD DS) Domäne **[Domain]** und an einem Domänencontroller ( **-dc**) wurde in Windows Server 2012 hinzugefügt. Den Befehl erfolgreich ausgeführt werden soll, müssen Sie ein Konto, das Mitglied ist verwenden **Domänen-Admins** oder **Organisations-Admins**. Die Änderungen Verhalten dieses Befehls lauten wie folgt aus:</br>> 1.  Wenn eine Domäne nicht angegeben ist und ein bestimmten Domänencontroller nicht angegeben ist, gibt diese Option eine Liste der Domänencontroller, auf dem Standarddomänencontroller verarbeiten.</br>> 2.  Wenn eine Domäne ist nicht angegeben, aber ein Domänencontroller angegeben ist, wird ein Bericht über die Zertifikate auf dem angegebenen Domänencontroller generiert.</br>> 3.  Wenn keine Domäne angegeben ist, aber ein Domänencontroller ist nicht angegeben, wird eine Liste der Domänencontroller und die Berichte für die Zertifikate für jeden Domänencontroller in der Liste generiert.</br>> 4.  Wenn die Domäne und Domänencontroller angegeben sind, wird eine Liste der Domänencontroller aus der entsprechenden Domänencontroller generiert. Ein Bericht über die Zertifikate für jeden Domänencontroller in der Liste wird auch generiert.

Nehmen wir beispielsweise an eine Domäne mit dem Namen CPANDL mit einem Domänencontroller mit dem Namen CPANDL-DC1 vorhanden ist. Sie können führen den folgenden Befehl Abrufen einer Liste von Domänencontrollern und ihre Zertifikate, die von CPANDL-DC1: Certutil -dc Cpandl-dc1 - Dcinfo Cpandl

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-entinfo"></a>-EntInfo

CertUtil [Optionen] - EntInfo DomainName\MachineName$

[-f]. [-Benutzer]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-tcainfo"></a>-TCAInfo

-TCAInfo CertUtil [Optionen] [DomainDN |-]

Zertifizierungsstellen-Informationen anzeigen

[-f]. [– Enterprise] [-Benutzer] [-Urlfetch] [-dc DCName] [-t Timeout]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-scinfo"></a>-SCInfo

CertUtil [Options] -SCInfo [ReaderName [CRYPT_DELETEKEYSET]]

Smartcard-Benutzerinformationen anzeigen

CRYPT_DELETEKEYSET: Alle Schlüssel auf der Smartcard löschen

[-silent] [-Teilen] [-Urlfetch] [-t Timeout]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-scroots"></a>-SCRoots

CertUtil [Optionen] - SCRoots aktualisieren [+] [InputRootFile] [ReaderName]

Speichern Sie die CertUtil [Optionen] - SCRoots @OutputRootFile [ReaderName]

CertUtil [Optionen] SCRoots - Sicht [InputRootFile | ReaderName]

CertUtil [Optionen] - SCRoots löschen [ReaderName]

Verwalten von Smartcard-Stammzertifikate

[-f]. [-Teilen] [--p Kennwort]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-verifykeys"></a>-verifykeys

CertUtil [Optionen] - Verifykeys [Schlüsselcontainername Zertifizierungsstellen-Zertifikatdatei]

Überprüfen Sie die öffentlichen/privaten Schlüsselsatz

Schlüsselcontainername: Schlüsselcontainer-Name des zu überprüfenden Schlüssels. Der Standardwert ist Computerschlüssel.  Verwenden Sie - Benutzer für Benutzerschlüssel.

Zertifizierungsstellen-Zertifikatdatei: Signierung oder Verschlüsselung Zertifikatdatei

Wenn keine Argumente angegeben werden, wird jede CA-Signaturzertifikat mit dem privaten Schlüssel überprüft.

Dieser Vorgang kann nur mit einer lokalen Zertifizierungsstelle oder lokalen Schlüssel ausgeführt werden.

[-f]. [-Benutzer] [-silent] [-Config Machine\CAName]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-verify"></a>-Überprüfen

CertUtil [Optionen] - CertFile überprüfen [ApplicationPolicyList |-[IssuancePolicyList]]

CertUtil [Optionen]-[Zertifizierungsstellen-Zertifikatdatei [CrossedCACertFile]]-CertFile überprüfen

CertUtil [Optionen] - Überprüfen Sie die Zertifizierungsstellen-CRLFile Zertifikatdatei [IssuedCertFile]

CertUtil [Optionen] - Überprüfen Sie die Zertifizierungsstellen-CRLFile Zertifikatdatei [DeltaCRLFile]

Stellen Sie sicher, Zertifikat, Zertifikatsperrlisten oder die Kette

CertFile: Zertifikat zum Überprüfen

ApplicationPolicyList: optionale durch Trennzeichen getrennte Liste der erforderlichen Anwendung Richtlinie ObjectIds

IssuancePolicyList: optionale durch Trennzeichen getrennte Liste der erforderlichen ObjectIds der Ausstellung-Richtlinie

Zertifizierungsstellen-Zertifikatdatei: optionale Ausstellungszertifikat der Zertifizierungsstelle überprüft werden soll

CrossedCACertFile: Optionales Zertifikat übergreifend zertifizierte von CertFile

CRLFile: Zertifikatsperrliste überprüfen

IssuedCertFile: optionale CRLFile abgedeckten ausgestelltes Zertifikat

DeltaCRLFile: optional delta CRL

Wenn ApplicationPolicyList angegeben wird, ist die kettenerstellung dieses auf Ketten für die angegebene Anwendungsrichtlinien gültig beschränkt.

Wenn IssuancePolicyList angegeben wird, ist die kettenerstellung dieses auf Ketten für die angegebene Ausstellungsrichtlinien gültig beschränkt.

Wenn Zertifizierungsstellen-Zertifikatdatei angegeben wird, werden die Felder in der Zertifizierungsstellen-Zertifikatdatei für CertFile oder CRLFile überprüft.

Wenn der Zertifizierungsstellen-Zertifikatdatei nicht angegeben ist, wird CertFile zum Erstellen und überprüfen eine vollständige Kette.

Wenn Zertifizierungsstellen-Zertifikatdatei und CrossedCACertFile angegeben sind, werden die Felder in den Zertifizierungsstellen-Zertifikatdatei und CrossedCACertFile für CertFile überprüft.

Wenn IssuedCertFile angegeben wird, werden die Felder im IssuedCertFile für CRLFile überprüft.

Wenn DeltaCRLFile angegeben wird, werden die Felder im DeltaCRLFile für CRLFile überprüft.

[-f]. [– Enterprise] [-Benutzer] [-silent] [-Teilen] [-Urlfetch] [-t Timeout]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-verifyctl"></a>-verifyCTL

CertUtil [Optionen] - VerifyCTL CTLObject [CertDir] [CertFile]

Stellen Sie sicher AuthRoot oder Unzulässiger Zertifikate CTL

CTLObject: Identifiziert die CTL, um zu überprüfen:

- AuthRootWU: Lesen Sie AuthRoot CAB-Datei und übereinstimmende Zertifikate aus dem URL-Cache. Verwenden Sie -f, um stattdessen von Windows Update herunterzuladen.
- DisallowedWU: Lesen Sie die Zertifikate CAB nicht zulässig, und es nicht erlaubt Zertifikatspeicher-Datei aus dem URL-Cache.  Verwenden Sie -f, um stattdessen von Windows Update herunterzuladen.
- AuthRoot: der schreibgeschützten Registrierung zwischengespeichert AuthRoot CTL.  Verwenden Sie mit der f#- und eine Zertifikatdatei, die nicht bereits als vertrauenswürdig eingestuft wird zum Erzwingen der Aktualisierung der Registrierung zwischengespeichert, AuthRoot und Zertifikat CTLs nicht zulässig.
- Nicht erlaubt: Lesen der Registrierung zwischengespeichert Zertifikate CTL nicht zulässig. -f weist das gleiche Verhalten wie bei AuthRoot.
- CTLFileName: Datei "oder" http: Pfad zur CTL oder CAB-Datei

CertDir: Dieser Ordner enthält Zertifikate, die übereinstimmende CTL-Einträge. Eine http: Ordnerpfad muss mit einem Pfadtrennzeichen enden. Wenn Sie ein Ordner mit AuthRoot oder nicht erlaubt nicht angegeben ist, mehrere Standorte durchsucht werden für den Abgleich von Zertifikaten: lokalen Zertifikatspeicher, crypt32.dll-Ressourcen und den lokalen Cache für die URL. Verwenden Sie zum Herunterladen von Windows Update bei Bedarf -f. Andernfalls wird standardmäßig auf den gleichen Ordner oder Website als die CTLObject.

Zertifikatdatei:-Datei, die mit der Zertifikate, um zu überprüfen. Zertifikate abgeglichen wird mit der CTL-Einträge, und die angezeigten Ergebnisse entsprechen. Unterdrückt die meisten der Standardausgabe.

[-f]. [-Benutzer] [-Teilen]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-sign"></a>– Anmeldung

CertUtil [Optionen] - InFileList anmelden | SerialNumber | CRL-OutFileList ["StartDate" + tt: hh] [+ Seriennummernliste | Seriennummernliste-| - Objektkennungsliste | @ExtensionFile]

CertUtil [Optionen] - InFileList anmelden | SerialNumber | Zertifikatsperrliste OutFileList [#HashAlgorithm] [+ AlternateSignatureAlgorithm | - AlternateSignatureAlgorithm]

Erneut signieren CRL oder ein Zertifikat

InFileList: durch Trennzeichen getrennte Liste von Zertifikat oder die CRL-Dateien zu ändern und erneut signieren

SerialNumber: Die Seriennummer des Zertifikats zu erstellen. Gültigkeitsdauer und andere Optionen dürfen nicht vorhanden sein.

CRL: Erstellen Sie eine leere CRL an. Gültigkeitsdauer und andere Optionen dürfen nicht vorhanden sein.

OutFileList: durch Trennzeichen getrennte Liste der geänderten Zertifikat oder die CRL-Ausgabedateien. Die Anzahl der Dateien muss InFileList übereinstimmen.

"StartDate" + tt: hh: neue Gültigkeitsdauer: optionale Datum plus; Optionale Tagen und Stunden Gültigkeitsdauer; Wenn beide angegeben werden, wird verwenden Sie eine Pluszeichen (+)-Trennzeichen. Verwenden Sie "jetzt [+ tt: hh]" zum aktuellen Zeitpunkt gestartet. "Never" verwenden Sie, damit kein Ablaufdatum (für nur CRLs).

Seriennummernliste: durch Trennzeichen getrennte Liste von Seriennummern hinzufügen oder entfernen

Objektkennungsliste: durch Trennzeichen getrennte ObjectId Erweiterungsliste entfernen

@ExtensionFile: INF-Datei, die mit Erweiterungen zur aktualisieren oder zu entfernen:

```
[Extensions]
     2.5.29.31 = ; Remove CRL Distribution Points extension
     2.5.29.15 = "{hex}" ; Update Key Usage extension
     _continue_="03 02 01 86"
```

HashAlgorithm: Name des Hashalgorithmus, ein #-Zeichen vorangestellt

AlternateSignatureAlgorithm: Alternative Signatur-Algorithmus-Spezifizierer

Ein Minuszeichen (-) bewirkt, dass die Seriennummer und Erweiterungen entfernt werden. Ein Pluszeichen (+) bewirkt, dass Seriennummern einer Zertifikatsperrliste hinzugefügt werden. Wenn Sie Elemente aus einer Zertifikatsperrliste zu entfernen, kann die Liste Seriennummern zu ObjectIds enthalten. Ein Minuszeichen (-) vor dem AlternateSignatureAlgorithm bewirkt, dass die ältere Signaturformat verwendet werden. Ein Pluszeichen (+) vor dem AlternateSignatureAlgorithm bewirkt, dass das Alternature Signaturformat verwendet werden. AlternateSignatureAlgorithm nicht angegeben haben, wird das Signaturformat in das Zertifikat oder die CRL verwendet.

[-Nullsign] [-f]. [-silent] [--Zertifikat-CertId]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-vroot"></a>-vroot

CertUtil [Optionen] - Vroot [löschen]

Erstellen/Löschen von virtuellen Stammverzeichnissen für Web und Dateifreigaben

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-vocsproot"></a>-vocsproot

CertUtil [Optionen] - Vocsproot [löschen]

Erstellen/Löschen von Web virtuelle Stammverzeichnisse für OCSP-Webproxy

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-addenrollmentserver"></a>-addEnrollmentServer

CertUtil [Options] -addEnrollmentServer Kerberos | UserName | ClientCertificate [AllowRenewalsOnly] [AllowKeyBasedRenewal]

Hinzufügen einer Anwendung Registrierungsserver

Fügen Sie eine Registrierung-Server-Anwendung und der Anwendungspool bei Bedarf für die angegebene Zertifizierungsstelle hinzu. Dieser Befehl installiert keine Binärdateien oder Pakete. Einer der folgenden Authentifizierungsmethoden mit denen der Client mit einem Zertifikat-Registrierung-Server verbunden.

- Kerberos: Verwenden Sie Kerberos SSL-Anmeldeinformationen
- Benutzername: Verwenden Sie benanntes Konto wird für SSL-Anmeldeinformationen.
- ClientCertificate: X. 509-Zertifikats SSL-Anmeldeinformationen verwenden
- AllowRenewalsOnly: Nur erneuerungsanforderungen können an diese Zertifizierungsstelle über diese URL übermittelt werden
- AllowKeyBasedRenewal – Ermöglicht die Verwendung eines Zertifikats, das über kein zugeordnetes Konto in AD verfügt. Dies gilt nur für ClientCertificate und AllowRenewalsOnly-Modus.

[-Config Machine\CAName]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-deleteenrollmentserver"></a>-deleteEnrollmentServer

CertUtil [Optionen] - DeleteEnrollmentServer Kerberos | Benutzername | ClientCertificate

Löschen einer Anwendung Registrierungsserver

Löschen Sie eine Registrierung-Server-Anwendung und der Anwendungspool bei Bedarf für die angegebene Zertifizierungsstelle. Mit diesem Befehl wird nicht auf Binärdateien oder Pakete entfernt. Einer der folgenden Authentifizierungsmethoden mit denen der Client mit einem Zertifikat-Registrierung-Server verbunden.

1. Kerberos: Verwenden Sie Kerberos SSL-Anmeldeinformationen
2. Benutzername: Verwenden Sie benanntes Konto wird für SSL-Anmeldeinformationen.
3. ClientCertificate: X. 509-Zertifikats SSL-Anmeldeinformationen verwenden

[-Config Machine\CAName]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-addpolicyserver"></a>-addPolicyServer

CertUtil [Optionen] - AddPolicyServer Kerberos | Benutzername | ClientCertificate [KeyBasedRenewal]

Hinzufügen einer Anwendung der Richtlinien-Server

Fügen Sie eine Richtlinie von Server-Anwendung und der Anwendungspool bei Bedarf. Dieser Befehl installiert keine Binärdateien oder Pakete. Eine der folgenden Authentifizierungsmethoden mit denen der Client die Verbindung mit einem Zertifikat-Policy-Server:

- Kerberos: Verwenden Sie Kerberos SSL-Anmeldeinformationen
- Benutzername: Verwenden Sie benanntes Konto wird für SSL-Anmeldeinformationen.
- ClientCertificate: X. 509-Zertifikats SSL-Anmeldeinformationen verwenden
- KeyBasedRenewal: Nur Richtlinien mit KeyBasedRenewal Vorlagen werden an den Client zurückgegeben. Dieses Flag gilt nur für Benutzernamen und ClientCertificate-Authentifizierung.

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-deletepolicyserver"></a>-deletePolicyServer

CertUtil [Options] -deletePolicyServer Kerberos | UserName | ClientCertificate [KeyBasedRenewal]

Löschen einer Richtlinie von Server-Anwendung

Löschen Sie eine Richtlinie von Server-Anwendung und den Anwendungspool aus, falls erforderlich. Mit diesem Befehl wird nicht auf Binärdateien oder Pakete entfernt. Eine der folgenden Authentifizierungsmethoden mit denen der Client die Verbindung mit einem Zertifikat-Policy-Server:

1. Kerberos: Verwenden Sie Kerberos SSL-Anmeldeinformationen
2. Benutzername: Verwenden Sie benanntes Konto wird für SSL-Anmeldeinformationen.
3. ClientCertificate: X. 509-Zertifikats SSL-Anmeldeinformationen verwenden
4. KeyBasedRenewal: Richtlinienserver KeyBasedRenewal

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-oid"></a>-oid

CertUtil [Options] -oid ObjectId [DisplayName | delete [LanguageId [Type]]]

Die Oid - GroupId CertUtil [Optionen]

CertUtil [Optionen] - Oid AlgId | AlgorithmName [GroupId]

Anzeigen von Objekt-ID oder Anzeigename festlegen

- ObjectId – ObjectId oder Anzeigenamen hinzufügen
- GroupId - Dezimalzahl GroupId für ObjectIds auflisten
- AlgId: hexadezimale AlgId für Objekt-ID nachschlagen
- AlgorithmName – Der Name des Algorithmus für zu suchende Objekt-ID
- DisplayName – Der Anzeigename zum Speichern in DS
- Löschen: Löschen von Anzeigenamen
- LanguageId – Sprach-Id (standardmäßig auf den aktuellen: 1033)
- Typ: DS Objekttyp erstellen: 1 für die Vorlage (Standard), 2 für Ausstellungsrichtlinie, 3 für die Richtlinie für die Anwendungen
- Verwenden Sie -f, um die DS-Objekt zu erstellen.

[-f]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-error"></a>-Fehler

CertUtil [Optionen] - Fehler ErrorCode

Meldungstext des Fehlers anzeigen

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-getreg"></a>-getreg

[Optionen]-CertUtil - Getreg [{Zertifizierungsstelle | wiederherstellen | Richtlinien | beenden | Vorlagen | registrieren | Kette | PolicyServers}\[ProgId\]] [reg.-Wertname]

Zeigt den Registrierungswert an

Zertifizierungsstelle: Registrierungsschlüssel für die Verwendung der Zertifizierungsstelle

Wiederherstellung: Verwenden der Zertifizierungsstelle wiederherstellen-Registrierungsschlüssel

Richtlinie: Verwenden des Richtlinienmoduls-Registrierungsschlüssel

Beenden: Verwendet zunächst Beenden des Moduls-Registrierungsschlüssel

Vorlage: Verwenden Sie Registrierungsschlüssel für die Vorlage (- Benutzer verwenden für Benutzervorlagen)

registrieren: Verwenden Sie Registrierungsschlüssel für die Registrierung (verwenden - Benutzer für den Benutzerkontext)

Kette: Verwenden Sie die Kette der Konfigurationsregistrierungsschlüssel

PolicyServers: Verwenden Sie Network Policy Server-Registrierungsschlüssel

ProgId: Verwenden Sie die Richtlinie oder beenden Sie des Moduls ProgId (Name des Registrierungsunterschlüssels)

REG.-Wertname: Name des Registrierungswerts (verwenden Sie "Name\*" um präfixübereinstimmung)

Wert: neue numerische, Zeichenfolgen- oder Datum Registrierungswert oder Dateiname. Wenn ein numerischer Wert mit beginnt "+" oder "-", die in den neuen Wert angegebenen Bits festgelegt sind, oder in den vorhandenen Registrierungswert deaktiviert.

Wenn ein Zeichenfolgenwert beginnt "+" oder "-", und der vorhandene Wert ist ein REG_MULTI_SZ-Wert, die Zeichenfolge hinzugefügt oder entfernt Sie aus der vorhandenen Registrierungswerts. Um die Erstellung eines Werts REG_MULTI_SZ zu erzwingen, fügen Sie eine "\n" am Ende der Zeichenfolgenwert hinzu.

Wenn der Wert beginnt "@", der Rest des Werts ist der Name der Datei mit der Darstellung hexadezimaler Text ist ein binärer Wert. Sofern sie nicht auf eine gültige Datei verwiesen wird, wird er stattdessen analysiert als [Date] [+ |-] [tt: hh]: ein optionaler Datum plus oder minus optional Tagen und Stunden. Wenn beide angegeben werden, verwenden Sie ein Pluszeichen (+) oder Minuszeichen (-) als Trennzeichen ein. Verwenden Sie "jetzt + TT: hh" für ein Datum in Bezug auf die aktuelle Uhrzeit an.

Mit "Chain\ChainCacheResyncFiletime @now" zwischengespeicherte CRLs effektiv zu leeren.

[-f]. [-Benutzer] [-GroupPolicy] [-Config Machine\CAName]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-setreg"></a>-setreg

[Optionen]-CertUtil - Setreg [{Zertifizierungsstelle | wiederherstellen | Richtlinien | beenden | Vorlagen | registrieren | Kette | PolicyServers}\[ProgId\]] reg.-Wertname Wert

Registrierungswert fest.

Zertifizierungsstelle: Registrierungsschlüssel für die Verwendung der Zertifizierungsstelle

Wiederherstellung: Verwenden der Zertifizierungsstelle wiederherstellen-Registrierungsschlüssel

Richtlinie: Verwenden des Richtlinienmoduls-Registrierungsschlüssel

Beenden: Verwendet zunächst Beenden des Moduls-Registrierungsschlüssel

Vorlage: Verwenden Sie Registrierungsschlüssel für die Vorlage (- Benutzer verwenden für Benutzervorlagen)

registrieren: Verwenden Sie Registrierungsschlüssel für die Registrierung (verwenden - Benutzer für den Benutzerkontext)

Kette: Verwenden Sie die Kette der Konfigurationsregistrierungsschlüssel

PolicyServers: Verwenden Sie Network Policy Server-Registrierungsschlüssel

ProgId: Verwenden Sie die Richtlinie oder beenden Sie des Moduls ProgId (Name des Registrierungsunterschlüssels)

REG.-Wertname: Name des Registrierungswerts (verwenden Sie "Name\*" um präfixübereinstimmung)

Wert: neue numerische, Zeichenfolgen- oder Datum Registrierungswert oder Dateiname. Wenn ein numerischer Wert mit beginnt "+" oder "-", die in den neuen Wert angegebenen Bits festgelegt sind, oder in den vorhandenen Registrierungswert deaktiviert.

Wenn ein Zeichenfolgenwert beginnt "+" oder "-", und der vorhandene Wert ist ein REG_MULTI_SZ-Wert, die Zeichenfolge hinzugefügt oder entfernt Sie aus der vorhandenen Registrierungswerts. Um die Erstellung eines Werts REG_MULTI_SZ zu erzwingen, fügen Sie eine "\n" am Ende der Zeichenfolgenwert hinzu.

Wenn der Wert beginnt "@", der Rest des Werts ist der Name der Datei mit der Darstellung hexadezimaler Text ist ein binärer Wert. Sofern sie nicht auf eine gültige Datei verwiesen wird, wird er stattdessen analysiert als [Date] [+ |-] [tt: hh]: ein optionaler Datum plus oder minus optional Tagen und Stunden. Wenn beide angegeben werden, verwenden Sie ein Pluszeichen (+) oder Minuszeichen (-) als Trennzeichen ein. Verwenden Sie "jetzt + TT: hh" für ein Datum in Bezug auf die aktuelle Uhrzeit an.

Mit "Chain\ChainCacheResyncFiletime @now" zwischengespeicherte CRLs effektiv zu leeren.

[-f]. [-Benutzer] [-GroupPolicy] [-Config Machine\CAName]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-delreg"></a>-delreg

-Delreg CertUtil [Optionen] [{ca | wiederherstellen | Richtlinie | beenden | Vorlagen | registrieren | Kette | PolicyServers}\[ProgId\]] [reg.-Wertname]

Registrierungswert löschen

Zertifizierungsstelle: Registrierungsschlüssel für die Verwendung der Zertifizierungsstelle

Wiederherstellung: Verwenden der Zertifizierungsstelle wiederherstellen-Registrierungsschlüssel

Richtlinie: Verwenden des Richtlinienmoduls-Registrierungsschlüssel

Beenden: Verwendet zunächst Beenden des Moduls-Registrierungsschlüssel

Vorlage: Verwenden Sie Registrierungsschlüssel für die Vorlage (- Benutzer verwenden für Benutzervorlagen)

registrieren: Verwenden Sie Registrierungsschlüssel für die Registrierung (verwenden - Benutzer für den Benutzerkontext)

Kette: Verwenden Sie die Kette der Konfigurationsregistrierungsschlüssel

PolicyServers: Verwenden Sie Network Policy Server-Registrierungsschlüssel

ProgId: Verwenden Sie die Richtlinie oder beenden Sie des Moduls ProgId (Name des Registrierungsunterschlüssels)

REG.-Wertname: Name des Registrierungswerts (verwenden Sie "Name\*" um präfixübereinstimmung)

Wert: neue numerische, Zeichenfolgen- oder Datum Registrierungswert oder Dateiname. Wenn ein numerischer Wert mit beginnt "+" oder "-", die in den neuen Wert angegebenen Bits festgelegt sind, oder in den vorhandenen Registrierungswert deaktiviert.

Wenn ein Zeichenfolgenwert beginnt "+" oder "-", und der vorhandene Wert ist ein REG_MULTI_SZ-Wert, die Zeichenfolge hinzugefügt oder entfernt Sie aus der vorhandenen Registrierungswerts. Um die Erstellung eines Werts REG_MULTI_SZ zu erzwingen, fügen Sie eine "\n" am Ende der Zeichenfolgenwert hinzu.

Wenn der Wert beginnt "@", der Rest des Werts ist der Name der Datei mit der Darstellung hexadezimaler Text ist ein binärer Wert. Sofern sie nicht auf eine gültige Datei verwiesen wird, wird er stattdessen analysiert als [Date] [+ |-] [tt: hh]: ein optionaler Datum plus oder minus optional Tagen und Stunden. Wenn beide angegeben werden, verwenden Sie ein Pluszeichen (+) oder Minuszeichen (-) als Trennzeichen ein. Verwenden Sie "jetzt + TT: hh" für ein Datum in Bezug auf die aktuelle Uhrzeit an.

Mit "Chain\ChainCacheResyncFiletime @now" zwischengespeicherte CRLs effektiv zu leeren.

[-f]. [-Benutzer] [-GroupPolicy] [-Config Machine\CAName]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-importkms"></a>-ImportKMS

CertUtil [Optionen] - ImportKMS BenutzerSchlüsselUndZertDatei [CertId]

Importieren von Benutzerschlüssel und Zertifikate in Server-Datenbank für die schlüsselarchivierung

BenutzerSchlüsselUndZertDatei--Datendatei, die Benutzer private Schlüssel und Zertifikate, die archiviert werden.  Dies kann eine der folgenden sein:

- Exportdatei Exchange Key Management Server (KMS)
- PFX-Datei

CertId: KMS exportieren Datei Entschlüsselung Übereinstimmung Zertifikatstoken.  Finden Sie unter [-speichern](#-store).

Verwenden Sie beim Importieren von Zertifikaten, die nicht von der Zertifizierungsstelle ausgestellten -f.

[-f]. [-silent] [-Teilen] [-Config Machine\CAName] [--p Kennwort] [-Symkeyalg SymmetricKeyAlgorithm [, KeyLength]]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-importcert"></a>-ImportCert

CertUtil [Optionen] ImportCert - Certfile [ExistingRow]

Importieren eines Zertifikats in die Datenbank

Verwenden Sie zum Importieren des Zertifikats anstelle eine ausstehende Anforderung für den gleichen Schlüssel ExistingRow.

Verwenden Sie beim Importieren von Zertifikaten, die nicht von der Zertifizierungsstelle ausgestellten -f.

Die Zertifizierungsstelle müssen möglicherweise auch zur Unterstützung von foreign Zertifikatimport konfiguriert werden: Certutil - Setreg Ca\KRAFlags + KRAF_ENABLEFOREIGN

[-f]. [-Config Machine\CAName]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-getkey"></a>-GetKey

CertUtil [Optionen] - GetKey Suchtoken [RecoveryBlobOutFile]

CertUtil [Optionen] - GetKey Suchtoken Skript OutputScriptFile

Abrufen von CertUtil [Optionen] - GetKey Suchtoken | OutputFileBaseName wiederherstellen

Archivierte Wiederherstellung von privaten Schlüsseln Blob abrufen, ein Wiederherstellungsskript zu generieren oder archivierte Schlüssel wiederherstellen

Skript: generiert ein Skript zum Abrufen und Wiederherstellen von Schlüsseln (Standardverhalten, wenn mehrere passende Recovery Kandidaten gefunden wurden, oder die Ausgabedatei ist nicht angegeben).

Abrufen von: Abrufen von ein oder mehrere Key Recovery Blobs (Standardverhalten, wenn genau eine übereinstimmende Recovery Kandidat gefunden wird und die angegebene Ausgabedatei ist)

Wiederherstellung: Abrufen und die Wiederherstellung privater Schlüssel in einem Schritt (erfordert Key Recovery Agent-Zertifikaten und privaten Schlüsseln)

SearchToken: Wird verwendet, um die Schlüssel und Zertifikate, die wiederhergestellt werden, auszuwählen.

Dabei kann es sich um eine der folgenden sein:

1. Allgemeine Name des Zertifikats
2. Seriennummer des Zertifikats
3. Zertifikat-SHA1-Hash (Fingerabdruck)
4. Zertifikat (Subject Key Identifier) KeyId SHA-1-hash
5. Name des Auftraggebers (Domäne\Benutzer)
6. UPN (user@domain)

RecoveryBlobOutFile:-Ausgabedatei mit einer Zertifikatkette und einen zugeordneten privaten Schlüssel, die weiterhin auf einem oder mehreren Key Recovery Agent-Zertifikaten verschlüsselt werden.

OutputScriptFile: der Ausgabedatei, die ein Batch-Skript zum Abrufen und Wiederherstellung von privaten Schlüssel enthält.

OutputFileBaseName: base Name der Ausgabedatei. Für abrufen eine beliebige Erweiterung abgeschnitten, und eine Zertifikat-spezifische Zeichenfolge und die Erweiterung .rec werden für jedes Blob schlüsselwiederherstellung angefügt.  Jede Datei enthält eine Zertifikatkette und einen zugeordneten privaten Schlüssel, die weiterhin auf einem oder mehreren Key Recovery Agent-Zertifikaten verschlüsselt. Zum Ausführen der Wiederherstellung eine beliebige Erweiterung abgeschnitten, und die P12-Erweiterung angefügt wird.  Enthält die wiederhergestellte Zertifikatketten und den zugehörigen privaten Schlüssel, die als PFX-Datei gespeichert.

[-f]. [-UnicodeText] [-silent] [-Config Machine\CAName] [--p Kennwort] [-ProtectTo SAMNameAndSIDList] [-Csp-Anbieter]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-recoverkey"></a>-RecoverKey

CertUtil [Optionen] - RecoverKey RecoveryBlobInFile [PFX-Ausgabedatei [RecipientIndex]]

Archivierten privaten Schlüssel wiederherstellen

[-f]. [-Benutzer] [-silent] [-Teilen] [--p Kennwort] [-ProtectTo SAMNameAndSIDList] [-Csp-Anbieter] [-t Timeout]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-mergepfx"></a>-MergePFX

CertUtil [Optionen] - MergePFX PFX-PFXEingabeDateiListe ["ExtendedProperties"] Ausgabedatei

PFXInFileList: Durch Trennzeichen getrennte Liste von PFX-Datei

PFXOutFile: PFX-Datei

ExtendedProperties: Erweiterten Eigenschaften mit einbeziehen

In der Befehlszeile angegebene Kennwort ist eine durch Trennzeichen getrennten Kennwort-Liste.  Wenn mehr als ein Kennwort angegeben ist, wird das letzte Kennwort für die Ausgabedatei verwendet.  Wenn nur ein Kennwort angegeben wird, oder wenn das letzte Kennwort ist "\*", der Benutzer wird aufgefordert werden, für das Dateikennwort Ausgabe.

[-f]. [-Benutzer] [-Teilen] [--p Kennwort] [-ProtectTo SAMNameAndSIDList] [-Csp-Anbieter]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="-convertepf"></a>-ConvertEPF

CertUtil [Optionen] - ConvertEPF PFXEingabeDateiListe EPFOutFile [Umwandlung | Cast-] [V3CACertId] [, Salt]

Konvertieren der PFX-Dateien in EPF-Datei

PFXInFileList: Durch Trennzeichen getrennte Liste von PFX-Datei

EPF: EPF-Ausgabedatei

Umwandlung: Verwenden Sie CAST 64-Verschlüsselung

CAST-: Verwenden Sie CAST 64-Verschlüsselung (Export)

V3CACertId: V3-CA-Zertifikat-Match-Token.  Finden Sie unter [-speichern](#-store) CertId-Beschreibung.

Salt-Wert: EPF ausgegebene Datei salt-Zeichenfolge

In der Befehlszeile angegebene Kennwort ist eine durch Trennzeichen getrennten Kennwort-Liste. Wenn mehr als ein Kennwort angegeben ist, wird das letzte Kennwort für die Ausgabedatei verwendet.  Wenn nur ein Kennwort angegeben wird, oder wenn das letzte Kennwort ist "\*", der Benutzer wird aufgefordert werden, für das Dateikennwort Ausgabe.

[-f]. [-silent] [-Teilen] [-dc DCName] [--p Kennwort] [-Csp-Anbieter]

Wechseln Sie zurück zur [Menü](#menu)

## <a name="options"></a>Optionen

Dieser Abschnitt definiert die Optionen, die Sie mit dem Befehl angeben können.

|Optionen|Beschreibung|
|-------|-----------|
|-nullsign|Verwenden Sie der Hash der Daten als Signatur.|
|-f|Erzwingt das Überschreiben|
|– Enterprise|Zertifikatspeicher des lokalen Computers Enterprise-Registrierung verwenden|
|-Benutzer|Verwenden Sie HKEY_CURRENT_USER-Schlüssel oder den Zertifikatspeicher|
|-GroupPolicy|Verwenden von Gruppenrichtlinien-Zertifikatspeicher|
|-Ut|Benutzervorlagen anzeigen|
|-mt|Anzeigen von Vorlagen für Computer|
|-Unicode-|Schreiben Sie umgeleiteten Ausgaben im Unicode-Format|
|-UnicodeText|Geschrieben Sie Ausgabedatei wird im Unicode-Format.|
|-gmt|Die Anzeigezeiten von GMT-Format|
|-Sekunden|Zeigt die Uhrzeit in Sekunden und Millisekunden|
|-Automatische|Einsetzen Sie automatische Flag, um Kryptografiekontext abzurufen.|
|-split|Teilen Sie die eingebetteten ASN. 1-Elemente und in Dateien speichern|
|-v|Ausführliche Vorgang|
|-privatekey|Anzeigen von Kennwort und privaten Schlüssel Daten|
|-PIN anheften|Smartcard-PIN|
|-urlfetch|Rufen Sie ab und überprüfen Sie Zertifikate für AIA und CDP-Zertifikatsperrliste|
|-Config Machine\CAName|Zeichenfolge-Zertifizierungsstelle und computer|
|-PolicyServer URLOrId|Richtlinien-URL oder -Id. Zur Auswahl U / I, - PolicyServer verwenden. Verwenden Sie für alle Policy Server - PolicyServer \*|
|-Anonym|Verwenden Sie anonyme Anmeldedaten für SSL|
|-Kerberos|Verwenden Sie Kerberos SSL-Anmeldeinformationen|
|ClientCertificate - ClientCertId|Verwenden Sie x. 509-Zertifikats SSL-Anmeldeinformationen. Zur Auswahl U / I, - ClientCertificate verwenden.|
|Benutzername - Benutzername|Verwenden Sie benanntes Konto wird für SSL-Anmeldeinformationen. Zur Auswahl U / I, - Benutzername verwendet.|
|-Zertifikat Cert-ID|Signaturzertifikat|
|-dc DCName|Ziel von einem bestimmten Domänencontroller|
|-RestrictionList einschränken|Durch Trennzeichen getrennte Liste der Einschränkung. Jeder Einschränkung besteht aus einem Spaltennamen, ein relationaler Operator und eine Konstante ganze Zahl, Zeichenfolge oder Datum. Ein Spaltenname kann ein Plus- oder Minuszeichen an der Sortierreihenfolge vorangestellt werden. Beispiele:</br>"RequestId = 47"</br>"+ RequesterName > = a, RequesterName < b"</br>"-RequesterName > DOMAIN, Disposition = 21"|
|-out ColumnList|Durch Trennzeichen getrennte Liste der Spalten|
|-p-Kennwort|Kennwort|
|-ProtectTo SAMNameAndSIDList|Durch Trennzeichen getrennte Liste der SAM-Name/der SID|
|-Csp-Anbieter|Anbieter|
|-t-Timeout|URL-Fetch-Timeout in Millisekunden|
|-symkeyalg SymmetricKeyAlgorithm[,KeyLength]|Name des Algorithmus für symmetrische Schlüssel mit einer optionalen Schlüssellänge, Beispiel: AES, 128 oder 3DES|

Wechseln Sie zurück zur [Menü](#menu)

## <a name="additional-certutil-examples"></a>Zusätzliche Certutil-Beispiele

Einige Beispiele zur Verwendung mit diesem Befehl finden Sie unter

1. [Certutil-Beispiele für die Verwaltung von Active Directory-Zertifikatdienste (AD CS) über die Befehlszeile](https://social.technet.microsoft.com/wiki/contents/articles/3063.certutil-examples-for-managing-active-directory-certificate-services-ad-cs-from-the-command-line.aspx)
2. [Aufgaben von Certutil zum Verwalten von Zertifikaten](https://technet.microsoft.com/library/cc772898.aspx)
3. [Binäre Anforderung exportieren, die mit der exemplarischen Vorgehensweise CertUtil.exe-Befehlszeilentool](https://social.technet.microsoft.com/wiki/contents/articles/7573.active-directory-certificate-services-pki-key-archival-and-management.aspx)
4. [Stamm-CA-Zertifikat erneuern](https://social.technet.microsoft.com/wiki/contents/articles/2016.root-ca-certificate-renewal.aspx)
5. [Certutil](https://msdn.microsoft.com/subscriptions/cc773087.aspx)

Wechseln Sie zurück zur [Menü](#menu)
