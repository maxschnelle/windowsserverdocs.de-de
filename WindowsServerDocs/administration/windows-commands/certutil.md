---
title: certutil
description: Referenz Artikel für den certutil-Befehl, bei dem es sich um ein Befehlszeilenprogramm handelt, das die Konfigurationsinformationen der Zertifizierungsstelle absichert und anzeigt, Zertifikat Dienste konfiguriert, Zertifizierungsstellen-und Wiederherstellungs Zertifizierungsstellen-Komponenten konfiguriert und Zertifikate, Schlüsselpaare und Zertifikat Ketten überprüft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c264ccf0-ba1e-412b-9dd3-d77dd9345ad9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 159a3d2eb54d6a3040c4a22864a1c90e16bf2247
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86955332"
---
# <a name="certutil"></a>certutil

Certutil.exe ist ein Befehlszeilenprogramm, das als Teil der Zertifikat Dienste installiert ist. Sie können certutil.exe zum Sichern und Anzeigen von Konfigurationsinformationen von Zertifizierungsstellen (Certification Authority, ca), zum Konfigurieren von Zertifikat Diensten, zum Sichern und Wiederherstellen von Zertifizierungsstellen Komponenten und zum Überprüfen von Zertifikaten, Schlüsselpaaren und Zertifikat Ketten verwenden.

Wenn certutil auf einer Zertifizierungsstelle ohne zusätzliche Parameter ausgeführt wird, wird die aktuelle Zertifizierungsstellen Konfiguration angezeigt. Wenn certutil auf einer nicht Zertifizierungsstelle ausgeführt wird, wird standardmäßig der `certutil [-dump]` Befehl ausgeführt.

> [!IMPORTANT]
> Frühere Versionen von certutil bieten möglicherweise nicht alle Optionen, die in diesem Dokument beschrieben werden. Sie können alle Optionen anzeigen, die eine bestimmte Version von certutil bereitstellt, indem Sie `certutil -?` oder Ausführen `certutil <parameter> -?` .

## <a name="parameters"></a>Parameter

### <a name="-dump"></a>-Dump

Sichern Sie Konfigurationsinformationen oder Dateien.

```
certutil [options] [-dump]
certutil [options] [-dump] file
```

```
[-f] [-silent] [-split] [-p password] [-t timeout]
```

### <a name="-asn"></a>-ASN

Analysieren Sie die Datei ASN. 1.

```
certutil [options] -asn file [type]
```

`[type]`: numeric CRYPT_STRING_ *-decodetyp

### <a name="-decodehex"></a>-decodehex

Decodieren einer hexadezimal codierten Datei.

```
certutil [options] -decodehex infile outfile [type]
```

`[type]`: numeric CRYPT_STRING_ *-Codierungstyp

```
[-f]
```

### <a name="-decode"></a>-Decodieren

Decodieren einer Base64-codierten Datei.

```
certutil [options] -decode infile outfile
```

```
[-f]
```

### <a name="-encode"></a>-Codieren

Codieren einer Datei in base64.

```
certutil [options] -encode infile outfile
```

```
[-f] [-unicodetext]
```

### <a name="-deny"></a>-verweigern

Ablehnen einer ausstehenden Anforderung.

```
certutil [options] -deny requestID
```

```
[-config Machine\CAName]
```

### <a name="-resubmit"></a>-erneut übermitteln

Übermitteln Sie eine ausstehende Anforderung erneut.

```
certutil [options] -resubmit requestId
```

```
[-config Machine\CAName]
```

### <a name="-setattributes"></a>-----Tributes

Legen Sie Attribute für eine ausstehende Zertifikat Anforderung fest.

```
certutil [options] -setattributes RequestID attributestring
```

Hierbei gilt:

- **RequestId** ist die numerische Anforderungs-ID für die ausstehende Anforderung.

- **AttributeString** ist das Name-Wert-Paar des Anforderungs Attributs.

```
[-config Machine\CAName]
```

#### <a name="remarks"></a>Bemerkungen

- Namen und Werte müssen durch Doppelpunkte getrennt sein, während mehrere Name-Wert-Paare zeilenweise getrennt sein müssen. Beispiel: `CertificateTemplate:User\nEMail:User@Domain.com` `\n` gibt an, wo die Sequenz in ein Zeilen Trennzeichen konvertiert wird.

### <a name="-setextension"></a>-abtextension

Legen Sie eine Erweiterung für eine ausstehende Zertifikat Anforderung fest.

```
certutil [options] -setextension requestID extensionname flags {long | date | string | \@infile}
```

Hierbei gilt:

- **RequestId** ist die numerische Anforderungs-ID für die ausstehende Anforderung.

- **ExtensionName** ist die ObjectID-Zeichenfolge für die Erweiterung.

- **Flags** legt die Priorität der Erweiterung fest. `0`wird empfohlen, während `1` die Erweiterung auf kritisch festlegt, `2` die Erweiterung deaktiviert und beides bewirkt `3` .

```
[-config Machine\CAName]
```

#### <a name="remarks"></a>Bemerkungen

- Wenn der letzte Parameter numerisch ist, wird er als **Long**-Wert angenommen.

- Wenn der letzte Parameter als Datum analysiert werden kann, wird er als **Datum**angenommen.

- Wenn der letzte Parameter mit beginnt `\@` , wird der Rest des Tokens als Dateiname mit Binärdaten oder einem ASCII-Text-hexadezimal Abbild entnommen.

- Wenn der letzte Parameter etwas anderes ist, wird er als Zeichenfolge verwendet.

### <a name="-revoke"></a>-widerrufen

Widerrufen eines Zertifikats.

```
certutil [options] -revoke serialnumber [reason]
```

Hierbei gilt:

- **serialNumber** ist eine durch Trennzeichen getrennte Liste von Zertifikat Seriennummern, die widerrufen werden sollen.

- der **Grund** ist die numerische oder symbolische Darstellung des Sperr Grunds, einschließlich:

  - **0. CRL_REASON_UNSPECIFIED** nicht angegeben (Standard)

  - **1. CRL_REASON_KEY_COMPROMISE** schlüsselkompromittierung

  - **2.** Gefährdung der CRL_REASON_CA_COMPROMISE Zertifizierungsstelle

  - **3. CRL_REASON_AFFILIATION_CHANGED** Zugehörigkeit geändert

  - **4. CRL_REASON_SUPERSEDED** abgelöst

  - **5. CRL_REASON_CESSATION_OF_OPERATION** Beendigung des Vorgangs

  - **6. CRL_REASON_CERTIFICATE_HOLD** -Zertifikat Aufbewahrung

  - **8. CRL_REASON_REMOVE_FROM_CRL** -aus CRL entfernen

  - **1. aufheben** der Sperrung aufheben

```
[-config Machine\CAName]
```

### <a name="-isvalid"></a>-IsValid

Zeigt die Disposition des aktuellen Zertifikats an.

```
certutil [options] -isvalid serialnumber | certhash
```

```
[-config Machine\CAName]
```

### <a name="-getconfig"></a>-GetConfig

Standard Konfigurations Zeichenfolge erhalten.

```
certutil [options] -getconfig
```

```
[-config Machine\CAName]
```

### <a name="-ping"></a>-Ping

Versuchen Sie, die Anforderungs Schnittstelle der Active Directory Zertifikat Dienste zu kontaktieren.

```
certutil [options] -ping [maxsecondstowait | camachinelist]
```

Hierbei gilt:

- **camachinelist** eine durch Trennzeichen getrennte Liste von Zertifizierungsstellen-Computernamen. Verwenden Sie für einen einzelnen Computer ein abschließendes Komma. Mit dieser Option werden auch die Standortkosten für die einzelnen Zertifizierungsstellen Computer angezeigt.

```
[-config Machine\CAName]
```

### <a name="-cainfo"></a>-cainfo

Anzeigen von Informationen zur Zertifizierungsstelle.

```
certutil [options] -cainfo [infoname [index | errorcode]]
```

Hierbei gilt:

- **Infoname** gibt die anzuzeigende ZS-Eigenschaft basierend auf der folgenden Syntax für das Infoname-Argument an:

  - **Datei** Dateiversion

  - **Produkt** -Produktversion

  - **exitcount** -Beendigungs Modul Anzahl

  - **Beenden `[index]` ** -Modulbeschreibung beenden

  - Beschreibung des **Richtlinien** Richtlinien Moduls

  - **Name** : Zertifizierungsstellen Name

  - **bertizedname** -Name der Zertifizierungsstelle

  - **dsname** -der kurze Name der Zertifizierungsstelle (DS-Name)

  - **Freigabe Ordner** : frei gegebener Ordner

  - **Error1 ErrorCode** -Fehlermeldungs Text

  - **error2 ErrorCode** -Fehlermeldungs Text und Fehlercode

  - **Type** -ca-Typ

  - **Info** -ca-Informationen

  - über **geordnete** übergeordnete Zertifizierungsstelle

  - **certcount** -ca-CERT-Anzahl

  - **xchgcount** -ca Exchange-Zertifikat Anzahl

  - **kracount** -Kra-CERT-Anzahl

  - **kraused** -Kra-Anzahl verwendeter Zertifikate

  - **propidmax** -maximale Zertifizierungsstellen-PROPID

  - **certstate `[index]` ** -Zertifizierungsstellen Zertifikat

  - **certversion `[index]` ** -Zertifizierungsstellen-CERT-Version

  - **certstatus Code `[index]` ** -CA CERT Verify-Status

  - **crlstate `[index]` ** -CRL

  - **krastate `[index]` ** -Kra CERT

  - **crossstate + `[index]` ** -Weiterleiten-Kreuz Zertifikat

  - **crossstate- `[index]` ** -Abwärts Kreuz Zertifikat

  - **Zertifikat `[index]` ** -Zertifizierungsstellen Zertifikat

  - **certchain `[index]` ** -Zertifizierungsstellen-Zertifikat Kette

  - **certcrlchain `[index]` ** -Zertifizierungsstellen-Zertifikat Kette mit CRLs

  - **xchg `[index]` ** -CA Exchange-Zertifikat

  - **xchgchain `[index]` ** -CA Exchange-Zertifikat Kette

  - **xchgcrlchain `[index]` ** -CA Exchange-Zertifikat Kette mit CRLs

  - **Kra `[index]` ** -Kra CERT

  - **Kreuz + `[index]` ** -Weiterleiten-Kreuz Zertifikat

  - **Kreuz `[index]` ** -Abwärts Kreuz Zertifikat

  - **CRL `[index]` ** -Basis-CRL

  - **Delta `[index]` ** - -Delta-CRL

  - **crlstatus `[index]` ** -CRL-Veröffentlichungs Status

  - **Delta-Status `[index]` ** -Status der Delta-CRL-Veröffentlichung

  - **DNS** -DNS-Name

  - **Rollen** Rollen Trennung

  - **ADS** -Advanced Server

  - **Vorlagen** -Vorlagen

  - **CSP `[index]` ** -OCSP-URLs

  - **AIA `[index]` ** -AIA-URLs

  - **CDP `[index]` ** -CDP-URLs

  - **localename** -ca-Gebiets Schema Name

  - **subjettemplateoids** -Subjekt Vorlage OIDs

  - **&#42;** : zeigt alle Eigenschaften an.

