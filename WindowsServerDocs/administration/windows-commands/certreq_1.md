---
title: certreq
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7a04e51f-f395-4bff-b57a-0e9efcadf973
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9e48682cee40c00e187ca674bd8019b136a2c3f4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59818141"
---
# <a name="certreq"></a>certreq



Certreq kann verwendet werden, zum Anfordern von Zertifikaten von einer Zertifizierungsstelle (CA) zum Abrufen einer Antwort auf eine vorherige Anforderung von einer Zertifizierungsstelle zum Erstellen einer neuen Anforderung aus einer INF-Datei zu akzeptieren, und installieren Sie eine Antwort auf eine Anforderung, erstellen Sie eine Kreuzzertifizierung oder die qualifizierte unterordnungsanforderung aus einer vorhandenen Zertifizierungsstellenzertifikats oder Anforderung und eine Kreuzzertifizierung oder qualifizierte unterordnungsanforderung signiert.

> [!WARNING]
> - Frühere Versionen von Certreq möglicherweise keine aller Optionen bereit, die in diesem Dokument beschrieben werden. Sie können alle Optionen anzuzeigen, die eine bestimmte Version von Certreq bereitstellt, durch Ausführen der Befehle im Syntaxabschnitt Notationen angezeigt.
> - Erstellen eine neue zertifikatanforderung, die auf Grundlage einer Vorlage Schlüsselnachweis, wenn Sie sich in einer Umgebung mit CEP/CES unterstützt nicht certreq

## <a name="BKMK_Contents"></a>Inhalt