- **Index** ist der optionale null basierte Eigenschafts Index.

- **errorCode** ist der numerische Fehlercode.

```
[-f] [-split] [-config Machine\CAName]
```

### <a name="-cacert"></a>-ca. cert

Rufen Sie das Zertifikat für die Zertifizierungsstelle ab.

```
certutil [options] -ca.cert outcacertfile [index]
```

Hierbei gilt:

- **outcacertfile** ist die Ausgabedatei.

- der **Index** ist der Zertifizierungsstellen-Zertifikat Erneuerungs Index (standardmäßig der aktuellste).

```
[-f] [-split] [-config Machine\CAName]
```

### <a name="-cachain"></a>-ca. Chain

Rufen Sie die Zertifikat Kette für die Zertifizierungsstelle ab.

```
certutil [options] -ca.chain outcacertchainfile [index]
```

Hierbei gilt:

- **outcacertchainfile** ist die Ausgabedatei.

- der **Index** ist der Zertifizierungsstellen-Zertifikat Erneuerungs Index (standardmäßig der aktuellste).

```
[-f] [-split] [-config Machine\CAName]
```

### <a name="-getcrl"></a>-getcrl

Ruft eine Zertifikat Sperr Liste (CRL) ab.

certutil [Optionen]-getcrl outfile [index] [Delta]

Hierbei gilt:

- **Index** ist der CRL-Index oder Schlüssel Index (Standardmäßig ist CRL für den neuesten Schlüssel).

- **Delta** ist die Delta-CRL (Standardwert ist Basis-CRL).

```
[-f] [-split] [-config Machine\CAName]
```

### <a name="-crl"></a>-CRL

Veröffentlichen Sie neue Zertifikat Sperr Listen (CRLs) oder Delta-CRLs.

```
certutil [options] -crl [dd:hh | republish] [delta]
```

Hierbei gilt:

- **DD: hh** ist die neue Gültigkeitsdauer der Zertifikat Sperr Liste in Tagen und Stunden.

- **erneut** veröffentlichen veröffentlicht die neuesten CRLs.

- **Delta** veröffentlicht nur die Delta-CRLs (der Standardwert ist Basis-und Delta-CRLs).

```
[-split] [-config Machine\CAName]
```

### <a name="-shutdown"></a>-Herunterfahren

Fährt die Active Directory Zertifikat Dienste herunter.

```
certutil [options] -shutdown
```

```
[-config Machine\CAName]
```

### <a name="-installcert"></a>-installCert

Installiert ein Zertifizierungsstellen Zertifikat.

```
certutil [options] -installcert [cacertfile]
```

```
[-f] [-silent] [-config Machine\CAName]
```

### <a name="-renewcert"></a>-verläncert

Erneuert ein Zertifizierungsstellen Zertifikat.

```
certutil [options] -renewcert [reusekeys] [Machine\ParentCAName]
```

- Verwenden `-f` Sie, um eine ausstehende Erneuerungs Anforderung zu ignorieren und eine neue Anforderung zu generieren.

```
[-f] [-silent] [-config Machine\CAName]
```

### <a name="-schema"></a>-Schema

Sichert das Schema für das Zertifikat.

```
certutil [options] -schema [ext | attrib | cRL]
```
Hierbei gilt:

- Der Befehl verwendet standardmäßig die Anforderungs-und Zertifikat Tabelle.

- **ext** ist die Erweiterungs Tabelle.

- **Attribut** ist die Attribut Tabelle.

- die **CRL** ist die CRL-Tabelle.

```
[-split] [-config Machine\CAName]
```

### <a name="-view"></a>-Ansicht

Sichert die Zertifikat Ansicht.

```
certutil [options] -view [queue | log | logfail | revoked | ext | attrib | crl] [csv]
```

Hierbei gilt:

- **Queue** sichert eine bestimmte Anforderungs Warteschlange.

- **Protokoll** sichert die ausgestellten oder gesperrten Zertifikate sowie alle fehlgeschlagenen Anforderungen.

- **logfail** sichert die fehlgeschlagenen Anforderungen.

- **widerrufene** Zertifikate rufen die gesperrten Zertifikate ab.

- **ext** sichert die Erweiterungs Tabelle.

- Das **Attribut** sichert die Attribut Tabelle.

- die **CRL** sichert die CRL-Tabelle.

- **CSV** stellt die Ausgabe mit durch Trennzeichen getrennten Werten bereit.

```
[-silent] [-split] [-config Machine\CAName] [-restrict RestrictionList] [-out ColumnList]
```

#### <a name="remarks"></a>Bemerkungen

- Wenn Sie die Spalte **Statuscode** für alle Einträge anzeigen möchten, geben Sie ein.`-out StatusCode`

- Wenn Sie alle Spalten für den letzten Eintrag anzeigen möchten, geben Sie Folgendes ein:`-restrict RequestId==$`

- Geben Sie Folgendes ein, um die **RequestId** und **Disposition** für drei Anforderungen anzuzeigen:`-restrict requestID>37,requestID<40 -out requestID,disposition`

- Geben Sie Folgendes ein, um Zeilen-**IDs** und **CRL-Nummern** für Zeilen-IDs für alle Basis Sperr Listen anzuzeigen:`-restrict crlminbase=0 -out crlrowID,crlnumber crl`

- Geben Sie zum Anzeigen von Folgendes ein:`-v -restrict crlminbase=0,crlnumber=3 -out crlrawcrl crl`

- Geben Sie Folgendes ein, um die gesamte CRL-Tabelle anzuzeigen:`CRL`

- Verwenden Sie `Date[+|-dd:hh]` für Datums Einschränkungen.

- Verwenden `now+dd:hh` Sie für ein Datum in Bezug auf die aktuelle Zeit.

### <a name="-db"></a>-db

Sichert die Rohdatenbank.

```
certutil [options] -db
```

```
[-config Machine\CAName] [-restrict RestrictionList] [-out ColumnList]
```

### <a name="-deleterow"></a>-deleteRow

Löscht eine Zeile aus der Server Datenbank.

```
certutil [options] -deleterow rowID | date [request | cert | ext | attrib | crl]
```

Hierbei gilt:

- die **Anforderung** löscht die fehlgeschlagenen und ausstehenden Anforderungen auf der Grundlage des Übermittlungs Datums.

- **CERT** löscht abgelaufene und widerrufene Zertifikate basierend auf dem Ablaufdatum.

- **ext** löscht die Erweiterungs Tabelle.

- Das **Attribut** löscht die Attribut Tabelle.

- **CRL** löscht die CRL-Tabelle.

```
[-f] [-config Machine\CAName]
```

#### <a name="examples"></a>Beispiele

- Geben Sie Folgendes ein, um fehlerhafte und ausstehende Anforderungen zu löschen, die vom 22. Januar 2001`1/22/2001 request`

- Geben Sie Folgendes ein, um alle Zertifikate zu löschen, die bis zum 22. Januar 2001 ablaufen:`1/22/2001 cert`

- Geben Sie Folgendes ein, um die Zertifikat Zeile, Attribute und Erweiterungen für RequestId 37 zu löschen:`37`

- Zum Löschen von CRLs, die bis zum 22. Januar 2001 ablaufen, geben Sie Folgendes ein:`1/22/2001 crl`

### <a name="-backup"></a>-backup

Sichert die Active Directory Zertifikat Dienste.

```
certutil [options] -backup backupdirectory [incremental] [keeplog]
```

Hierbei gilt:

- **Backup Directory** ist das Verzeichnis, in dem die gesicherten Daten gespeichert werden.

- die **inkrementelle** Sicherung führt nur eine inkrementelle Sicherung durch

- **keeplog** behält die Protokolldateien der Datenbank bei (Standardmäßig werden Protokolldateien gekürzt).

```
[-f] [-config Machine\CAName] [-p Password]
```

### <a name="-backupdb"></a>-backupDB

Sichert die Active Directory Zertifikat Dienst-Datenbank.

```
certutil [options] -backupdb backupdirectory [incremental] [keeplog]
```

Hierbei gilt:

- **Backup Directory** ist das Verzeichnis, in dem die gesicherten Datenbankdateien gespeichert werden.

- die **inkrementelle** Sicherung führt nur eine inkrementelle Sicherung durch

- **keeplog** behält die Protokolldateien der Datenbank bei (Standardmäßig werden Protokolldateien gekürzt).

```
[-f] [-config Machine\CAName]
```

### <a name="-backupkey"></a>-backupkey

Sichert das Zertifikat für die Active Directory Zertifikat Dienste und den privaten Schlüssel.

```
certutil [options] -backupkey backupdirectory
```

Hierbei gilt:

- **Backup Directory** ist das Verzeichnis, in dem die gesicherte PFX-Datei gespeichert wird.

```
[-f] [-config Machine\CAName] [-p password] [-t timeout]
```

### <a name="-restore"></a>-restore

Stellt die Active Directory Zertifikat Dienste wieder her.

```
certutil [options] -restore backupdirectory
```

Hierbei gilt:

- **Backup Directory** ist das Verzeichnis, in dem die wiederherzustellenden Daten enthalten sind.

```
[-f] [-config Machine\CAName] [-p password]
```

### <a name="-restoredb"></a>-restoreDB

Stellt die Active Directory Zertifikat Dienste-Datenbank wieder her.

```
certutil [options] -restoredb backupdirectory
```

Hierbei gilt:

- **Backup Directory** ist das Verzeichnis, das die wiederherzustellenden Datenbankdateien enthält.

```
[-f] [-config Machine\CAName]
```

### <a name="-restorekey"></a>-restorekey

Stellt das Zertifikat für die Active Directory Zertifikat Dienste und den privaten Schlüssel wieder her.

```
certutil [options] -restorekey backupdirectory | pfxfile
```

Hierbei gilt:

- **Backup Directory** ist das Verzeichnis mit der PFX-Datei, die wieder hergestellt werden soll.

```
[-f] [-config Machine\CAName] [-p password]
```

### <a name="-importpfx"></a>-importpfx

Importieren Sie das Zertifikat und den privaten Schlüssel. Weitere Informationen finden Sie `-store` in diesem Artikel unter dem-Parameter.

```
certutil [options] -importpfx [certificatestorename] pfxfile [modifiers]
```

Hierbei gilt:

- **certifikatestorename** ist der Name des Zertifikat Speichers.

- **modifiziererer** sind eine durch Trennzeichen getrennte Liste, die eine oder mehrere der folgenden Werte enthalten kann:

  1. **AT_SIGNATURE** : die KeySpec wird in eine Signatur geändert.

  2. **AT_KEYEXCHANGE** : die KeySpec wird in den Schlüsselaustausch geändert.

  3. **Noexport** : der private Schlüssel wird nicht exportierbar.

  4. **Nocert** : das Zertifikat wird nicht importiert.

  5. **Nochain** : die Zertifikatskette wird nicht importiert.

  6. **Noroot** : importiert nicht das Stamm Zertifikat.

  7. **Schützen** : schützt Schlüssel mithilfe eines Kennworts.

  8. **Noprotect** : Kenn Wort Schutz Schlüssel nicht mithilfe eines Kennworts

```
[-f] [-user] [-p password] [-csp provider]
```

#### <a name="remarks"></a>Bemerkungen

- Der Standardwert ist der persönliche Computerspeicher.

### <a name="-dynamicfilelist"></a>-dynamicfilelist

Zeigt eine dynamische Datei Liste an.

```
certutil [options] -dynamicfilelist
```

```
[-config Machine\CAName]
```

### <a name="-databaselocations"></a>-databaselocations

Zeigt Daten Bank Speicherorte an.

```
certutil [options] -databaselocations
```

```
[-config Machine\CAName]
```

### <a name="-hashfile"></a>-Hashdatei

Generiert und zeigt einen kryptografiehash über eine Datei an.

```
certutil [options] -hashfile infile [hashalgorithm]
```

### <a name="-store"></a>-Store

Sichert den Zertifikat Speicher.

```
certutil [options] -store [certificatestorename [certID [outputfile]]]
```

Hierbei gilt:

- **certifikatestorename** ist der Name des Zertifikat Speichers. Beispiel:

  - `My, CA (default), Root,`

  - `ldap:///CN=Certification Authorities,CN=Public Key Services,CN=Services,CN=Configuration,DC=cpandl,DC=com?cACertificate?one?objectClass=certificationAuthority (View Root Certificates)`

  - `ldap:///CN=CAName,CN=Certification Authorities,CN=Public Key Services,CN=Services,CN=Configuration,DC=cpandl,DC=com?cACertificate?base?objectClass=certificationAuthority (Modify Root Certificates)`

  - `ldap:///CN=CAName,CN=MachineName,CN=CDP,CN=Public Key Services,CN=Services,CN=Configuration,DC=cpandl,DC=com?certificateRevocationList?base?objectClass=cRLDistributionPoint (View CRLs)`

  - `ldap:///CN=NTAuthCertificates,CN=Public Key Services,CN=Services,CN=Configuration,DC=cpandl,DC=com?cACertificate?base?objectClass=certificationAuthority (Enterprise CA Certificates)`

  - `ldap: (AD computer object certificates)`

  - `-user ldap: (AD user object certificates)`

- **CertID** ist das Zertifikat-oder CRL-Übereinstimmungs Token. Hierbei kann es sich um eine Seriennummer, ein SHA-1-Zertifikat, eine CRL, einen CTL-oder einen öffentlichen Schlüssel Hash, einen numerischen Zertifikat Index (0, 1 usw.), einen numerischen CRL-Index (0, 1 usw.), einen numerischen CTL-Index (.. 0,.. 1 usw.), einen öffentlichen Schlüssel, eine Signatur oder eine Erweiterungs Objekt-ID, einen allgemeinen Namen für den Zertifikat Antragsteller, eine e-Mail-Adresse, einen UPN-oder DNS-Namen, einen Schlüssel Container Namen oder einen CSP-Namen, einen Vorlagen Namen oder eine ObjectID, eine EKU-oder Anwendungsrichtlinien-ObjectID oder einen allgemeinen CRL-Aussteller Viele davon können zu mehreren Übereinstimmungen führen.

- **OutputFile** ist die Datei, die zum Speichern der übereinstimmenden Zertifikate verwendet wird.

```
[-f] [-user] [-enterprise] [-service] [-grouppolicy] [-silent] [-split] [-dc DCName]
```

#### <a name="options"></a>Optionen

- Die `-user` Option greift auf einen Benutzerspeicher anstelle eines Computerspeicher zu.

- Die `-enterprise` Option greift auf einen Computer im Enterprise Store zu.

- Die `-service` Option greift auf einen Computerdienst Speicher zu.

- Die `-grouppolicy` Option greift auf einen Computer Gruppenrichtlinien Speicher zu.

Beispiel:

- `-enterprise NTAuth`

- `-enterprise Root 37`

- `-user My 26e0aaaf000000000004`

- `CA .11`

### <a name="-addstore"></a>-addstore

Fügt dem Speicher ein Zertifikat hinzu. Weitere Informationen finden Sie `-store` in diesem Artikel unter dem-Parameter.

```
certutil [options] -addstore certificatestorename infile
```

Hierbei gilt:

- **certifikatestorename** ist der Name des Zertifikat Speichers.

- **Eingabedatei** ist das Zertifikat oder die CRL-Datei, die Sie zum Speichern hinzufügen möchten.

```
[-f] [-user] [-enterprise] [-grouppolicy] [-dc DCName]
```

### <a name="-delstore"></a>-Delta Store

Löscht ein Zertifikat aus dem Speicher. Weitere Informationen finden Sie `-store` in diesem Artikel unter dem-Parameter.

```
certutil [options] -delstore certificatestorename certID
```

Hierbei gilt:

- **certifikatestorename** ist der Name des Zertifikat Speichers.

- **CertID** ist das Zertifikat-oder CRL-Übereinstimmungs Token.

```
[-enterprise] [-user] [-grouppolicy] [-dc DCName]
```

### <a name="-verifystore"></a>-verifystore

Überprüft ein Zertifikat im Speicher. Weitere Informationen finden Sie `-store` in diesem Artikel unter dem-Parameter.

```
certutil [options] -verifystore certificatestorename [certID]
```

Hierbei gilt:

- **certifikatestorename** ist der Name des Zertifikat Speichers.

- **CertID** ist das Zertifikat-oder CRL-Übereinstimmungs Token.

```
[-enterprise] [-user] [-grouppolicy] [-silent] [-split] [-dc DCName] [-t timeout]
```

### <a name="-repairstore"></a>-repairren Store

Repariert eine Schlüssel Zuordnung oder Update Zertifikat Eigenschaften oder die Schlüssel Sicherheits Beschreibung. Weitere Informationen finden Sie `-store` in diesem Artikel unter dem-Parameter.

```
certutil [options] -repairstore certificatestorename certIDlist [propertyinffile | SDDLsecuritydescriptor]
```

Hierbei gilt:

- **certifikatestorename** ist der Name des Zertifikat Speichers.

- **certidlist** ist eine durch Trennzeichen getrennte Liste von Zertifikat-oder CRL-abgleichstoken. Weitere Informationen finden Sie in der `-store certID` Beschreibung in diesem Artikel.

- **propertyinffile** ist die INF-Datei, die externe Eigenschaften enthält, einschließlich:

  ```
  [Properties]
      19 = Empty ; Add archived property, OR:
      19 =       ; Remove archived property

      11 = {text}Friendly Name ; Add friendly name property

      127 = {hex} ; Add custom hexadecimal property
          _continue_ = 00 01 02 03 04 05 06 07 08 09 0a 0b 0c 0d 0e 0f
          _continue_ = 10 11 12 13 14 15 16 17 18 19 1a 1b 1c 1d 1e 1f

      2 = {text} ; Add Key Provider Information property
        _continue_ = Container=Container Name&
        _continue_ = Provider=Microsoft Strong Cryptographic Provider&
        _continue_ = ProviderType=1&
        _continue_ = Flags=0&
        _continue_ = KeySpec=2

      9 = {text} ; Add Enhanced Key Usage property
        _continue_ = 1.3.6.1.5.5.7.3.2,
        _continue_ = 1.3.6.1.5.5.7.3.1,
  ```

```
[-f] [-enterprise] [-user] [-grouppolicy] [-silent] [-split] [-csp provider]
```

### <a name="-viewstore"></a>-Viewstore

Sichert den Zertifikat Speicher. Weitere Informationen finden Sie `-store` in diesem Artikel unter dem-Parameter.

```
certutil [options] -viewstore [certificatestorename [certID [outputfile]]]
```

Hierbei gilt:

- **certifikatestorename** ist der Name des Zertifikat Speichers.

- **CertID** ist das Zertifikat-oder CRL-Übereinstimmungs Token.

- **OutputFile** ist die Datei, die zum Speichern der übereinstimmenden Zertifikate verwendet wird.

```
[-f] [-user] [-enterprise] [-service] [-grouppolicy] [-dc DCName]
```

#### <a name="options"></a>Optionen

- Die `-user` Option greift auf einen Benutzerspeicher anstelle eines Computerspeicher zu.

- Die `-enterprise` Option greift auf einen Computer im Enterprise Store zu.

- Die `-service` Option greift auf einen Computerdienst Speicher zu.

- Die `-grouppolicy` Option greift auf einen Computer Gruppenrichtlinien Speicher zu.

Beispiel:

- `-enterprise NTAuth`

- `-enterprise Root 37`

- `-user My 26e0aaaf000000000004`

- `CA .11`

### <a name="-viewdelstore"></a>-viewdelta Store