Die wichtigsten Abschnitte in diesem Artikel sind wie folgt aus:
1.  [Verbs](#BKMK_Verbs)
2.  [Die Syntax Notationen](#BKMK_notation)
3.  [Optionen](#BKMK_Options)
4.  [Formats](#BKMK_Formats)
5.  [Zusätzliche Certreq-Beispiele](#BKMK_Examples)

## <a name="BKMK_Verbs"></a>Verbs

Gibt es beschreibt folgende Tabelle die Verben, die mit dem Befehl "Certreq" verwendet werden können

|Schalter|Beschreibung|
|------|-----------|
|-Submit|Sendet eine Anforderung an eine Zertifizierungsstelle. Weitere Informationen finden Sie unter [Certreq-übermitteln](#BKMK_Submit).|
|-Abrufen *Anforderungs-ID*|Ruft eine Antwort auf eine vorherige Anforderung von einer Zertifizierungsstelle ab. Weitere Informationen finden Sie unter [Certreq-abrufen](#BKMK_Retrieve).|
|– Neue|Erstellt eine neue Anforderung aus einer INF-Datei an. Weitere Informationen finden Sie unter [Certreq – neue](#BKMK_New).|
|-Akzeptieren|Akzeptiert und installiert eine Antwort auf eine zertifikatanforderung. Weitere Informationen finden Sie unter [Certreq-akzeptieren](#BKMK_accept).|
|-Policy|Legt die Richtlinie für eine Anforderung. Weitere Informationen finden Sie unter [Certreq-Richtlinie](#BKMK_policy).|
|– Anmeldung|Signiert eine Kreuzzertifizierung oder eine qualifizierte unterordnungsanforderung. Weitere Informationen finden Sie unter [Certreq-Anmeldung](#BKMK_sign).|
|– Registrieren|Für registriert, oder ein Zertifikat erneuert. Weitere Informationen finden Sie unter [Certreq-registrieren](#BKMK_enroll).|
|-?|Zeigt eine Liste von Certreq-Syntax, Optionen und Beschreibungen.|
|*\<verb>* -?|Zeigt die Hilfe für das angegebene Verb.|
|-v -?|Zeigt eine ausführliche Liste mit dem Certreq-Syntax, Optionen und eine Beschreibung an.|

Wechseln Sie zurück zur [Inhalt](#BKMK_Contents)

## <a name="BKMK_notation"></a>Die Syntax Notationen

-   Führen Sie für grundlegende Befehlszeilensyntax `certreq -?`
-   Führen Sie die Syntax zum Verwenden von Certutil mit der ein bestimmtes Verb **Certreq**  *\<Verb >* **-?**
-   Um die Certutil-Syntax in eine Textdatei zu senden, führen Sie die folgenden Befehle aus:  
    -   `certreq -v -? > certreqhelp.txt`
    -   `notepad certreqhelp.txt`

Die folgende Tabelle beschreibt die Notation verwendet, um die Syntax der Befehlszeile anzugeben.

|Notation|Beschreibung|
|--------|-----------|
|Text ohne eckigen oder geschweiften Klammern|Elemente, die Sie eingeben müssen, siehe|
|\<Text in spitzen Klammern >|Platzhalter für die Sie einen Wert angeben muss|
|[Text innerhalb der eckigen Klammern]|Optionale Elemente|
|{Text in geschweiften Klammern}|Der Satz von erforderlichen Elemente; Wählen Sie eine|
|Senkrechter Strich (&#124;)|Trennzeichen für sich gegenseitig ausschließende Elemente Wählen Sie eine|
|Auslassungspunkte (…)|Elemente, die wiederholt werden kann|

Wechseln Sie zurück zur [Inhalt](#BKMK_Contents)

## <a name="BKMK_Submit"></a>Certreq – übermitteln

Dies die Standardparameter certreq.exe ist, wenn keine Option explizit an der Eingabeaufforderung angegeben wurde, wird versucht, dass certreq.exe Übermitteln einer zertifikatanforderung an eine Zertifizierungsstelle.
```
CertReq [-Submit] [Options] [RequestFileIn [CertFileOut [CertChainFileOut [FullResponseFileOut]]]]
```
Sie müssen eine Datei zur zertifikatanforderung angeben, bei Verwendung der – Option übermitteln. Wenn dieser Parameter ausgelassen wird, wird ein Fenster für allgemeine Datei öffnen, in dem Sie die entsprechende Datei auswählen können.

Sie können diese Beispiele als Ausgangspunkt verwenden, um die zertifikatanforderung für das Senden zu erstellen:

Verwenden Sie zum Übermitteln eine einfachen zertifikatanforderung im folgenden Beispiel:
```
certreq –submit certRequest.req certnew.cer certnew.pfx
```
Um ein Zertifikat anfordern, indem Sie SAN-Attribut angeben, finden Sie auf die ausführlichen Schritte im Microsoft Knowledge Base-Artikel 931351 [wie ein Zertifikat für sicheres LDAP eine Subject Alternative Name hinzugefügt](https://support.microsoft.com/kb/931351) in der"das Hilfsprogramm Certreq.exe verwenden im Abschnitt "erstellen und Übermitteln einer zertifikatanforderung, die ein SAN enthält.

Wechseln Sie zurück zur [Inhalt](#BKMK_Contents)

## <a name="BKMK_Retrieve"></a>Certreq – abrufen

```
certreq -retrieve [Options] RequestId [CertFileOut [CertChainFileOut [FullResponseFileOut]]]
```
-   Wenn Sie im Dialogfeld CAComputerName\CANamea - Config oder CAName angeben nicht angezeigt wird, und zeigt eine Liste aller Zertifizierungsstellen, die verfügbar sind.
-   Wenn Sie anstelle der-Config CAComputerName\CAName - Config - verwenden, wird der Vorgang mit der Standardzertifizierungsstelle verarbeitet.
-   Können Sie Certreq-abrufen *RequestID* um das Zertifikat abzurufen, nachdem es tatsächlich von die Zertifizierungsstelle ausgestellt hat. Die *RequestID*PKC kann eine Dezimalzahl oder hex mit 0 x-Präfix, und sie können eine Seriennummer des Zertifikats ohne Präfix 0 X. Sie können es auch verwenden, um ein Zertifikat abzurufen, die jemals von der Zertifizierungsstelle, einschließlich widerrufenen oder abgelaufene Zertifikaten, unabhängig davon, ob das Zertifikat der Anforderung jemals den Status "Ausstehend" war ausgegeben wurde.
-   Wenn Sie eine Anforderung an die Zertifizierungsstelle senden, kann das Richtlinienmodul der Zertifizierungsstelle lassen die Anforderung in einem Status "Ausstehend" und die Rückgabe der *RequestID* an den Aufrufer Certreq für die Anzeige. Schließlich wird der Administrator der Zertifizierungsstelle stellen Sie das Zertifikat oder die Anforderung verweigert.

Der folgenden Befehl ruft die Zertifikat-Id 20 ab und erstellt die Zertifikatdatei (. cer):
```
certreq -retrieve 20 MyCertificate.cer 

```
Wechseln Sie zurück zur [Inhalt](#BKMK_Contents)

## <a name="BKMK_New"></a>Certreq – new

```
certreq -new [Options] [PolicyFileIn [RequestFileOut]]
```
Da die INF-Datei für einen umfangreichen Satz von Parametern und-Optionen angegeben werden kann, ist es schwierig, eine Standardvorlage zu definieren, die Administratoren für alle Zwecke verwendet werden soll. Aus diesem Grund wird in diesem Abschnitt aktivieren Sie zum Erstellen einer INF-Datei, die auf Ihre speziellen Anforderungen zugeschnitten sind alle Optionen beschrieben. Die folgenden Schlüsselwörter werden verwendet, um die INF-Datei-Struktur zu beschreiben.
1.  Ein *Abschnitt* ist ein Bereich in der INF-Datei, die eine logische Gruppe von Schlüsseln behandelt. Ein Abschnitt wird immer in Klammern in der INF-Datei angezeigt.
2.  Ein *Schlüssel* ist der Parameter, der in der linken Seite des Gleichheitszeichens wird.
3.  Ein *Wert* ist der Parameter, der in der rechten Seite des Gleichheitszeichens wird.

Eine minimale INF-Datei würde beispielsweise etwa wie folgt aussehen:
```
[NewRequest] 
; At least one value must be set in this section 
Subject = "CN=W2K8-BO-DC.contoso2.com"
```
Im folgenden werden einige der möglichen Abschnitte, die auf die INF-Datei hinzugefügt werden können:

**[NewRequest]**

In diesem Abschnitt ist erforderlich für eine INF-Datei, die als Vorlage für eine neue zertifikatanforderung fungiert. In diesem Abschnitt erfordert mindestens einen Schlüssel mit einem Wert.

|Key|Definition|Wert|Beispiel|
|---|----------|-----|-------|
|Antragsteller|Mehrere Anwendungen basieren auf der Antragstellerinformationen in einem Zertifikat. Daher empfiehlt es sich, dass ein Wert für diesen Schlüssel angegeben werden. Wenn der Antragsteller hier nicht festgelegt ist, empfiehlt es sich, dass ein Antragstellernamen als Teil des Antragstellers Erweiterung des alternativen Zertifikat enthalten sein.|Relative Distinguished Name-Zeichenfolgenwerten|Subject = "CN=computer1.contoso.com" Subject="CN=John Smith,CN=Users,DC=Contoso,DC=com"|
|Exportable|Wenn dieses Attribut auf "true" festgelegt ist, kann der private Schlüssel mit dem Zertifikat exportiert werden. Um ein hohes Maß an Sicherheit zu gewährleisten, sollte nicht private Schlüssel exportiert werden. Allerdings kann in einigen Fällen es erforderlich sein, machen den privaten Schlüssel exportierbar ist, wenn mehrere Computer oder Benutzer den gleichen privaten Schlüssel gemeinsam nutzen müssen.|"true", "false"|Exportierbare = "true". CNG-Schlüsseln können dadurch unterscheiden "und" Plaintext "Exportierbar" markieren. CAPI1 Schlüssel ist nicht möglich.|
|ExportableEncrypted|Gibt an, ob der private Schlüssel exportierbar sein soll, festgelegt werden soll.|"true", "false"|ExportableEncrypted = True</br>Tipp: Nicht alle öffentlichen Schlüssellängen und Algorithmen funktionieren mit allen Hashalgorithmen. Tamehe angegeben, dass der CSP auch des angegebenen Hashalgorithmus unterstützen muss. Um die Liste der unterstützten Hashalgorithmen anzuzeigen, können Sie den Befehl ausführen. <code>certutil -oid 1 &#124; findstr pwszCNGAlgid &#124; findstr /v CryptOIDInfo</code>|
|HashAlgorithm|Für diese Anforderung zu verwendende Hashalgorithmus.|Sha256, sha384, sha512, sha1, md5, md4, md2|HashAlgorithm = sha1. Um die Liste der unterstützten Hashalgorithmen verwenden, finden Sie unter: Certutil - Oid 1 &#124; Findstr PwszCNGAlgid &#124; Findstr/v CryptOIDInfo|
|KeyAlgorithm|Der Algorithmus, der zum Generieren eines öffentlichen und privaten Schlüsselpaars vom Dienstanbieter verwendet werden.|RSA, DH, DSA, ECDH_P256, ECDH_P521, ECDSA_P256, ECDSA_P384, ECDSA_P521|KeyAlgorithm = RSA|
|KeyContainer|Es wird nicht empfohlen, legen Sie diesen Parameter für neue Anforderungen, in dem neue Daten generiert wird. Der Schlüsselcontainer wird automatisch generiert und vom System verwaltet. Für Anforderungen, in dem das vorhandene Schlüsselmaterial verwendet werden soll, kann dieser Wert auf den Schlüsselcontainer Namen des vorhandenen Schlüssels festgelegt werden. Verwenden Sie den Certutil – Schlüssel-Befehl aus, um die Liste der verfügbaren Key Container für den Kontext des Computers anzuzeigen. Verwenden Sie den Certutil – Schlüssel – User-Befehl für den Kontext des aktuellen Benutzers.|Zufällige Zeichenfolge</br>Tipp: Sie sollten alle INF-Schlüsselwert in doppelte Anführungszeichen verwenden, die Leerzeichen oder Sonderzeichen enthalten, um potenzielle Analyse INF-Probleme zu vermeiden.|KeyContainer = {C347BD28-7F69-4090-AA16-BC58CF4D749C}|
|KeyLength|Definiert die Länge des öffentlichen und privaten Schlüssels. Die Länge des Schlüssels hat Auswirkungen auf die Sicherheitsstufe des Zertifikats. Größere Schlüssellänge bietet in der Regel eine höhere Sicherheitsstufe; Bei einigen Anwendungen haben jedoch möglicherweise Einschränkungen im Hinblick auf die Länge des Schlüssels.|Gültige Schlüssellänge, die von den cryptographic Service Provider unterstützt wird.|KeyLength = 2048|
|KeySpec|Bestimmt, ob der Schlüssel für Signaturen, für Exchange (Verschlüsselung), oder für beides verwendet werden kann.|AT_NONE, AT_SIGNATURE, AT_KEYEXCHANGE|KeySpec = AT_KEYEXCHANGE|
|KeyUsage|Definiert, wofür der Zertifikatschlüssel verwendet werden soll.|CERT_DIGITAL_SIGNATURE_KEY_USAGE -- 80 (128)</br>Tipp: Die angezeigten Werte sind Hexadezimalwerte (dezimal) für jedes Bit-Definition. Älterer Syntax kann auch verwendet werden: ein einzelner hexadezimaler Wert mit mehreren bits festgelegt ist, anstatt die symbolische Darstellung. Z. B. KeyUsage 0xa0 =.</br>CERT_NON_REPUDIATION_KEY_USAGE -- 40 (64)</br>CERT_KEY_ENCIPHERMENT_KEY_USAGE -- 20 (32)</br>CERT_DATA_ENCIPHERMENT_KEY_USAGE -- 10 (16)</br>CERT_KEY_AGREEMENT_KEY_USAGE -- 8</br>CERT_KEY_CERT_SIGN_KEY_USAGE -- 4</br>CERT_OFFLINE_CRL_SIGN_KEY_USAGE -- 2</br>CERT_CRL_SIGN_KEY_USAGE -- 2</br>CERT_ENCIPHER_ONLY_KEY_USAGE -- 1</br>CERT_DECIPHER_ONLY_KEY_USAGE -- 8000 (32768)|KeyUsage = "CERT_DIGITAL_SIGNATURE_KEY_USAGE &#124; CERT_KEY_ENCIPHERMENT_KEY_USAGE"</br>Tipp: Mehrere Werte verwenden Sie einen senkrechten Strich (&#124;)-Symbol als Trennzeichen. Stellen Sie sicher, dass Sie, Anführungszeichen verwenden, wenn mehrere Werte zu verwenden, um INF Analyse der Probleme zu vermeiden.|
|KeyUsageProperty|Ruft einen Wert, der den jeweiligen Zweck identifiziert, für den privater Schlüssel verwendet werden kann.|NCRYPT_ALLOW_DECRYPT_FLAG -- 1</br>NCRYPT_ALLOW_SIGNING_FLAG -- 2</br>NCRYPT_ALLOW_KEY_AGREEMENT_FLAG -- 4</br>NCRYPT_ALLOW_ALL_USAGES -- ffffff (16777215)|KeyUsageProperty = "NCRYPT_ALLOW_DECRYPT_FLAG &#124; NCRYPT_ALLOW_SIGNING_FLAG"|
|MachineKeySet|Dieser Schlüssel ist wichtig, wenn Sie zum Erstellen von Zertifikaten, die den Computer und kein gehören müssen. Das Schlüsselmaterial ab, das generiert wird, wird im Sicherheitskontext des Sicherheitsprinzipals (Benutzer- oder Computerkonto) verwaltet, die die Anforderung erstellt hat. Wenn ein Administrator eine zertifikatanforderung im Auftrag von einem Computer erstellt, muss das Schlüsselmaterial in Sicherheitskontexts des Computers und der Sicherheitskontext nicht der Administrator erstellt werden. Der Computer konnte, andernfalls nicht seinen privaten Schlüssel zugreifen, da er im Sicherheitskontext des Administrators wäre.|"true", "false"|MachineKeySet = True</br>Tipp: Der Standardwert ist FALSE.|
|NotBefore|Gibt einen Datums- oder Datums- und vor dem die Anforderung kann nicht ausgegeben werden. NotBefore kann mit ValidityPeriod und ValidityPeriodUnits verwendet werden.|Datum oder Datum und Uhrzeit|NotBefore = "7/24/2012 10:31 AM"</br>Tipp: NotBefore "und" NotAfter "RequestType" sind nur Cert =. Analysieren von Datum versuchen für die Beachtung des Gebietsschemas. Verwenden von Monat Namen werden Mehrdeutigkeiten bei und sollte in den einzelnen Gebietsschemas funktionieren.|
|NotAfter|Gibt einen Datums- oder Datums- und nach dem die Anforderung kann nicht ausgegeben werden. NotAfter kann nicht mit ValidityPeriod oder ValidityPeriodUnits verwendet werden.|Datum oder Datum und Uhrzeit|NotAfter = "9/23/2014 10:31 AM"</br>Tipp: NotBefore "und" NotAfter "RequestType" sind nur Cert =. Analysieren von Datum versuchen für die Beachtung des Gebietsschemas. Verwenden von Monat Namen werden Mehrdeutigkeiten bei und sollte in den einzelnen Gebietsschemas funktionieren.|
|PrivateKeyArchive|Die PrivateKeyArchive Einstellung funktioniert nur, wenn die entsprechende "RequestType" auf "CMC" festgelegt ist, da nur die Certificate Management Nachrichten über Anforderungsformat CMS (CMC) für die Übertragung von der anfordernden Person private Schlüssel sicher an die Zertifizierungsstelle für die schlüsselarchivierung ermöglicht.|"true", "false"|PrivateKeyArchive = True|
|EncryptionAlgorithm|Der Verschlüsselungsalgorithmus zu verwenden.|Mögliche Optionen variieren je nach Version des Betriebssystems und der Satz der installierten kryptografischen Datenanbieter. Um die Liste der verfügbaren Algorithmen anzuzeigen, führen Sie den Befehl <code>certutil -oid 2 &#124; findstr pwszCNGAlgid</code> der angegebene CSP verwendet, muss auch unterstützen, den angegebenen symmetrischen Verschlüsselungsalgorithmus und die Länge.|EncryptionAlgorithm = 3des|
|EncryptionLength|Länge des zu verwendenden Verschlüsselungsalgorithmus.|Beliebiger Länge, die von der angegebenen "EncryptionAlgorithm" zugelassen wird.|EncryptionLength = 128|
|ProviderName|Der Anbietername ist der Anzeigename des CSP...|Wenn Sie nicht den Anbieternamen des CSP, die Sie verwenden kennen, führen Sie Certutil – Csplist über die Befehlszeile. Der Befehl zeigt die Namen aller CSPs, die auf dem lokalen System verfügbar sind|ProviderName = "Microsoft RSA SChannel Cryptographic Provider"|
|ProviderType|Der Anbietertyp wird zum Auswählen von bestimmter Anbietern, die basierend auf bestimmten Algorithmus-Funktion, wie z. B. "RSA-Full".|Wenn Sie nicht mit den Anbietertyp des CSP, die Sie verwenden kennen, führen Sie Certutil – Csplist von einer Eingabeaufforderung aus. Der Befehl zeigt den Anbietertyp, der alle CSPs, die auf dem lokalen System verfügbar sind.|ProviderType = 1|
|RenewalCert|Wenn Sie müssen zum Erneuern von Zertifikaten, die auf dem System vorhanden ist, in die zertifikatanforderung generiert wird, müssen Sie die Zertifikat-Hash als Wert für diesen Schlüssel angeben.|Der Zertifikat-Hash eines Zertifikats, das auf dem Computer verfügbar ist, in die zertifikatanforderung erstellt wird. Wenn Sie nicht, dass den Zertifikat-Hash wissen, das Zertifikate-MMC-Snap-In verwenden Sie, und sehen Sie sich das Zertifikat, das erneuert werden soll. Öffnen Sie die Zertifikateigenschaften, und finden Sie das Attribut "Fingerabdruck" des Zertifikats. Zertifikaterneuerung erfordert entweder eine PKCS #7 oder eine CMC Anforderungsformat.|RenewalCert = 4EDF274BD2919C6E9EC6A522F0F3B153E9B1582D|
|RequesterName</br>Hinweis: Dadurch wird die Anforderung an die im Auftrag einer anderen Anforderung des Benutzers zu registrieren. Die Anforderung muss außerdem mit einem Enrollment Agent-Zertifikat signiert sein, oder die Zertifizierungsstelle wird die Anforderung abzulehnen. Verwenden der - Cert-Option, um das Zertifikat des Enrollment Agents anzugeben.|Der Name des Auftraggebers kann für zertifikatanforderungen angegeben werden, wenn das "RequestType" PKCS #7 oder CMC festgelegt ist. Wenn das "RequestType" PKCS # 10 festgelegt ist, wird dieser Schlüssel ignoriert. Die Requestername kann nur als Teil der Anforderung festgelegt werden. Sie können nicht die Requestername in eine ausstehende Anforderung bearbeiten.|Domain\User|Requestername = "Contoso\BSmith"|
|RequestType|Bestimmt, der Standard, der zum Generieren und senden die zertifikatanforderung verwendet wird.|PKCS10 -- 1</br>PKCS7 -- 2</br>CMC -- 3</br>CERT: 4</br>SCEP - fd00 (64768)</br>Tipp: Diese Option gibt an, ein selbstsigniertes oder selbst ausgestellte Zertifikat. Es wird nicht generiert werden, eine Anforderung, jedoch stattdessen ein neues Zertifikat und installiert anschließend das Zertifikat. Selbstsigniert ist die Standardeinstellung. Geben Sie ein Signaturzertifikat mit – Cert-Option aus, um ein selbst ausgestelltes Zertifikat zu erstellen, die nicht selbstsigniert ist.|RequestType = CMC|
|SecurityDescriptor</br>Tipp: Dies gilt nur für nicht-Smartcard von Computerschlüsseln-Kontext.|Enthält die Sicherheitsinformationen sicherungsfähige Objekte zugeordnet. Für die meisten sicherungsfähige Objekte können Sie die Sicherheitsbeschreibung eines Objekts im Funktionsaufruf angeben, die das Objekt erstellt.|Zeichenfolgen basierend auf [SDDL](https://msdn.microsoft.com/library/aa379567(v=vs.85).aspx).|SecurityDescriptor = "D:P(A;;GA;;;SY)(A;;GA;;;BA)"|
|AlternateSignatureAlgorithm|Gibt an, und ruft einen booleschen Wert, der angibt, ob die Signatur-Algorithmus Objekt-ID (OID) für eine PKCS #10-Anforderung oder ein Zertifikat Signatur diskrete oder kombiniert wird.|"true", "false"|AlternateSignatureAlgorithm = "false"</br>Tipp: Für ein RSA-Signatur gibt "false" eine Pkcs1 v1. 5 an. True gibt an, eine v2. 1-Signatur.|
|Unbeaufsichtigt|Standardmäßig ermöglicht diese Option die CSP-Zugriffs auf die interaktiven Desktop und Anforderung Benutzerinformationen wie z. B. eine Smartcard-PIN des Benutzers. Wenn dieser Schlüssel auf "true" festgelegt ist, wird der CSP muss nicht mit dem Desktop interagieren und über eine Benutzeroberfläche anzuzeigen, für den Benutzer blockiert werden.|"true", "false"|Automatische = True|
|SMIME|Wenn dieser Parameter auf "true" festgelegt ist, wird die Anforderung eine Erweiterung mit der Objekt-ID-Wert 1.2.840.113549.1.9.15 hinzugefügt. Die Anzahl von Objektbezeichnern hängt von der auf die Version des Betriebssystems installiert und den CSP-Funktion, die Verschlüsselungsalgorithmen mit symmetrischen verweisen, die von Secure Multipurpose Internet Mail Extensions (S/MIME)-Anwendungen wie Outlook verwendet werden kann.|"true", "false"|SMIME = True|
|UseExistingKeySet|Dieser Parameter wird verwendet, um anzugeben, dass ein vorhandenes Schlüsselpaar verwendet werden soll, erstellen Sie eine zertifikatanforderung. Wenn dieser Schlüssel auf "true" festgelegt ist, müssen Sie auch einen Wert für den RenewalCert-Schlüssel oder den KeyContainer-Namen angeben. Den Schlüssel exportierbar darf nicht festgelegt werden, da Sie nicht die Eigenschaften eines vorhandenen Schlüssels ändern können. In diesem Fall wird keine Schlüsselmaterial generiert, wenn die zertifikatanforderung erstellt wird.|"true", "false"|UseExistingKeySet = True|
|KeyProtection|Gibt einen Wert, der angibt, wie ein privater Schlüssel vor der Verwendung geschützt ist.|XCN_NCRYPT_UI_NO_PROTCTION_FLAG -- 0</br>XCN_NCRYPT_UI_PROTECT_KEY_FLAG -- 1</br>XCN_NCRYPT_UI_FORCE_HIGH_PROTECTION_FLAG -- 2|KeyProtection = NCRYPT_UI_FORCE_HIGH_PROTECTION_FLAG|
|SuppressDefaults|Gibt einen booleschen Wert, der angibt, ob die standarderweiterungen und Attribute in der Anforderung enthalten sind. Die Standardeinstellungen werden durch ihre Objekt-IDs (OIDs) dargestellt.|"true", "false"|SuppressDefaults = true|
|FriendlyName|Ein Anzeigename für das neue Zertifikat.|Text|FriendlyName = "Server1"|
|ValidityPeriodUnits</br>Hinweis: Hiermit wird nur bei die Anforderung geben Cert =.|Gibt eine Anzahl von Einheiten, die mit ValidityPeriod verwendet werden soll.|Numerisch|ValidityPeriodUnits = 3|
|ValidityPeriod</br>Hinweis: Hiermit wird nur bei die Anforderung geben Cert =.|VValidityPeriod muss eine US-Englisch im plural Zeitraum sein.|Jahre, Monate, Wochen, Tage, Stunden, Minuten, Sekunden|ValidityPeriod = Jahre|

Wechseln Sie zurück zur [Inhalt](#BKMK_Contents)

**[Erweiterungen]**

Dieser Abschnitt ist optional.

|OID-Erweiterung|Definition|Wert|Beispiel|
|-------------|----------|-----|-------|
|2.5.29.17|||2.5.29.17 = "{text}"|
|_continue_|||_continue_ = "UPN=User@Domain.com&"|
|_continue_|||_continue_ = "EMail=User@Domain.com&"|
|_continue_|||_continue_ = "DNS=host.domain.com&"|
|_continue_|||_continue_ = "DirectoryName=CN=Name,DC=Domain,DC=com&"|
|_continue_|||_weiterhin_ = "URL =http://host.domain.com/default.html&"|
|_continue_|||_continue_ = "IPAddress=10.0.0.1&"|
|_continue_|||_weiterhin_ = "RegisteredId 1.2.3.4.5 = &"|
|_continue_|||_weiterhin_ = "1.2.3.4.6.1={utf8}String &"|
|_continue_|||_continue_ = "1.2.3.4.6.2={octet}AAECAwQFBgc=&"|
|_continue_|||_continue_ = "1.2.3.4.6.2={octet}{hex}00 01 02 03 04 05 06 07&"|
|_continue_|||_continue_ = "1.2.3.4.6.3={asn}BAgAAQIDBAUGBw==&"|
|_continue_|||_continue_ = "1.2.3.4.6.3={hex}04 08 00 01 02 03 04 05 06 07"|
|2.5.29.37|||2.5.29.37="{text}"|
|_continue_|||_weiterhin_ = "1.3.6.1.5.5.7.|
|_continue_|||_continue_ = "1.3.6.1.5.5.7.3.1"|
|2.5.29.19|||"{text}ca=0pathlength=3"|
|Kritisch|||Kritische 2.5.29.19 =|
|KeySpec|||AT_NONE -- 0</br>AT_SIGNATURE -- 2</br>AT_KEYEXCHANGE -- 1|
|RequestType|||PKCS10 -- 1</br>PKCS7 -- 2</br>CMC -- 3</br>CERT: 4</br>SCEP - fd00 (64768)|
|KeyUsage|||CERT_DIGITAL_SIGNATURE_KEY_USAGE -- 80 (128)</br>CERT_NON_REPUDIATION_KEY_USAGE -- 40 (64)</br>CERT_KEY_ENCIPHERMENT_KEY_USAGE -- 20 (32)</br>CERT_DATA_ENCIPHERMENT_KEY_USAGE -- 10 (16)</br>CERT_KEY_AGREEMENT_KEY_USAGE -- 8</br>CERT_KEY_CERT_SIGN_KEY_USAGE -- 4</br>CERT_OFFLINE_CRL_SIGN_KEY_USAGE -- 2</br>CERT_CRL_SIGN_KEY_USAGE -- 2</br>CERT_ENCIPHER_ONLY_KEY_USAGE -- 1</br>CERT_DECIPHER_ONLY_KEY_USAGE -- 8000 (32768)|
|KeyUsageProperty|||NCRYPT_ALLOW_DECRYPT_FLAG -- 1</br>NCRYPT_ALLOW_SIGNING_FLAG -- 2</br>NCRYPT_ALLOW_KEY_AGREEMENT_FLAG -- 4</br>NCRYPT_ALLOW_ALL_USAGES -- ffffff (16777215)|
|KeyProtection|||NCRYPT_UI_NO_PROTECTION_FLAG -- 0</br>NCRYPT_UI_PROTECT_KEY_FLAG -- 1</br>NCRYPT_UI_FORCE_HIGH_PROTECTION_FLAG -- 2|
|SubjectNameFlags|Vorlage||CT_FLAG_SUBJECT_REQUIRE_COMMON_NAME -- 40000000 (1073741824)</br>CT_FLAG_SUBJECT_REQUIRE_DIRECTORY_PATH -- 80000000 (2147483648)</br>CT_FLAG_SUBJECT_REQUIRE_DNS_AS_CN -- 10000000 (268435456)</br>CT_FLAG_SUBJECT_REQUIRE_EMAIL--20000000 (536870912)</br>CT_FLAG_OLD_CERT_SUPPLIES_SUBJECT_AND_ALT_NAME -- 8</br>CT_FLAG_SUBJECT_ALT_REQUIRE_DIRECTORY_GUID -- 1000000 (16777216)</br>CT_FLAG_SUBJECT_ALT_REQUIRE_DNS -- 8000000 (134217728)</br>CT_FLAG_SUBJECT_ALT_REQUIRE_DOMAIN_DNS -- 400000 (4194304)</br>CT_FLAG_SUBJECT_ALT_REQUIRE_EMAIL--4000000 (67108864)</br>CT_FLAG_SUBJECT_ALT_REQUIRE_SPN--800000 (8388608)</br>CT_FLAG_SUBJECT_ALT_REQUIRE_UPN -- 2000000 (33554432)|
|X500NameFlags|||CERT_NAME_STR_NONE -- 0</br>CERT_OID_NAME_STR -- 2</br>CERT_X500_NAME_STR -- 3</br>CERT_NAME_STR_SEMICOLON_FLAG -- 40000000 (1073741824)</br>CERT_NAME_STR_NO_PLUS_FLAG -- 20000000 (536870912)</br>CERT_NAME_STR_NO_QUOTING_FLAG -- 10000000 (268435456)</br>CERT_NAME_STR_CRLF_FLAG -- 8000000 (134217728)</br>CERT_NAME_STR_COMMA_FLAG -- 4000000 (67108864)</br>CERT_NAME_STR_REVERSE_FLAG -- 2000000 (33554432)</br>CERT_NAME_STR_FORWARD_FLAG -- 1000000 (16777216)</br>CERT_NAME_STR_DISABLE_IE4_UTF8_FLAG -- 10000 (65536)</br>CERT_NAME_STR_ENABLE_T61_UNICODE_FLAG -- 20000 (131072)</br>CERT_NAME_STR_ENABLE_UTF8_UNICODE_FLAG -- 40000 (262144)</br>CERT_NAME_STR_FORCE_UTF8_DIR_STR_FLAG -- 80000 (524288)</br>CERT_NAME_STR_DISABLE_UTF8_DIR_STR_FLAG -- 100000 (1048576)</br>CERT_NAME_STR_ENABLE_PUNYCODE_FLAG -- 200000 (2097152)|

Wechseln Sie zurück zur [Inhalt](#BKMK_Contents)

> [!NOTE]
> SubjectNameFlags ermöglicht die INF-Datei, um anzugeben, welche Felder "Betreff" und "SubjectAltName-Erweiterung von Certreq basierend auf den aktuellen Benutzer oder die aktuellen Computereigenschaften automatisch ausgefüllt werden soll: DNS-Name, UPN und So weiter. Verwenden das Literal "Template" bedeutet, dass die Vorlage Namen Flags stattdessen verwendet werden. Dadurch wird eine einzelne INF-Datei in mehreren Kontexten verwendet werden, um Anforderungen mit kontextspezifische Antragstellerinformationen zu generieren.
>
> X500NameFlags gibt an, dass die Flags, die direkt an CertStrToName-API übergeben werden, wenn der Betreff-INF-Schlüssel-Wert in ein ASN. 1 konvertiert wird, definierten Namen codiert.

Anfordern eines Zertifikats basiert, mithilfe von Certreq – new verwenden Sie die Schritte im folgenden Beispiel:

> [!WARNING]
> Der Inhalt für dieses Thema basiert auf den Standardeinstellungen für Windows Server 2008 AD CS; Wenn z. B. die Länge des Schlüssels, auf 2048, Microsoft Software Key Storage Provider als CSP auswählen und mithilfe des Secure Hash Algorithm 1 (SHA1). Bewerten Sie die Auswahl auf die Anforderungen der Sicherheitsrichtlinie Ihres Unternehmens.

So erstellen Sie eine Kopie der Richtliniendatei (.inf), und speichern Sie das Beispiel unten im Editor, und speichern als RequestConfig.inf:
```
[NewRequest] 
Subject = "CN=<FQDN of computer you are creating the certificate>" 
Exportable = TRUE 
KeyLength = 2048 
KeySpec = 1 
KeyUsage = 0xf0 
MachineKeySet = TRUE 
[RequestAttributes]
CertificateTemplate="WebServer"
[Extensions] 
OID = 1.3.6.1.5.5.7.3.1 
OID = 1.3.6.1.5.5.7.3.2  

```
Geben Sie den folgenden Befehl aus, auf dem Computer, die für den Sie ein Zertifikat anfordern:
```
CertReq –New RequestConfig.inf CertRequest.req 

```
Das folgende Beispiel zeigt die Syntax des [Strings]-Abschnitt für die OIDs und anderen schwierig zu interpretieren von Daten implementieren. Das neue {Text} Syntaxbeispiel für die EKU-Erweiterung, die eine durch Trennzeichen getrennte Liste der OIDs verwendet:
```
[Version]
Signature="$Windows NT$

[Strings]
szOID_ENHANCED_KEY_USAGE = "2.5.29.37"
szOID_PKIX_KP_SERVER_AUTH = "1.3.6.1.5.5.7.3.1"
szOID_PKIX_KP_CLIENT_AUTH = "1.3.6.1.5.5.7.3.2"

[NewRequest]
Subject = "CN=TestSelfSignedCert"
Requesttype = Cert

[Extensions]
%szOID_ENHANCED_KEY_USAGE%="{text}%szOID_PKIX_KP_SERVER_AUTH%,"
_continue_ = "%szOID_PKIX_KP_CLIENT_AUTH%"
```
Wechseln Sie zurück zur [Inhalt](#BKMK_Contents)

## <a name="BKMK_accept"></a>Certreq – akzeptieren

```
CertReq -accept [Options] [CertChainFileIn | FullResponseFileIn | CertFileIn]
```
– Akzeptieren Parameter den zuvor generierten privaten Schlüssel mit das ausgestellte Zertifikat verknüpft, und entfernt die ausstehende zertifikatanforderung aus dem System, in dem das Zertifikat angefordert wird (Wenn eine übereinstimmende Anforderung vorhanden ist).

Sie können in diesem Beispiel verwenden, ein Zertifikat manuell zu akzeptieren:
```
certreq -accept certnew.cer 

```

> [!WARNING]
> -Verb zu akzeptieren, dem - Benutzer und -Computer-Optionen anzugeben, ob das Zertifikat installiert wird Benutzer oder Computerkontext installiert werden muss. Wenn Sie in beide Kontexte, die den öffentlichen Schlüssel, die Installation entspricht eine ausstehende Anforderung vorhanden ist, sind diese Optionen nicht erforderlich. Liegt keine ausstehende Anforderung, muss eines der folgenden angegeben werden.

Wechseln Sie zurück zur [Inhalt](#BKMK_Contents)

## <a name="BKMK_policy"></a>Certreq-Richtlinie

```
certreq -policy [-attrib AttributeString] [-binary] [-cert CertID] [RequestFileIn [PolicyFileIn [RequestFileOut [PKCS10FileOut]]]]
```
-   Die Konfigurationsdatei, die die Einschränkungen definiert, die auf ein Zertifizierungsstellenzertifikat angewendet werden, wenn die qualifizierte Unterordnung definiert ist, heißt Policy.inf...
-   Sie finden ein Beispiel für die Policy.inf-Datei in die [Anhang A der Planung und Implementing Cross-Certification und die qualifizierte Unterordnung](https://technet.microsoft.com/library/cc738878(WS.10).aspx) finden Sie im Whitepaper.
-   Wenn Sie die Certreq eingeben-Richtlinie ohne zusätzliche Parameter es wird ein Dialogfeld geöffnet, damit Sie auswählen können, die angeforderte Speicherabbilddatei (Req, cmd-, Txt, der, Cer oder crt). Nachdem Sie die angeforderte Datei auswählen, und klicken Sie auf die Schaltfläche "Öffnen", wird ein weiteres Dialogfeld-Fenster geöffnet, um die INF-Datei auszuwählen.

Sie können in diesem Beispiel verwenden, um eine übergreifende zertifikatanforderung zu erstellen:
```
certreq -policy Certsrv.req Policy.inf newcertsrv.req 

```
Wechseln Sie zurück zur [Inhalt](#BKMK_Contents)

## <a name="BKMK_sign"></a>Certreq – Anmeldung

```
certreq -sign [Options] [RequestFileIn [RequestFileOut]]
```
-   Wenn Sie die Certreq eingeben-Anmeldung ohne zusätzliche Parameter wird es ein Dialogfeld geöffnet, so können Sie die angeforderte Datei (Req, cmd-, Txt, der, Cer oder crt) auswählen.
-   Signieren der Anforderung die qualifizierte Unterordnung unter Umständen Unternehmensadministrator-Anmeldeinformationen. Dies ist eine bewährte Methode für das Signieren der Zertifikate für die qualifizierte Unterordnung ausstellen.
-   Das Zertifikat zum Signieren der Anforderung die qualifizierte Unterordnung wird mithilfe der qualifizierten Unterordnung-Vorlage erstellt. Organisations-Admins müssen die Anforderung signieren oder gewähren von Benutzerberechtigungen für die Personen, die das Zertifikat signiert.
-   Wenn Sie die Anforderung CMC anmelden, müssen Sie damit mehrere Mitarbeiter, die diese Anforderung, je nach den Sicherheitsgrad anzumelden, das die qualifizierte Unterordnung zugeordnet ist.
-   Wenn die übergeordnete ZS, der die qualifizierte untergeordnete Zertifizierungsstelle, die Sie installieren, offline ist, müssen Sie das Zertifizierungsstellenzertifikat aus dem übergeordneten offline für die qualifizierte untergeordnete Zertifizierungsstelle abrufen. Wenn die übergeordnete ZS online ist, geben Sie das ZS-Zertifikat für die qualifizierte untergeordnete Zertifizierungsstelle, während der Installation-Assistent-Zertifikat.

Die Sequenz der unten aufgeführten Befehle erfahren, wie Sie eine neue zertifikatanforderung zu erstellen, Signieren und zu übermitteln:
```
certreq -new policyfile.inf MyRequest.req
certreq -sign MyRequest.req MyRequest_Sign.req
certreq -submit MyRequest_Sign.req MyRequest_cert.cer 

```
Wechseln Sie zurück zur [Inhalt](#BKMK_Contents)

## <a name="BKMK_enroll"></a>Certreq – registrieren

Um ein Zertifikat zu registrieren.
```
certreq –enroll [Options] TemplateName
```
Um ein vorhandenes Zertifikat zu erneuern.
```
certreq –enroll –cert CertId [Options] Renew [ReuseKeys]
```
Sie können nur Zertifikate erneuern, die Zeit, die ungültig sind. Abgelaufene Zertifikate nicht erneuert werden und müssen mit einem neuen Zertifikat ersetzt werden.

Hier sehen Sie ein Beispiel für das Erneuern eines Zertifikats mit der Seriennummer:
```
certreq –enroll -machine –cert "61 2d 3c fe 00 00 00 00 00 05" Renew
```
Hier ein Beispiel für die Registrierung für eine Zertifikatvorlage WebServer mithilfe von Sternchen (*) zum Auswählen des Servers Richtlinie über U/I: aufgerufen
```
certreq -enroll –machine –policyserver * "WebServer"
```
Wechseln Sie zurück zur [Inhalt](#BKMK_Contents)

## <a name="BKMK_Options"></a>Optionen

|Optionen|Beschreibung|
|-------|-----------|
|– alle|ICertRequest:: übermittelt, um zu bestimmen, Codierungstyp zu erzwingen.|
|-attrib \<AttributeString>|Gibt die Name-Wert-Zeichenfolgenpaare, getrennt durch einen Doppelpunkt an.</br>Separate Zeichenfolge von Name-Wert-Paaren mit \n (z. B. Name1:Value1\nName2:Value2).|
|-binary|Formatiert die Ausgabedateien im Binärformat anstatt base64-codiert.|
|-PolicyServer  *\<PolicyServer >*|"ldap: *\<path>*"</br>Fügen Sie den URI bzw. die eindeutige ID für einen Computer mit dem Zertifikatregistrierungs-Webdienst.</br>Um anzugeben, dass Sie eine Datei durchsuchen verwenden möchten, verwenden Sie einfach ein Minuszeichen (-) Vorzeichen für  *\<Policyserver >*.|
|-config \<ConfigString>|Verarbeitet den Vorgang unter Verwendung der Zertifizierungsstelle, die in der Konfigurationszeichenfolge, handelt es sich CAHostName\CAName angegeben. Geben Sie für eine Https-Verbindung die Registrierungsserver-URI ein. Zertifizierungsstelle für den lokalen Computer zu speichern, verwenden Sie ein Minuszeichen (-) anmelden.|
|-Anonym|Verwenden Sie anonyme Anmeldedaten für Zertifikatregistrierungs-Webdienste.|
|-Kerberos|Verwenden Sie Kerberos (Domäne) Anmeldeinformationen für Zertifikatregistrierungs-Webdienste.|
|ClientCertificate -  *\<ClientCertId >*|Ersetzen Sie die  *\<ClientCertID >* mit Fingerabdruck eines Zertifikats, CN, EKU, Vorlage, e-Mail-Adresse, UPN und der neue Name = Wert-Syntax.|
|-UserName  *\<Benutzername >*|Mit dem Zertifikatregistrierungs-Webdienste verwendet. Sie können ersetzen  *\<Benutzername >* mit dem SAM-Name oder die "Domäne\Benutzer". Diese Option ist für die Verwendung mit der Option-p angegeben.|
|-p  *\<Kennwort >*|Mit dem Zertifikatregistrierungs-Webdienste verwendet. Ersatz  *\<Kennwort >* mit des tatsächlichen Benutzerkennworts. Diese Option ist für die Verwendung mit der Option - Benutzername.|
|-Benutzer|Konfiguriert den - Benutzerkontext für eine neue zertifikatanforderung oder gibt an, den Kontext für eine ein Zertifikat akzeptieren. Dies ist der Standard-Kontext, wenn keine in der INF oder der Vorlage angegeben ist.|
|-Computer|Konfiguriert eine neue zertifikatanforderung, oder gibt an, den Kontext für einen Kontext des Computers ein Zertifikatsannahme. Neue Anforderungen muss sie konsistent mit dem MachineKeyset INF-Schlüssel und den Vorlagenkontext. Wenn diese Option nicht angegeben ist, und die Vorlage wird einen Kontext nicht festgelegt, wird standardmäßig der Benutzerkontext.|
|-crl|Enthält die Zertifikatsperrlisten (CRLs) in der Ausgabe in die base64-codierten PKCS #7-Datei durch ZertifizierungskettendateiAus angegeben oder der base64-codierte Datei, die gemäß der Anforderungsdatei-aus.|
|-rpc|Weist der Active Directory-Zertifikatdienste (AD CS) auf eine Server-Verbindung von remote Procedure Call (RPC) anstelle von Distributed COM verwenden|
|-AdminForceMachine|Verwenden Sie den Schlüsselverwaltungsdienst oder Identitätswechsel, um die Anforderung aus dem lokalen Systemkontext senden. Erfordert, dass es sich bei der Aufrufen dieser Option Benutzer Mitglied der lokalen Gruppe Administratoren sein.|
|-RenewOnBehalfOf|Senden Sie eine Verlängerung für den Antragsteller im Signaturzertifikat identifiziert. Hiermit CR_IN_ROBO wird beim Aufrufen von [ICertRequest:: übermittelt](https://technet.microsoft.com/subscriptions/aa385040.aspx)|
|-f|Erzwingen Sie vorhandene Dateien überschrieben werden sollen. Dadurch werden außerdem das Zwischenspeichern von Vorlagen und Richtlinien umgangen.|
|-q|Verwenden von automatischen Modus; Unterdrückt alle interaktive eingabeaufforderungen an.|
|-Unicode-|Schreibt Unicode-Ausgabe bei der Standardausgabe umgeleitet oder über die Pipeline an einen anderen Befehl, die Ihnen hilft, wenn aus Windows PowerShell® Skripts aufgerufen wird).|
|-UnicodeText|Unicode-Ausgabe sendet, wenn Datenblobs und Dateien Schreiben von Text mit base64 codiert werden.|

Wechseln Sie zurück zur [Inhalt](#BKMK_Contents)

## <a name="BKMK_Formats"></a>Formate

|Formate|Beschreibung|
|-------|-----------|
|RequestFileIn|Name der Base64-codierte oder binäre Eingabedatei: PKCS #10-zertifikatanforderung, CMS-zertifikatanforderung, PKCS #7-zertifikaterneuerungsanforderung, x. 509-Zertifikat ist übergreifend zertifizierte oder zertifikatanforderung für KeyGen Tag-Format.|
|RequestFileOut|Dateiname für die Base64-codierte Ausgabe|
|CertFileOut|Base64-codierte X-509 Dateiname.|
|PKCS10FileOut|Für die Verwendung mit der [Certreq-Richtlinie](#BKMK_policy) nur Verb. Base64-codierte PKCS10 Name der Ausgabedatei.|
|CertChainFileOut|Base64-codierte PKCS7-Dateiname.|
|FullResponseFileOut|Name der vollständige Antwort Base64-codierte Datei.|
|PolicyFileIn|Für die Verwendung mit der [Certreq-Richtlinie](#BKMK_policy) nur Verb. INF-Datei, die mit einer Textdarstellung von Erweiterungen, die zum Qualifizieren einer Anforderungs verwendet werden.|

## <a name="BKMK_Examples"></a>Zusätzliche Certreq-Beispiele

Die folgenden Artikel enthalten Beispiele für die Verwendung von Certreq:
-   [Gewusst wie: Anfordern eines Zertifikats mit einem benutzerdefinierten alternativen Antragsstellernamen](https://technet.microsoft.com/library/ff625722.aspx)
-   [Testumgebungsanleitung: Bereitstellen einer AD CS Zweistufen-PKI-Hierarchie](https://technet.microsoft.com/library/hh831348.aspx)
-   [Anhang 3: Certreq.exe Syntax](https://technet.microsoft.com/library/cc736326.aspx)
-   [Vorgehensweise: Erstellen Sie ein Web-Server SSL-Zertifikat manuell](http://blogs.technet.com/b/pki/archive/2009/08/05/how-to-create-a-web-server-ssl-certificate-manually.aspx)
-   [Fordern Sie ein AMT-Bereitstellungszertifikats über eine Windows Server 2008-Zertifizierungsstelle](https://social.technet.microsoft.com/wiki/contents/articles/request-an-amt-provisioning-certificate-using-a-windows-server-2008-ca.aspx)
-   [Zertifikatregistrierung für System Center Operations Manager-Agent](https://social.technet.microsoft.com/wiki/contents/articles/certificate-enrollment-for-system-center-operations-manager-agent.aspx)
-   [AD CS-Schritt-für-Schritt-Anleitung: Bereitstellung der PKI-Hierarchie mit zwei Ebenen](https://social.technet.microsoft.com/wiki/contents/articles/15037.ad-cs-step-by-step-guide-two-tier-pki-hierarchy-deployment.aspx)
-   [Gewusst wie: Aktivieren von LDAP über SSL mit einer Drittanbieter-Zertifizierungsstelle](https://support.microsoft.com/kb/321051)

Wechseln Sie zurück zur [Inhalt](#BKMK_Contents)