Löscht ein Zertifikat aus dem Speicher.

```
certutil [options] -viewdelstore [certificatestorename [certID [outputfile]]]
```

Hierbei gilt:

- **certifikatestorename** ist der Name des Zertifikat Speichers.

- **CertID** ist das Zertifikat-oder CRL-Übereinstimmungs Token.

- **OutputFile** ist die Datei, die zum Speichern der übereinstimmenden Zertifikate verwendet wird.

```
[-f] [-user] [-enterprise] [-service] [-grouppolicy] [-dc DCName]
```

#### <a name="options"></a>Optionen

- Die `-user` Option greift auf einen Benutzerspeicher anstelle eines Computerspeicher zu.

- Die `-enterprise` Option greift auf einen Computer im Enterprise Store zu.

- Die `-service` Option greift auf einen Computerdienst Speicher zu.

- Die `-grouppolicy` Option greift auf einen Computer Gruppenrichtlinien Speicher zu.

Beispiel:

- `-enterprise NTAuth`

- `-enterprise Root 37`

- `-user My 26e0aaaf000000000004`

- `CA .11`

### <a name="-dspublish"></a>-dspublish

Veröffentlicht ein Zertifikat oder eine Zertifikat Sperr Liste (CRL) für die Active Directory.

```
certutil [options] -dspublish certfile [NTAuthCA | RootCA | SubCA | CrossCA | KRA | User | Machine]
```

```
certutil [options] -dspublish CRLfile [DSCDPContainer [DSCDPCN]]
```

Hierbei gilt:

- **CertFile** ist der Name der zu veröffentlichenden Zertifikatsdatei.

- **Ntauthca** veröffentlicht das Zertifikat im DS Enterprise Store.

- **Rootca** veröffentlicht das Zertifikat im Stamm Speicher für vertrauenswürdige DS.

- Die **subzertifizierungs** Stelle veröffentlicht das Zertifizierungsstellen Zertifikat für das DS-ca-Objekt.

- **Crossca** veröffentlicht das Zertifikat übergreifende Zertifikat für das DS-ca-Objekt.

- **Kra** veröffentlicht das Zertifikat für das DS-Schlüsselwiederherstellungs-Agent-Objekt.

- Der **Benutzer** veröffentlicht das Zertifikat für das Benutzer-DS-Objekt.

- Der **Computer** veröffentlicht das Zertifikat für das Machine DS-Objekt.

- **Crlfile** ist der Name der zu veröffentlichenden CRL-Datei.

- **Dscdpcontainer** ist der DS-CDP-Container CN, in der Regel der Name der Zertifizierungsstellen Maschine.

- **Dscdpcn** ist das DS-CDP-Objekt CN, das in der Regel auf dem kurz Namen der bereinigen Zertifizierungsstelle und dem Schlüssel Index basiert.

- Verwenden `-f` Sie, um ein neues DS-Objekt zu erstellen.

```
[-f] [-user] [-dc DCName]
```

### <a name="-adtemplate"></a>-adtemplate

Zeigt Active Directory Vorlagen an.

```
certutil [options] -adtemplate [template]
```

```
[-f] [-user] [-ut] [-mt] [-dc DCName]
```

### <a name="-template"></a>-Vorlage

Zeigt die Zertifikat Vorlagen an.

```
certutil [options] -template [template]
```

```
[-f] [-user] [-silent] [-policyserver URLorID] [-anonymous] [-kerberos] [-clientcertificate clientcertID] [-username username] [-p password]
```

### <a name="-templatecas"></a>-templatecas

Zeigt die Zertifizierungsstellen (CAS) für eine Zertifikat Vorlage an.

```
certutil [options] -templatecas template
```

```
[-f] [-user] [-dc DCName]
```

### <a name="-catemplates"></a>-| emplates

Zeigt Vorlagen für die Zertifizierungsstelle an.

```
certutil [options] -catemplates [template]
```

```
[-f] [-user] [-ut] [-mt] [-config Machine\CAName] [-dc DCName]
```

### <a name="-setcasites"></a>-setcasites

Dient zum Verwalten von Standortnamen, einschließlich festlegen, überprüfen und Löschen von Standortnamen von Zertifizierungsstellen.

```
certutil [options] -setcasites [set] [sitename]
certutil [options] -setcasites verify [sitename]
certutil [options] -setcasites delete
```

Hierbei gilt:

- **Sitename** ist nur zulässig, wenn eine einzelne Zertifizierungsstelle als Ziel verwendet wird.

```
[-f] [-config Machine\CAName] [-dc DCName]
```

#### <a name="remarks"></a>Bemerkungen

- Die `-config` Option ist für eine einzelne Zertifizierungsstelle vorgesehen (standardmäßig alle Zertifizierungsstellen).

- Die `-f` Option kann verwendet werden, um Validierungs Fehler für den angegebenen **Sitename** zu überschreiben oder alle Zertifizierungsstellen-sitenames zu löschen.

> [!NOTE]
> Weitere Informationen zum Konfigurieren von Zertifizierungsstellen für die Active Directory Domain Services (AD DS) Standortinformationen finden Sie unter [AD DS Site Awareness for AD CS and PKI Clients](https://social.technet.microsoft.com/wiki/contents/articles/14106.ad-ds-site-awareness-for-ad-cs-and-pki-clients.aspx).

### <a name="-enrollmentserverurl"></a>-enrollmentserverURL

Hiermit werden Registrierungs Server-URLs angezeigt, hinzugefügt oder gelöscht, die einer Zertifizierungsstelle zugeordnet sind.

```
certutil [options] -enrollmentServerURL [URL authenticationtype [priority] [modifiers]]
certutil [options] -enrollmentserverURL URL delete
```

Hierbei gilt:

- **AuthenticationType** gibt eine der folgenden Client Authentifizierungsmethoden beim Hinzufügen einer URL an:

  1. **Kerberos** : Verwenden Sie Kerberos-SSL-Anmelde Informationen.

  2. **username** : Verwenden Sie ein benanntes Konto für SSL-Anmelde Informationen.

  3. **ClientCertificate**: Verwenden Sie SSL-Anmelde Informationen für das X. 509-Zertifikat.

  4. **Anonym** : Verwenden Sie anonyme SSL-Anmelde Informationen.

- **Delete** löscht die angegebene URL, die der Zertifizierungsstelle zugeordnet ist.

- **Priorität** ist standardmäßig, `1` Wenn Sie beim Hinzufügen einer URL nicht angegeben wird.

- **modifiziererer** sind eine durch Trennzeichen getrennte Liste, die eine oder mehrere der folgenden Werte enthält:

1. **allowrenewalsonly** -nur Erneuerungs Anforderungen können über diese URL an diese Zertifizierungsstelle übermittelt werden.

2. **allowkeybasedrenewal** : ermöglicht die Verwendung eines Zertifikats, das über kein zugeordnetes Konto in der AD-Verbindung verfügt. Dies gilt nur für den Modus "ClientCertificate" und "allowrenewalsonly".

```
[-config Machine\CAName] [-dc DCName]
```

### <a name="-adca"></a>-ADCA

Zeigt Active Directory Zertifizierungsstellen an.

```
certutil [options] -adca [CAName]
```

```
[-f] [-split] [-dc DCName]
```

### <a name="-ca"></a>-ca

Zeigt Registrierungsrichtlinien-Zertifizierungsstellen an.

```
certutil [options] -CA [CAName | templatename]
```

```
[-f] [-user] [-silent] [-split] [-policyserver URLorID] [-anonymous] [-kerberos] [-clientcertificate clientcertID] [-username username] [-p password]
```

### <a name="-policy"></a>-Richtlinie

Zeigt die Registrierungs Richtlinie an.

```
[-f] [-user] [-silent] [-split] [-policyserver URLorID] [-anonymous] [-kerberos] [-clientcertificate clientcertID] [-username username] [-p password]
```

### <a name="-policycache"></a>-PolicyCache

Hiermit werden Registrierungsrichtlinien-Cache Einträge angezeigt oder gelöscht.

```
certutil [options] -policycache [delete]
```

Hierbei gilt:

- **Delete** löscht die Richtlinien Server-Cache Einträge.

- **-f** löscht alle Cache Einträge.

```
[-f] [-user] [-policyserver URLorID]
```

### <a name="-credstore"></a>--Datenspeicher

Hiermit werden Anmelde Informationsspeicher Einträge angezeigt, hinzugefügt oder gelöscht.

```
certutil [options] -credstore [URL]
certutil [options] -credstore URL add
certutil [options] -credstore URL delete
```

Hierbei gilt:

- **URL** ist die Ziel-URL. Sie können auch verwenden `*` , um alle Einträge abzugleichen oder `https://machine*` um ein URL-Präfix abzugleichen.

- **Hinzufügen** fügt einen Anmelde Informationsspeicher-Eintrag hinzu. Die Verwendung dieser Option erfordert auch die Verwendung von SSL-Anmelde Informationen.

- **Delete** löscht Anmelde Informationsspeicher Einträge.

- **-f** überschreibt einen einzelnen Eintrag oder löscht mehrere Einträge.

```
[-f] [-user] [-silent] [-anonymous] [-kerberos] [-clientcertificate clientcertID] [-username username] [-p password]
```

### <a name="-installdefaulttemplates"></a>-installdefaulttemplates

Installiert Standard Zertifikat Vorlagen.

```
certutil [options] -installdefaulttemplates
```

```
[-dc DCName]
```

### <a name="-urlcache"></a>-Urlcache

Zeigt URL-Cache Einträge an oder löscht sie.

```
certutil [options] -URLcache [URL | CRL | * [delete]]
```

Hierbei gilt:

- **URL** ist die zwischengespeicherte URL.

- Die **CRL** wird nur für alle zwischengespeicherten CRL-URLs ausgeführt.

- **&#42;** funktioniert für alle zwischengespeicherten URLs.

- **Delete** löscht relevante URLs aus dem lokalen Cache des aktuellen Benutzers.

- **-f erzwingt** das Abrufen einer bestimmten URL und das Aktualisieren des Caches.

```
[-f] [-split]
```

### <a name="-pulse"></a>-Pulse

Pulse Ereignisse für die automatische Registrierung.

```
certutil [options] -pulse
```

```
[-user]
```

### <a name="-machineinfo"></a>-machineinfo

Zeigt Informationen zum Active Directory Computer Objekt an.

```
certutil [options] -machineinfo domainname\machinename$
```

### <a name="-dcinfo"></a>-Dcinfo

Zeigt Informationen zum Domänen Controller an. Standardmäßig werden Domänen Controller Zertifikate ohne Überprüfung angezeigt.

```
certutil [options] -DCInfo [domain] [verify | deletebad | deleteall]
```

```
[-f] [-user] [-urlfetch] [-dc DCName] [-t timeout]
```

> [!TIP]
> Die Möglichkeit, eine Active Directory Domain Services (AD DS)-Domäne **[Domäne]** anzugeben und einen Domänen Controller (**-DC**) anzugeben, wurde in Windows Server 2012 hinzugefügt. Um den Befehl erfolgreich auszuführen, müssen Sie ein Konto verwenden, das Mitglied der Gruppe " **Domänen-Admins** " oder "Organisations- **Admins**" ist. Die Verhaltensänderungen dieses Befehls lauten wie folgt:<ol><li>1. wenn keine Domäne angegeben ist und kein bestimmter Domänen Controller angegeben ist, gibt diese Option eine Liste der Domänen Controller zurück, die vom Standard Domänen Controller verarbeitet werden sollen.</li><li>2. wenn keine Domäne angegeben ist, aber ein Domänen Controller angegeben ist, wird ein Bericht der Zertifikate auf dem angegebenen Domänen Controller generiert.</li><li>3. Wenn eine Domäne angegeben ist, jedoch kein Domänen Controller angegeben ist, wird eine Liste mit Domänen Controllern zusammen mit Berichten zu den Zertifikaten für die einzelnen Domänen Controller in der Liste generiert.</li><li>4. wenn die Domäne und der Domänen Controller angegeben sind, wird eine Liste der Domänen Controller vom Zieldomänen Controller generiert. Ein Bericht der Zertifikate für jeden Domänen Controller in der Liste wird ebenfalls generiert.</li></ol>
>
>Nehmen wir beispielsweise an, dass eine Domäne mit dem Namen CPANDL mit einem Domänen Controller namens CPANDL-DC1 vorhanden ist. Sie können den folgenden Befehl ausführen, um eine Liste der Domänen Controller und ihrer Zertifikate abzurufen, die von CPANDL-DC1:`certutil -dc cpandl-dc1 -DCInfo cpandl`

### <a name="-entinfo"></a>-entinfo

Zeigt Informationen zu einer Unternehmens Zertifizierungsstelle an.

```
certutil [options] -entinfo domainname\machinename$
```

```
[-f] [-user]
```

### <a name="-tcainfo"></a>-tcainfo

Zeigt Informationen zur Zertifizierungsstelle an.

```
certutil [options] -tcainfo [domainDN | -]
```

```
[-f] [-enterprise] [-user] [-urlfetch] [-dc DCName] [-t timeout]
```

### <a name="-scinfo"></a>-scinfo

Hiermit werden Informationen über die Smartcard angezeigt.

```
certutil [options] -scinfo [readername [CRYPT_DELETEKEYSET]]
```

Hierbei gilt:

- **CRYPT_DELETEKEYSET** löscht alle Schlüssel auf der Smartcard.

```
[-silent] [-split] [-urlfetch] [-t timeout]
```

### <a name="-scroots"></a>-scroots

Verwaltet smartcardstamm Zertifikate.

```
certutil [options] -scroots update [+][inputrootfile] [readername]
certutil [options] -scroots save \@in\\outputrootfile [readername]
certutil [options] -scroots view [inputrootfile | readername]
certutil [options] -scroots delete [readername]
```

```
[-f] [-split] [-p Password]
```

### <a name="-verifykeys"></a>-verifykeys

Überprüft einen öffentlichen oder privaten Schlüsselsatz.

```
certutil [options] -verifykeys [keycontainername cacertfile]
```

Hierbei gilt:

- **KeyContainerName** ist der Schlüssel Container Name für den Schlüssel, der überprüft werden soll. Diese Option ist standardmäßig auf Computer Schlüssel eingestellt. Verwenden Sie, um zu Benutzer Schlüsseln zu wechseln `-user` .

- **CACertFile** signiert oder verschlüsselt Zertifikat Dateien.

```
[-f] [-user] [-silent] [-config Machine\CAName]
```

#### <a name="remarks"></a>Bemerkungen

- Wenn keine Argumente angegeben werden, wird jedes Signatur Zertifizierungsstellen Zertifikat anhand des privaten Schlüssels überprüft.

- Dieser Vorgang kann nur für lokale Zertifizierungsstellen oder lokale Schlüssel ausgeführt werden.

### <a name="-verify"></a>-Überprüfen

Überprüft ein Zertifikat, eine Zertifikat Sperr Liste (CRL) oder eine Zertifikat Kette.

```
certutil [options] -verify certfile [applicationpolicylist | - [issuancepolicylist]]
certutil [options] -verify certfile [cacertfile [crossedcacertfile]]
certutil [options] -verify CRLfile cacertfile [issuedcertfile]
certutil [options] -verify CRLfile cacertfile [deltaCRLfile]
```

Hierbei gilt:

- **CertFile** ist der Name des Zertifikats, das überprüft werden soll.

- **applicationpolicylist** ist die optionale durch Trennzeichen getrennte Liste erforderlicher Anwendungsrichtlinien-ObjectIDs.

- **issuancepolicylist** ist die optionale durch Trennzeichen getrennte Liste der erforderlichen Ausstellungs Richtlinien-ObjectIDs.

- **CACertFile** ist das optionale Zertifikat der ausstellenden Zertifizierungsstelle, das überprüft werden soll.

- " **crossedcacertfile** " ist das optionale Zertifikat, das von " **CertFile**" Cross-Certified ist.

- **Crlfile** ist die CRL-Datei, mit der die **CACertFile**überprüft wird.

- **issuedcertfile** ist das optionale ausgestellte Zertifikat, das von der crlfile abgedeckt wird.

- **deltacrlfile** ist die optionale Delta-CRL-Datei.

```
[-f] [-enterprise] [-user] [-silent] [-split] [-urlfetch] [-t timeout]
```

#### <a name="remarks"></a>Bemerkungen

- Die Verwendung von **applicationpolicylist** schränkt die Ketten Bildung auf die für die angegebenen Anwendungsrichtlinien gültigen Ketten ein.

- Die Verwendung von **issuancepolicylist** schränkt die Ketten Erstellung auf die für die angegebenen Ausstellungs Richtlinien gültigen Ketten ein.

- Durch die Verwendung von **CACertFile** werden die Felder in der Datei mit " **CertFile** " oder " **crlfile**" überprüft.

- Durch die Verwendung von **issuedcertfile** werden die Felder in der Datei mit **crlfile**überprüft.

- Durch die Verwendung von Delta-Datei werden die Felder in der Datei anhand von " **CertFile**" überprüft.

- Wenn **CACertFile** nicht angegeben wird, wird die vollständige Kette erstellt und anhand von " **CertFile**" überprüft.

- Wenn " **CACertFile** " und " **crossedcacertfile** " angegeben sind, werden die Felder in beiden Dateien anhand von " **CertFile**" überprüft.

### <a name="-verifyctl"></a>-verifyctl

Überprüft die CTL "AuthRoot" oder "unzulässige Zertifikate".

```
certutil [options] -verifyCTL CTLobject [certdir] [certfile]
```

Hierbei gilt:

- **Ctlobject** identifiziert die zu überprüfende CTL, einschließlich:

  - **Authrootwu** : liest das AuthRoot-CAB und übereinstimmende Zertifikate aus dem URL-Cache. Verwenden Sie `-f` stattdessen, um von Windows Update herunterzuladen.

  - **Diszuzuordnung** : liest die nicht zulässigen Zertifikate und die unzulässige Zertifikats Speicherdatei aus dem URL-Cache. Verwenden Sie `-f` stattdessen, um von Windows Update herunterzuladen.

  - **AuthRoot** : liest die CTL der Registrierungs Zwischenspeicherung (AuthRoot). Verwenden `-f` Sie with und eine nicht vertrauenswürdige **CertFile** , um zu erzwingen, dass die Registrierung zwischengespeicherte AuthRoot-und unzulässige Zertifikat-CTLs aktualisiert werden.

  - Nicht **zulässig** : liest die CTL der durch die Registrierung zwischengespeicherten Zertifikate. Verwenden `-f` Sie with und eine nicht vertrauenswürdige **CertFile** , um zu erzwingen, dass die Registrierung zwischengespeicherte AuthRoot-und unzulässige Zertifikat-CTLs aktualisiert werden.

- **Ctlfilename** gibt die Datei oder den HTTP-Pfad zur CTL-bzw. CAB-Datei an.

- **certdir** gibt den Ordner mit Zertifikaten an, die mit den CTL-Einträgen übereinstimmen. Der Standardwert ist der gleiche Ordner oder die gleiche Website wie das **ctlobject**. Die Verwendung eines HTTP-Ordner Pfads erfordert am Ende ein Pfad Trennzeichen. Wenn Sie **AuthRoot** oder nicht **zulässig**angeben, werden mehrere Speicherorte nach übereinstimmenden Zertifikaten, einschließlich lokaler Zertifikat Speicher, crypt32.dll Ressourcen und dem lokalen URL-Cache, durchsucht. Verwenden Sie `-f` , um bei Bedarf von Windows Update herunterzuladen.

- **CertFile** gibt die zu überprüfende Zertifikate an. Zertifikate werden mit CTL-Einträgen abgeglichen und zeigen die Ergebnisse an. Mit dieser Option wird der größte Teil der Standardausgabe unterdrückt.

```
[-f] [-user] [-split]
```

### <a name="-sign"></a>-Sign

Signiert eine Zertifikat Sperr Liste (CRL) oder ein Zertifikat erneut.

```
certutil [options] -sign infilelist | serialnumber | CRL outfilelist [startdate+dd:hh] [+serialnumberlist | -serialnumberlist | -objectIDlist | \@extensionfile]
certutil [options] -sign infilelist | serialnumber | CRL outfilelist [#hashalgorithm] [+alternatesignaturealgorithm | -alternatesignaturealgorithm]
```

Hierbei gilt:

- " **infilelist** " ist eine durch Trennzeichen getrennte Liste von Zertifikat-oder CRL-Dateien, die geändert und neu signiert werden sollen.

- **serialNumber** ist die Seriennummer des Zertifikats, das erstellt werden soll. Der Gültigkeits Zeitraum und andere Optionen können nicht vorhanden sein.

- **CRL** erstellt eine leere CRL. Der Gültigkeits Zeitraum und andere Optionen können nicht vorhanden sein.

- **outfilelist** ist die durch Trennzeichen getrennte Liste der geänderten Zertifikat-oder CRL-Ausgabedateien. Die Anzahl der Dateien muss mit "infilelist" verglichen werden.

- **StartDate + DD: hh** ist die neue Gültigkeitsdauer für die Zertifikat-oder CRL-Dateien, einschließlich:

  - Optionales Datum plus

  - optionale Gültigkeitsdauer für Tage und Stunden

  Wenn beide angegeben werden, müssen Sie ein Pluszeichen Trennzeichen (+) verwenden. Verwenden `now[+dd:hh]` Sie, um zum aktuellen Zeitpunkt zu starten. Verwenden `never` Sie, um kein Ablaufdatum zu verwenden (nur für CRLs).

- **serialnumlist** ist die durch Trennzeichen getrennte Liste der Dateien, die hinzugefügt oder entfernt werden sollen.

- **objectidlist** ist die durch Trennzeichen getrennte Erweiterung ObjectID der Dateien, die entfernt werden sollen.

- ** \@ extensionfile** ist die INF-Datei mit den zu aktualisierenden oder zu entfernenden Erweiterungen. Beispiel:

  ```
  [Extensions]
      2.5.29.31 = ; Remove CRL Distribution Points extension
      2.5.29.15 = {hex} ; Update Key Usage extension
      _continue_=03 02 01 86
  ```

- **HashAlgorithm** ist der Name des Hash Algorithmus. Dies darf nur der Text sein, dem das Vorzeichen vorangestellt ist `#` .

- "Alternate User Name **" ist der** Alternative Signatur Algorithmus-Spezifizierer.

```
[-nullsign] [-f] [-silent] [-cert certID]
```

#### <a name="remarks"></a>Bemerkungen

- Wenn Sie das Minuszeichen (-) verwenden, werden Seriennummern und Erweiterungen entfernt.

- Mit dem Pluszeichen (+) werden einer CRL Seriennummern hinzugefügt.

- Sie können eine Liste verwenden, um gleichzeitig sowohl Seriennummern als auch ObjectIDs aus einer CRL zu entfernen.

- Wenn Sie das Minuszeichen vor " **Alternativen** " verwenden, können Sie das Legacy-Signatur Format verwenden. Wenn Sie das Pluszeichen verwenden, können Sie das alternative Signatur Format verwenden. Wenn Sie nicht den Wert von " **Alternativen**" in der Zertifikat-/CRL angeben, wird das Signatur Format im Zertifikat oder der CRL verwendet.

### <a name="-vroot"></a>-vroot

Erstellt oder löscht virtuelle Webstämme und Dateifreigaben.

```
certutil [options] -vroot [delete]
```

### <a name="-vocsproot"></a>-vocsproot

Erstellt oder löscht virtuelle Webstämme für einen OCSP-WebProxy.

```
certutil [options] -vocsproot [delete]
```

### <a name="-addenrollmentserver"></a>-addenrollmentserver

Fügen Sie ggf. eine Registrierungs Server Anwendung und einen Anwendungs Pool für die angegebene Zertifizierungsstelle hinzu. Mit diesem Befehl werden keine Binärdateien oder Pakete installiert.

```
certutil [options] -addenrollmentserver kerberos | username | clientcertificate [allowrenewalsonly] [allowkeybasedrenewal]
```

Hierbei gilt:

- **addenrollmentserver** erfordert, dass Sie eine Authentifizierungsmethode für die Client Verbindung mit dem Zertifikat Registrierungs Server verwenden, einschließlich:

  - **Kerberos** verwendet Kerberos-SSL-Anmelde Informationen.

  - **username** verwendet das benannte Konto für SSL-Anmelde Informationen.

  - **ClientCertificate** verwendet SSL-Anmelde Informationen für das X. 509-Zertifikat.

- **allowrenewalsonly** gestattet nur Erneuerungs Anforderungen an die Zertifizierungsstelle über die URL.

- **allowkeybasedrenewal** ermöglicht die Verwendung eines Zertifikats ohne Zugeordnetes Konto in Active Directory. Dies gilt bei der Verwendung mit **ClientCertificate** und dem **allowrenewalsonly** -Modus.

```
[-config Machine\CAName]
```

### <a name="-deleteenrollmentserver"></a>-deleteenrollmentserver

Löscht ggf. eine Registrierungs Server Anwendung und einen Anwendungs Pool für die angegebene Zertifizierungsstelle. Mit diesem Befehl werden keine Binärdateien oder Pakete installiert.

```
certutil [options] -deleteenrollmentserver kerberos | username | clientcertificate
```

Hierbei gilt:

- **deleteenrollmentserver** erfordert, dass Sie eine Authentifizierungsmethode für die Client Verbindung mit dem Zertifikat Registrierungs Server verwenden, einschließlich:

  - **Kerberos** verwendet Kerberos-SSL-Anmelde Informationen.

  - **username** verwendet das benannte Konto für SSL-Anmelde Informationen.

  - **ClientCertificate** verwendet SSL-Anmelde Informationen für das X. 509-Zertifikat.

```
[-config Machine\CAName]
```

### <a name="-addpolicyserver"></a>-addpolicyserver

Fügen Sie ggf. eine Richtlinien Server Anwendung und einen Anwendungs Pool hinzu. Mit diesem Befehl werden keine Binärdateien oder Pakete installiert.

```
certutil [options] -addpolicyserver kerberos | username | clientcertificate [keybasedrenewal]
```

Hierbei gilt:

- **addpolicyserver** erfordert, dass Sie eine Authentifizierungsmethode für die Client Verbindung mit dem Zertifikat Richtlinien Server verwenden, einschließlich:

  - **Kerberos** verwendet Kerberos-SSL-Anmelde Informationen.

  - **username** verwendet das benannte Konto für SSL-Anmelde Informationen.

  - **ClientCertificate** verwendet SSL-Anmelde Informationen für das X. 509-Zertifikat.

- **keybasedrenewal** ermöglicht die Verwendung von Richtlinien, die an den Client zurückgegeben werden, der keybasedrenewal-Vorlagen enthält Diese Option gilt nur für die **Benutzername** -und **ClientCertificate** -Authentifizierung.

### <a name="-deletepolicyserver"></a>-deletepolicyserver

Löscht ggf. eine Richtlinien Server Anwendung und einen Anwendungs Pool. Mit diesem Befehl werden keine Binärdateien oder Pakete entfernt.

certutil [Optionen]-deletepolicyserver Kerberos | Benutzername | ClientCertificate [keybasedrenewal]

Hierbei gilt:

- **deletepolicyserver** erfordert, dass Sie eine Authentifizierungsmethode für die Client Verbindung mit dem Zertifikat Richtlinien Server verwenden, einschließlich:

  - **Kerberos** verwendet Kerberos-SSL-Anmelde Informationen.

  - **username** verwendet das benannte Konto für SSL-Anmelde Informationen.

  - **ClientCertificate** verwendet SSL-Anmelde Informationen für das X. 509-Zertifikat.

- **keybasedrenewal** ermöglicht die Verwendung eines keybasedrenewal-Richtlinien Servers.

### <a name="-oid"></a>-OID

Zeigt den Objekt Bezeichner an oder legt einen anzeigen Amen fest.

```
certutil [options] -oid objectID [displayname | delete [languageID [type]]]
certutil [options] -oid groupID
certutil [options] -oid agID | algorithmname [groupID]
```

Hierbei gilt:

- **objectID** zeigt oder an, um den anzeigen Amen hinzufügen.

- **GroupID** ist die GroupID-Nummer (Decimal), die ObjectIDs auflistet.

- **algid** ist die hexadezimal-ID, die ObjectID sucht.

- **algorithmName** ist der Algorithmusname, den ObjectID sucht.

- **Display Name** zeigt den Namen an, der in DS gespeichert werden soll.

- **Delete** löscht den anzeigen Amen.

- **LanguageID** ist der Sprach-ID-Wert (standardmäßig Current: 1033).

- **Typ** ist der Typ des zu erstellenden DS-Objekts, einschließlich:

  - `1`-Vorlage (Standard)

  - `2`-Ausstellungs Richtlinie

  - `3`-Anwendungs Richtlinie

- `-f`erstellt ein DS-Objekt.

### <a name="-error"></a>-Fehler

Zeigt den Meldungs Text an, der einem Fehlercode zugeordnet ist.

```
certutil [options] -error errorcode
```

### <a name="-getreg"></a>-getreg

Zeigt einen Registrierungs Wert an.

```
certutil [options] -getreg [{ca | restore | policy | exit | template | enroll |chain | policyservers}\[progID\]][registryvaluename]
```

Hierbei gilt:

- die Zertifizierungs **Stelle verwendet den** Registrierungsschlüssel einer Zertifizierungsstelle.

- **Restore** verwendet den Registrierungsschlüssel für die Wiederherstellung der Zertifizierungsstelle.

- die **Richtlinie** verwendet den Registrierungsschlüssel des Richtlinien Moduls.

- **Exit** verwendet den Registrierungsschlüssel des ersten Beendigungs Moduls.

- die **Vorlage** verwendet den Registrierungsschlüssel für die Vorlage (Verwendung `-user` für Benutzervorlagen).

- bei der Registrierung wird der Registrierungsschlüssel für die **Registrierung verwendet (** `-user` für Benutzer Kontext verwenden).

- die **Kette** verwendet den Registrierungsschlüssel für die Ketten Konfiguration.

- **policyservers** verwendet den Richtlinien Server-Registrierungsschlüssel.

- **ProgID** verwendet die ProgID der Richtlinie oder des Beendigungs Moduls (Name des Registrierungs unter Schlüssels).

- **registryvaluename** verwendet den Namen des Registrierungs Werts (mit `Name*` Präfix Übereinstimmung).

- der **Wert** verwendet den neuen numerischen, Zeichen folgen-oder Datums Registrierungs Wert bzw. Dateinamen. Wenn ein numerischer Wert mit `+` oder beginnt `-` , werden die im neuen Wert angegebenen Bits im vorhandenen Registrierungs Wert festgelegt oder gelöscht.

```
[-f] [-user] [-grouppolicy] [-config Machine\CAName]
```

#### <a name="remarks"></a>Bemerkungen

- Wenn ein Zeichen folgen Wert mit `+` oder beginnt `-` und der vorhandene Wert ein `REG_MULTI_SZ` Wert ist, wird die Zeichenfolge dem vorhandenen Registrierungs Wert hinzugefügt oder daraus entfernt. Um das Erstellen eines Werts zu erzwingen `REG_MULTI_SZ` , fügen Sie am `\n` Ende des Zeichen folgen Werts ein.

- Wenn der Wert mit beginnt `\@` , ist der restliche Wert der Name der Datei, die die hexadezimale Textdarstellung eines Binär Werts enthält. Wenn Sie nicht auf eine gültige Datei verweist, wird Sie stattdessen als `[Date][+|-][dd:hh]` -ein optionales Datum plus oder minus optionale Tage und Stunden analysiert. Wenn beide angegeben sind, verwenden Sie ein Pluszeichen (+) oder Minuszeichen (-). Verwenden `now+dd:hh` Sie für ein Datum in Bezug auf die aktuelle Zeit.

- Verwenden `chain\chaincacheresyncfiletime \@now` Sie, um zwischengespeicherte CRLs effektiv zu leeren.

### <a name="-setreg"></a>-Eing

Legt einen Registrierungs Wert fest.

```
certutil [options] -setreg [{ca | restore | policy | exit | template | enroll |chain | policyservers}\[progID\]]registryvaluename value
```

Hierbei gilt:

- die Zertifizierungs **Stelle verwendet den** Registrierungsschlüssel einer Zertifizierungsstelle.

- **Restore** verwendet den Registrierungsschlüssel für die Wiederherstellung der Zertifizierungsstelle.

- die **Richtlinie** verwendet den Registrierungsschlüssel des Richtlinien Moduls.

- **Exit** verwendet den Registrierungsschlüssel des ersten Beendigungs Moduls.

- die **Vorlage** verwendet den Registrierungsschlüssel für die Vorlage (Verwendung `-user` für Benutzervorlagen).

- bei der Registrierung wird der Registrierungsschlüssel für die **Registrierung verwendet (** `-user` für Benutzer Kontext verwenden).

- die **Kette** verwendet den Registrierungsschlüssel für die Ketten Konfiguration.

- **policyservers** verwendet den Richtlinien Server-Registrierungsschlüssel.

- **ProgID** verwendet die ProgID der Richtlinie oder des Beendigungs Moduls (Name des Registrierungs unter Schlüssels).

- **registryvaluename** verwendet den Namen des Registrierungs Werts (mit `Name*` Präfix Übereinstimmung).

- der **Wert** verwendet den neuen numerischen, Zeichen folgen-oder Datums Registrierungs Wert bzw. Dateinamen. Wenn ein numerischer Wert mit `+` oder beginnt `-` , werden die im neuen Wert angegebenen Bits im vorhandenen Registrierungs Wert festgelegt oder gelöscht.

```
[-f] [-user] [-grouppolicy] [-config Machine\CAName]
```

#### <a name="remarks"></a>Bemerkungen

- Wenn ein Zeichen folgen Wert mit `+` oder beginnt `-` und der vorhandene Wert ein `REG_MULTI_SZ` Wert ist, wird die Zeichenfolge dem vorhandenen Registrierungs Wert hinzugefügt oder daraus entfernt. Um das Erstellen eines Werts zu erzwingen `REG_MULTI_SZ` , fügen Sie am `\n` Ende des Zeichen folgen Werts ein.

- Wenn der Wert mit beginnt `\@` , ist der restliche Wert der Name der Datei, die die hexadezimale Textdarstellung eines Binär Werts enthält. Wenn Sie nicht auf eine gültige Datei verweist, wird Sie stattdessen als `[Date][+|-][dd:hh]` -ein optionales Datum plus oder minus optionale Tage und Stunden analysiert. Wenn beide angegeben sind, verwenden Sie ein Pluszeichen (+) oder Minuszeichen (-). Verwenden `now+dd:hh` Sie für ein Datum in Bezug auf die aktuelle Zeit.

- Verwenden `chain\chaincacheresyncfiletime \@now` Sie, um zwischengespeicherte CRLs effektiv zu leeren.

### <a name="-delreg"></a>-Delta reg

Löscht einen Registrierungs Wert.

```
certutil [options] -delreg [{ca | restore | policy | exit | template | enroll |chain | policyservers}\[progID\]][registryvaluename]
```

Hierbei gilt:

- die Zertifizierungs **Stelle verwendet den** Registrierungsschlüssel einer Zertifizierungsstelle.

- **Restore** verwendet den Registrierungsschlüssel für die Wiederherstellung der Zertifizierungsstelle.

- die **Richtlinie** verwendet den Registrierungsschlüssel des Richtlinien Moduls.

- **Exit** verwendet den Registrierungsschlüssel des ersten Beendigungs Moduls.

- die **Vorlage** verwendet den Registrierungsschlüssel für die Vorlage (Verwendung `-user` für Benutzervorlagen).

- bei der Registrierung wird der Registrierungsschlüssel für die **Registrierung verwendet (** `-user` für Benutzer Kontext verwenden).

- die **Kette** verwendet den Registrierungsschlüssel für die Ketten Konfiguration.

- **policyservers** verwendet den Richtlinien Server-Registrierungsschlüssel.

- **ProgID** verwendet die ProgID der Richtlinie oder des Beendigungs Moduls (Name des Registrierungs unter Schlüssels).

- **registryvaluename** verwendet den Namen des Registrierungs Werts (mit `Name*` Präfix Übereinstimmung).

- der **Wert** verwendet den neuen numerischen, Zeichen folgen-oder Datums Registrierungs Wert bzw. Dateinamen. Wenn ein numerischer Wert mit `+` oder beginnt `-` , werden die im neuen Wert angegebenen Bits im vorhandenen Registrierungs Wert festgelegt oder gelöscht.

```
[-f] [-user] [-grouppolicy] [-config Machine\CAName]
```

#### <a name="remarks"></a>Bemerkungen

- Wenn ein Zeichen folgen Wert mit `+` oder beginnt `-` und der vorhandene Wert ein `REG_MULTI_SZ` Wert ist, wird die Zeichenfolge dem vorhandenen Registrierungs Wert hinzugefügt oder daraus entfernt. Um das Erstellen eines Werts zu erzwingen `REG_MULTI_SZ` , fügen Sie am `\n` Ende des Zeichen folgen Werts ein.

- Wenn der Wert mit beginnt `\@` , ist der restliche Wert der Name der Datei, die die hexadezimale Textdarstellung eines Binär Werts enthält. Wenn Sie nicht auf eine gültige Datei verweist, wird Sie stattdessen als `[Date][+|-][dd:hh]` -ein optionales Datum plus oder minus optionale Tage und Stunden analysiert. Wenn beide angegeben sind, verwenden Sie ein Pluszeichen (+) oder Minuszeichen (-). Verwenden `now+dd:hh` Sie für ein Datum in Bezug auf die aktuelle Zeit.

- Verwenden `chain\chaincacheresyncfiletime \@now` Sie, um zwischengespeicherte CRLs effektiv zu leeren.

### <a name="-importkms"></a>-importkms

Importiert Benutzerschlüssel und Zertifikate in die Server Datenbank für die Schlüssel Archivierung.

```
certutil [options] -importKMS userkeyandcertfile [certID]
```

Hierbei gilt:

- " **userkeyandcertfile** " ist eine Datendatei mit privaten Benutzer Schlüsseln und Zertifikaten, die archiviert werden sollen. Diese Datei kann wie folgt lauten:

  - Eine Exportdatei für den Exchange-Schlüssel Verwaltungs Server (KMS).

  - Eine PFX-Datei.

- CertID ist ein abgleichstoken für die Zuordnung von KMS-Export Dateien. Weitere Informationen finden Sie `-store` in diesem Artikel unter dem-Parameter.

- `-f`importiert Zertifikate, die nicht von der Zertifizierungsstelle ausgestellt wurden.

```
[-f] [-silent] [-split] [-config Machine\CAName] [-p password] [-symkeyalg symmetrickeyalgorithm[,keylength]]
```

### <a name="-importcert"></a>-Import CERT

Importiert eine Zertifikatsdatei in die-Datenbank.

```
certutil [options] -importcert certfile [existingrow]
```

Hierbei gilt:

- **existingrow** importiert das Zertifikat anstelle einer ausstehenden Anforderung für denselben Schlüssel.

- `-f`importiert Zertifikate, die nicht von der Zertifizierungsstelle ausgestellt wurden.

```
[-f] [-config Machine\CAName]
```

#### <a name="remarks"></a>Bemerkungen

Die Zertifizierungsstelle muss möglicherweise auch für die Unterstützung von fremd Zertifikaten konfiguriert werden. Geben Sie hierzu ein `import - certutil -setreg ca\KRAFlags +KRAF_ENABLEFOREIGN` .

### <a name="-getkey"></a>-GetKey

Ruft ein archiviertes BLOB für die Wiederherstellung privater Schlüssel ab, generiert ein Wiederherstellungs Skript oder stellt archivierte Schlüssel wieder her.

```
certutil [options] -getkey searchtoken [recoverybloboutfile]
certutil [options] -getkey searchtoken script outputscriptfile
certutil [options] -getkey searchtoken retrieve | recover outputfilebasename
```

Hierbei gilt:

- **Skript** generiert ein Skript zum Abrufen und Wiederherstellen von Schlüsseln (Standardverhalten, wenn mehrere übereinstimmende Wiederherstellungs Kandidaten gefunden werden oder wenn die Ausgabedatei nicht angegeben ist).

- durch **Abrufen** werden mindestens eine Schlüsselwiederherstellungs-Blobdatei abgerufen (Standardverhalten, wenn genau ein übereinstimmender Wiederherstellungs Kandidat gefunden wird und die Ausgabedatei angegeben ist). Wenn Sie diese Option verwenden, werden alle Erweiterungen abgeschnitten, und die Zertifikat spezifische Zeichenfolge und die. rec-Erweiterung werden für jedes Schlüsselwiederherstellungs-BLOB angefügt.  Jede Datei enthält eine Zertifikat Kette und einen zugeordneten privaten Schlüssel, die weiterhin in einem oder mehreren Schlüsselwiederherstellungs-Agent-Zertifikaten verschlüsselt sind.

- durch die Wiederherstellung werden private Schlüssel in einem Schritt abgerufen und **wieder hergestellt** (erfordert Schlüssel Wiederherstellungs-Agentzertifikate und private Schlüssel). Wenn Sie diese Option verwenden, werden alle Erweiterungen abgeschnitten und die Erweiterung ". p12" angefügt.  Jede Datei enthält die wiederhergestellten Zertifikat Ketten und die zugehörigen privaten Schlüssel, die als PFX-Datei gespeichert werden.

- **searchtoken** wählt die Schlüssel und Zertifikate aus, die wieder hergestellt werden sollen, einschließlich:

  - 1. Allgemeiner Name (CN) für das Zertifikat

  - 2. Seriennummer des Zertifikats

  - 3. SHA-1-Hash Hash (Fingerabdruck)

  - 4. Zertifikat-keyid SHA-1-Hash (Subjekt Schlüssel Bezeichner)

  - 5. Requestname (Domäne \ Benutzer)

  - 6. UPN (Benutzer \@ Domäne)

- " **wiederherstellungsbloboutfile** " gibt eine Datei mit einer Zertifikat Kette und einem zugeordneten privaten Schlüssel aus, die noch in einem oder mehreren Schlüssel Wiederherstellungs-Agent-Zertifikaten verschlüsselt sind.

- **outputScriptFile** gibt eine Datei mit einem Batch-Skript aus, um private Schlüssel abzurufen und wiederherzustellen.

- **outputfilebasename** gibt einen Datei Basisnamen aus.

```
[-f] [-unicodetext] [-silent] [-config Machine\CAName] [-p password] [-protectto SAMnameandSIDlist] [-csp provider]
```

### <a name="-recoverkey"></a>-recoverkey

Stellen Sie einen archivierten privaten Schlüssel wieder her.

```
certutil [options] -recoverkey recoveryblobinfile [PFXoutfile [recipientindex]]
```

```
[-f] [-user] [-silent] [-split] [-p password] [-protectto SAMnameandSIDlist] [-csp provider] [-t timeout]
```

### <a name="-mergepfx"></a>-mergePFX

Führt PFX-Dateien zusammen.

```
certutil [options] -mergePFX PFXinfilelist PFXoutfile [extendedproperties]
```

Hierbei gilt:

- **Pfxinfilelist** eine durch Trennzeichen getrennte Liste mit PFX-Eingabedateien.

- **Pfxoutfile** ist der Name der PFX-Ausgabedatei.

- **collectionobjekte** schließt erweiterte Eigenschaften ein.

```
[-f] [-user] [-split] [-p password] [-protectto SAMnameAndSIDlist] [-csp provider]
```

#### <a name="remarks"></a>Bemerkungen

- Das in der Befehlszeile angegebene Kennwort muss eine durch Trennzeichen getrennte Kenn Wort Liste sein.

- Wenn mehr als ein Kennwort angegeben wird, wird das letzte Kennwort für die Ausgabedatei verwendet. Wenn nur ein Kennwort angegeben wird, oder wenn das letzte Kennwort lautet `*` , wird der Benutzer zur Eingabe des Kennworts für die Ausgabedatei aufgefordert.

### <a name="-convertepf"></a>-convertepf

Konvertiert eine PFX-Datei in eine EPF-Datei.

```
certutil [options] -convertEPF PFXinfilelist PFXoutfile [cast | cast-] [V3CAcertID][,salt]
```

Hierbei gilt:


- **Pfxinfilelist** eine durch Trennzeichen getrennte Liste mit PFX-Eingabedateien.

- **Pfxoutfile** ist der Name der PFX-Ausgabedatei.

- **EPF** ist der Name der EPF-Ausgabedatei.

- **Cast** verwendet CAST 64 Encryption.

- **Cast-** verwendet CAST 64 Encryption (Export)

- **V3CAcertID** ist das V3-Zertifizierungsstellen-Zertifikat Übereinstimmungs Token. Weitere Informationen finden Sie `-store` in diesem Artikel unter dem-Parameter.

- **Salt** ist die Salt-Zeichenfolge der EPF-Ausgabedatei.

```
[-f] [-silent] [-split] [-dc DCName] [-p password] [-csp provider]
```

#### <a name="remarks"></a>Bemerkungen

- Das in der Befehlszeile angegebene Kennwort muss eine durch Trennzeichen getrennte Kenn Wort Liste sein.

- Wenn mehr als ein Kennwort angegeben wird, wird das letzte Kennwort für die Ausgabedatei verwendet. Wenn nur ein Kennwort angegeben wird, oder wenn das letzte Kennwort lautet `*` , wird der Benutzer zur Eingabe des Kennworts für die Ausgabedatei aufgefordert.

### <a name="-"></a>-?

Zeigt die Liste der Parameter an.

```
certutil -?
certutil <name_of_parameter> -?
certutil -? -v
```

Hierbei gilt:

- **-?** zeigt die vollständige Liste der Parameter an.

- **-`<name_of_parameter>` -?** Zeigt Hilfe Inhalt für den angegebenen Parameter an.

- **-?-v** zeigt eine vollständige Liste der Parameter und Optionen an.

## <a name="options"></a>Optionen

Dieser Abschnitt definiert alle Optionen, die Sie basierend auf dem Befehl angeben können. Jeder Parameter enthält Informationen darüber, welche Optionen für die Verwendung gültig sind.

| Optionen | Beschreibung |
| ------- | ----------- |
| -nullsign | Verwenden Sie den Hash der Daten als Signatur. |
| -f | Erzwingen von überschreiben. |
| -enterprise | Verwenden Sie den Zertifikat Speicher des lokalen Computers für die Unternehmens Registrierung. |
| -Benutzer | Verwenden Sie die HKEY_CURRENT_USER-Schlüssel oder den Zertifikat Speicher. |
| -GroupPolicy | Verwenden Sie den Gruppenrichtlinien-Zertifikat Speicher. |
| -UT | Anzeigen von Benutzervorlagen. |
| -MT | Zeigen Sie Maschinen Vorlagen an. |
| -Unicode | Schreiben Sie die umgeleitete Ausgabe in Unicode. |
| -UnicodeText | Schreiben der Ausgabedatei in Unicode. |
| -GMT | Anzeige Zeiten mithilfe von GMT. |
| -Sekunden | Anzeige Zeiten mithilfe von Sekunden und Millisekunden. |
| -unbeaufsichtigt | Verwenden `silent` Sie das Flag, um den Crypt-Kontext abzurufen. |
| -Teilen | Unterteilen Sie eingebettete ASN. 1-Elemente, und speichern Sie Sie in Dateien. |
| -v | Geben Sie ausführlichere (ausführliche) Informationen an. |
| -PrivateKey | Hiermit werden Daten zum Kennwort und zum privaten Schlüssel angezeigt. |
| -PIN anheften | Smartcard-PIN. |
| -urlfetch | Abrufen und Überprüfen von AIA certs und CDP-CRLs. |
| -config machine\caname | Zertifizierungsstelle und Computer namens Zeichenfolge. |
| -policyserver urlorid | URL oder ID des Richtlinien Servers. Verwenden Sie für Auswahl-U/I `-policyserver` . Verwenden Sie für alle Richtlinien Server`-policyserver *`|
| -Anonym | Anonyme SSL-Anmelde Informationen verwenden. |
| -Kerberos | Verwenden Sie die Kerberos-SSL-Anmelde Informationen. |
| -ClientCertificate clientcertid | SSL-Anmelde Informationen des X. 509-Zertifikats verwenden. Verwenden Sie für Auswahl-U/I `-clientcertificate` . |
| -username username | Verwenden Sie das benannte Konto für SSL-Anmelde Informationen. Verwenden Sie für Auswahl-U/I `-username` . |
| -CERT CertID | Signaturzertifikat |
| -DC DCNAME | Richten Sie einen bestimmten Domänen Controller ein. |
| -Einschränkungs Liste einschränken | Durch Trennzeichen getrennte Einschränkungs Liste. Jede Einschränkung besteht aus einem Spaltennamen, einem relationalen Operator und einer Konstanten Ganzzahl, einer Zeichenfolge oder einem Datum. Einem Spaltennamen kann ein Plus-oder Minuszeichen vorangestellt werden, um die Sortierreihenfolge anzugeben. Beispiel: `requestID = 47`, `+requestername >= a, requestername` oder `-requestername > DOMAIN, Disposition = 21` |
| -Out ColumnList | Durch Trennzeichen getrennte Spaltenliste. |
| -p Kennwort | Kennwort |
| -protectto samnameandsidlist | Durch Trennzeichen getrennte SAM-Name/sid-Liste. |
| -CSP-Anbieter | Anbieter |
| -t Timeout | URL-Abruf Timeout in Millisekunden. |
| -symkeyalg symmetrickeyalgorithmus [, keylength] | Der Name des symmetrischen Schlüssel Algorithmus mit optionaler Schlüssellänge. Beispiel: `AES,128` oder `3DES`. |

### <a name="additional-references"></a>Zusätzliche Referenzen

Weitere Beispiele zur Verwendung dieses Befehls finden Sie unter.

- [Certutil-Beispiele für die Verwaltung von Active Directory Zertifikat Diensten (AD CS) über die Befehlszeile](https://social.technet.microsoft.com/wiki/contents/articles/3063.certutil-examples-for-managing-active-directory-certificate-services-ad-cs-from-the-command-line.aspx)

- [Certutil-Aufgaben für die Verwaltung von Zertifikaten](/previous-versions/orphan-topics/ws.10/cc772898(v=ws.10))

- [Binärer Anforderungs Export mithilfe der exemplarischen Vorgehensweise für das certutil.exe-Befehlszeilen Tool](https://social.technet.microsoft.com/wiki/contents/articles/7573.active-directory-certificate-services-pki-key-archival-and-management.aspx)

- [Zertifikat Erneuerung der Stamm Zertifizierungsstelle](https://social.technet.microsoft.com/wiki/contents/articles/2016.root-ca-certificate-renewal.aspx)

- [certutil-Befehl](certutil.md)
