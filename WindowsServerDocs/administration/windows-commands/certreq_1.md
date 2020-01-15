---
title: certreq
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 8e3c98fd965fc6923c6af7893261bd1e0eee7d8b
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/14/2020
ms.locfileid: "75947593"
---
# <a name="certreq"></a>certreq



Certreq kann zum Anfordern von Zertifikaten von einer Zertifizierungsstelle (Certification Authority, ca) verwendet werden, um eine Antwort auf eine vorherige Anforderung von einer Zertifizierungsstelle abzurufen, um eine neue Anforderung aus einer INF-Datei zu erstellen, um eine Antwort auf eine Anforderung zu akzeptieren und zu installieren, um eine Kreuz Zertifizierung zu erstellen oder qualifizierte Unterordnungs Anforderung von einem vorhandenen Zertifizierungsstellen Zertifikat oder einer vorhandenen Zertifizierungsstelle, und zum Signieren einer Kreuz Zertifizierungsstelle oder einer qualifizierten Unterordnungs Anforderung.

> [!WARNING]
> - In früheren Versionen von Certreq werden möglicherweise nicht alle Optionen bereitgestellt, die in diesem Dokument beschrieben werden. Sie können alle Optionen, die eine bestimmte Version von Certreq bereitstellt, anzeigen, indem Sie die im Abschnitt Syntax Notations aufgeführten Befehle ausführen.
> - Certreq bietet keine Unterstützung für das Erstellen einer neuen Zertifikat Anforderung auf Grundlage einer Schlüssel Nachweis Vorlage in einer CEP/CES-Umgebung.

## <a name="BKMK_Contents"></a>Inhalt

Die Hauptabschnitte dieses Artikels lauten wie folgt:
1.  [Verbund](#BKMK_Verbs)
2.  [Syntax Notationen](#BKMK_notation)
3.  [Optionen](#BKMK_Options)
4.  [Media](#BKMK_Formats)
5.  [Weitere Certreq-Beispiele](#BKMK_Examples)

## <a name="BKMK_Verbs"></a>Verbund

In der folgenden Tabelle werden die Verben beschrieben, die mit dem Certreq-Befehl verwendet werden können.

|Ändern Sie die Option|Beschreibung|
|------|-----------|
|-Übermitteln|Sendet eine Anforderung an eine Zertifizierungsstelle. Weitere Informationen finden Sie unter [certreq-Submit](#BKMK_Submit).|
|\- *RequestId* abrufen|Ruft eine Antwort auf eine vorherige Anforderung von einer Zertifizierungsstelle ab. Weitere Informationen finden Sie unter [certreq-retrieve](#BKMK_Retrieve).|
|-Neu|Erstellt eine neue Anforderung aus einer INF-Datei. Weitere Informationen finden Sie unter [certreq-new](#BKMK_New).|
|-Accept|Akzeptiert eine Antwort auf eine Zertifikat Anforderung und installiert sie. Weitere Informationen finden Sie unter [certreq-Accept](#BKMK_accept).|
|-Richtlinie|Legt die Richtlinie für eine Anforderung fest. Weitere Informationen finden Sie unter [certreq-policy](#BKMK_policy).|
|-Sign|Signiert eine Kreuz Zertifizierung oder eine qualifizierte Unterordnungs Anforderung. Weitere Informationen finden Sie unter [certreq-Sign](#BKMK_sign).|
|-Registrieren|Hiermit wird ein Zertifikat registriert oder erneuert. Weitere Informationen finden Sie unter [certreq-ENROLL](#BKMK_enroll).|
|-?|Zeigt eine Liste der Certreq-Syntax, Optionen und Beschreibungen an.|
|*\<Verb >* -?|Zeigt die Hilfe für das angegebene Verb an.|
|-v-?|Zeigt eine ausführliche Liste der Certreq-Syntax, Optionen und Beschreibungen an.|

Zurück zum [Inhalt](#BKMK_Contents)

## <a name="BKMK_notation"></a>Syntax Notationen

-   Führen Sie für die grundlegende Befehlszeilen Syntax `certreq -?`
-   Führen Sie **certreq** *\<Verb >* **-?** aus, um die Syntax für die Verwendung von certutil mit einem bestimmten Verb zu verwenden.
-   Um die gesamte certutil-Syntax in eine Textdatei zu senden, führen Sie die folgenden Befehle aus:  
    -   `certreq -v -? > certreqhelp.txt`
    -   `notepad certreqhelp.txt`

In der folgenden Tabelle wird die Notation beschrieben, mit der die Befehlszeilen Syntax angegeben wird.

|Notation|Beschreibung|
|--------|-----------|
|Text ohne eckige Klammern oder geschweifte Klammern|Elemente, die Sie eingeben müssen, wie gezeigt|
|\<Text in spitzen Klammern >|Platzhalter, für den Sie einen Wert angeben müssen|
|[Text in eckigen Klammern]|Optionale Elemente|
|{Text in geschweiften Klammern}|Satz erforderlicher Elemente; Wählen Sie einen aus|
|Senkrechter Strich&#124;()|Trennzeichen für sich gegenseitig ausschließende Elemente Wählen Sie einen aus|
|Auslassungspunkte (…)|Elemente, die wiederholt werden können|

Zurück zum [Inhalt](#BKMK_Contents)

## <a name="BKMK_Submit"></a>Certreq-Submit

Dies ist der Standardparameter "Certreq. exe". wenn keine Option explizit an der Eingabeaufforderung angegeben wird, versucht Certreq. exe, eine Zertifikat Anforderung an eine Zertifizierungsstelle zu übermitteln.
```
CertReq [-Submit] [Options] [RequestFileIn [CertFileOut [CertChainFileOut [FullResponseFileOut]]]]
```
Sie müssen eine Zertifikat Anforderungs Datei angeben, wenn Sie die Option – Submit verwenden. Wenn dieser Parameter ausgelassen wird, wird ein gängiges Fenster zum Öffnen von Dateien angezeigt, in dem Sie die entsprechende Zertifikat Anforderungs Datei auswählen können.

Sie können diese Beispiele als Ausgangspunkt verwenden, um die Anforderung zum Übermitteln von Zertifikaten zu erstellen:

Verwenden Sie das folgende Beispiel, um eine einfache Zertifikat Anforderung zu übermitteln:
```
certreq –submit certRequest.req certnew.cer certnew.pfx
```
Wenn Sie ein Zertifikat anfordern möchten, indem Sie das San-Attribut angeben, lesen Sie die ausführlichen Schritte im Microsoft Knowledge Base-Artikel 931351 [Hinzufügen eines alternativen Antragsteller namens zu einem sicheren LDAP-Zertifikat](https://support.microsoft.com/kb/931351) im Abschnitt "Verwenden des Hilfsprogramms" Certreq. exe "zum Erstellen und Übermitteln einer Zertifikat Anforderung mit einem San-Abschnitt.

Zurück zum [Inhalt](#BKMK_Contents)

## <a name="BKMK_Retrieve"></a>Certreq-Abruf

```
certreq -retrieve [Options] RequestId [CertFileOut [CertChainFileOut [FullResponseFileOut]]]
```
-   Wenn Sie das Dialogfeld CAComputername oder CAName in-config cacomputername\canamea nicht angeben, wird eine Liste aller verfügbaren Zertifizierungsstellen angezeigt.
-   Wenn Sie -config - statt -config Name des Zertifizierungsstellencomputers\Name der Zertifizierungsstelle verwenden, wird der Vorgang mit der Standardzertifizierungsstelle verarbeitet.
-   Sie können certreq-retrieve *RequestId* verwenden, um das Zertifikat abzurufen, nachdem es von der Zertifizierungsstelle tatsächlich ausgestellt wurde. Das *RequestId-* PKC kann ein Dezimal-oder hexadezimal mit einem 0x-Präfix sein, und es kann sich um eine Zertifikat Seriennummer ohne 0x-Präfix Sie können damit auch alle Zertifikate abrufen, die von der Zertifizierungsstelle ausgestellt wurden, einschließlich widerrufener oder abgelaufener Zertifikate, ohne Rücksicht darauf, ob die Anforderung des Zertifikats jemals den Status "Ausstehend" hatte.
-   Wenn Sie eine Anforderung an die Zertifizierungsstelle senden, kann das Richtlinien Modul der Zertifizierungsstelle die Anforderung in einen ausstehenden Status versetzt und die *RequestId* zur Anzeige an den Certreq-Aufrufer zurückgeben. Schließlich gibt der Administrator der Zertifizierungsstelle das Zertifikat aus oder lehnt die Anforderung ab.

Der folgende Befehl ruft die Zertifikat-ID 20 ab und erstellt die Zertifikatsdatei (CER-Datei):
```
certreq -retrieve 20 MyCertificate.cer 
```
Zurück zum [Inhalt](#BKMK_Contents)

## <a name="BKMK_New"></a>Certreq-New

```
certreq -new [Options] [PolicyFileIn [RequestFileOut]]
```
Da in der INF-Datei ein umfassender Satz an Parametern und Optionen angegeben werden kann, ist es schwierig, eine Standardvorlage zu definieren, die Administratoren für alle Zwecke verwenden sollten. In diesem Abschnitt werden daher alle Optionen beschrieben, mit denen Sie eine INF-Datei erstellen können, die auf Ihre spezifischen Anforderungen zugeschnitten ist. Die folgenden Schlüsselwörter werden verwendet, um die INF-Dateistruktur zu beschreiben.
1.  Ein *Abschnitt* ist ein Bereich in der INF-Datei, der eine logische Gruppe von Schlüsseln behandelt. Ein Abschnitt wird immer in eckigen Klammern in der INF-Datei angezeigt.
2.  Ein *Schlüssel* ist der-Parameter auf der linken Seite des Gleichheitszeichens.
3.  Ein- *Wert* ist der-Parameter auf der rechten Seite des Gleichheitszeichens.

Eine minimale INF-Datei würde z. b. wie folgt aussehen:
```
[NewRequest] 
; At least one value must be set in this section 
Subject = "CN=W2K8-BO-DC.contoso2.com"
```
Im folgenden finden Sie einige der möglichen Abschnitte, die der INF-Datei hinzugefügt werden können:

**[Newrequest]**

Dieser Abschnitt ist für eine INF-Datei obligatorisch, die als Vorlage für eine neue Zertifikat Anforderung fungiert. Dieser Abschnitt erfordert mindestens einen Schlüssel mit einem Wert.

|Schlüssel|Definition|Value|Beispiel|
|---|----------|-----|-------|
|Antragsteller|Mehrere Anwendungen basieren auf den Betreff-Informationen in einem Zertifikat. Daher wird empfohlen, einen Wert für diesen Schlüssel anzugeben. Wenn der Betreff hier nicht festgelegt ist, wird empfohlen, dass ein Antragsteller Name als Teil der Zertifikat Erweiterung für den alternativen Antragsteller Namen eingeschlossen wird.|Relative Distinguished Name-Zeichen folgen Werte|Subject = "CN = computer1. Configuration. com" Subject = "CN = John Smith, CN = Users, DC =% $ so, DC = com"|
|Exportable|Wenn dieses Attribut auf true festgelegt ist, kann der private Schlüssel mit dem Zertifikat exportiert werden. Um ein hohes Maß an Sicherheit sicherzustellen, sollten private Schlüssel nicht exportierbar sein. in einigen Fällen ist es jedoch möglicherweise erforderlich, dass der private Schlüssel exportierbar ist, wenn mehrere Computer oder Benutzer denselben privaten Schlüssel gemeinsam verwenden müssen.|true, false|Exportierbar = true. CNG-Schlüssel können zwischen diesem und nur-Text-Text unterscheiden. CAPI1-Schlüssel können nicht.|
|Exportableverschlüsselt|Gibt an, ob der private Schlüssel als exportierbar festgelegt werden soll.|true, false|Exportableverschlüsselt = true</br>Tipp: nicht alle Größen und Algorithmen von öffentlichen Schlüsseln funktionieren mit allen Hash Algorithmen. Der angegebene CSP-CSP muss auch den angegebenen Hash Algorithmus unterstützen. Wenn Sie die Liste der unterstützten Hash Algorithmen anzeigen möchten, können Sie den Befehl ausführen <code>certutil -oid 1 &#124; findstr pwszCNGAlgid &#124; findstr /v CryptOIDInfo</code>|
|HashAlgorithm|Der für diese Anforderung zu verwendende Hash Algorithmus.|SHA256, SHA384, SHA512, SHA1, MD5, MD4, MD2|HashAlgorithm = SHA1. Um die Liste der unterstützten Hash Algorithmen anzuzeigen, verwenden Sie: certutil &#124; -OID 1 findstr pwszcngalgid &#124; findstr/v cryptoidinfo|
|Keyalgorithmus|Der Algorithmus, der vom Dienstanbieter verwendet wird, um ein paar aus einem öffentlichen und einem privaten Schlüssel zu generieren.|RSA, dh, DSA, ECDH_P256, ECDH_P521, ECDSA_P256, ECDSA_P384, ECDSA_P521|Keyalgorithmus = RSA|
|KeyContainer|Es wird nicht empfohlen, diesen Parameter für neue Anforderungen festzulegen, bei denen ein neues Schlüsselmaterial generiert wird. Der Schlüssel Container wird vom System automatisch generiert und verwaltet. Bei Anforderungen, bei denen das vorhandene Schlüsselmaterial verwendet werden soll, kann dieser Wert auf den Schlüssel Container Namen des vorhandenen Schlüssels festgelegt werden. Verwenden Sie den Befehl certutil – Key, um die Liste der verfügbaren Schlüssel Container für den Computer Kontext anzuzeigen. Verwenden Sie den Befehl certutil – Key – User für den Kontext des aktuellen Benutzers.|Zufälliger Zeichen folgen Wert</br>Tipp: Sie sollten für jeden INF-Schlüsselwert, der Leerzeichen oder Sonderzeichen enthält, doppelte Anführungszeichen verwenden, um potenzielle Probleme mit der INF-Verarbeitung zu vermeiden.|Keycontainer = {C347BD28-7F69-4090-AA16-BC58CF4D749C}|
|KeyLength|Definiert die Länge des öffentlichen und des privaten Schlüssels. Die Schlüssellänge wirkt sich auf die Sicherheitsstufe des Zertifikats aus. Eine größere Schlüssellänge bietet in der Regel eine höhere Sicherheitsstufe. Einige Anwendungen haben jedoch möglicherweise Einschränkungen hinsichtlich der Schlüssellänge.|Jede gültige Schlüssellänge, die vom Kryptografiedienstanbieter unterstützt wird.|KeyLength = 2048|
|KeySpec|Bestimmt, ob der Schlüssel für Signaturen, für Exchange (Verschlüsselung) oder für beides verwendet werden kann.|AT_NONE, AT_SIGNATURE AT_KEYEXCHANGE|KeySpec = AT_KEYEXCHANGE|
|Endeinheits Zertifikaten der|Definiert, wofür der Zertifikat Schlüssel verwendet werden soll.|CERT_DIGITAL_SIGNATURE_KEY_USAGE--80 (128)</br>Tipp: die angezeigten Werte sind hexadezimale Werte (Dezimalwerte) für jede bitdefinition. Ältere Syntax kann auch verwendet werden: ein einzelner Hexadezimalwert mit mehreren Bits, der anstelle der symbolischen Darstellung festgelegt ist. Beispiel: KeyUsage = 0xa0.</br>CERT_NON_REPUDIATION_KEY_USAGE--40 (64)</br>CERT_KEY_ENCIPHERMENT_KEY_USAGE--20 (32)</br>CERT_DATA_ENCIPHERMENT_KEY_USAGE--10 (16)</br>CERT_KEY_AGREEMENT_KEY_USAGE--8</br>CERT_KEY_CERT_SIGN_KEY_USAGE--4</br>CERT_OFFLINE_CRL_SIGN_KEY_USAGE--2</br>CERT_CRL_SIGN_KEY_USAGE--2</br>CERT_ENCIPHER_ONLY_KEY_USAGE--1</br>CERT_DECIPHER_ONLY_KEY_USAGE--8000 (32768)|KeyUsage = "CERT_DIGITAL_SIGNATURE_KEY_USAGE &#124; CERT_KEY_ENCIPHERMENT_KEY_USAGE"</br>Tipp: bei mehreren Werten wird ein Pipe&#124;()-Symbol Trennzeichen verwendet. Stellen Sie sicher, dass Sie doppelte Anführungszeichen verwenden, wenn Sie mehrere Werte verwenden, um INF-Probleme zu vermeiden.|
|Keyusageproperty|Ruft einen Wert ab, der den spezifischen Zweck angibt, für den ein privater Schlüssel verwendet werden kann.|NCRYPT_ALLOW_DECRYPT_FLAG--1</br>NCRYPT_ALLOW_SIGNING_FLAG--2</br>NCRYPT_ALLOW_KEY_AGREEMENT_FLAG--4</br>NCRYPT_ALLOW_ALL_USAGES--FFFFFF (16777215)|Keyusageproperty = "NCRYPT_ALLOW_DECRYPT_FLAG &#124; NCRYPT_ALLOW_SIGNING_FLAG"|
|Machinekeyset|Dieser Schlüssel ist wichtig, wenn Sie Zertifikate erstellen müssen, die sich im Besitz des Computers befinden, nicht für einen Benutzer. Das Schlüsselmaterial, das generiert wird, wird im Sicherheitskontext des Sicherheits Prinzipals (Benutzer-oder Computer Konto) verwaltet, von dem die Anforderung erstellt wurde. Wenn ein Administrator im Auftrag eines Computers eine Zertifikat Anforderung erstellt, muss das Schlüsselmaterial im Sicherheitskontext des Computers und nicht im Sicherheitskontext des Administrators erstellt werden. Andernfalls konnte der Computer nicht auf den privaten Schlüssel zugreifen, da er sich im Sicherheitskontext des Administrators befinden würde.|true, false|Machinekeyset = true</br>Tipp: der Standardwert ist false.|
|NotBefore|Gibt ein Datum oder ein Datum und eine Uhrzeit an, bevor die Anforderung nicht ausgegeben werden kann. NotBefore kann mit ValidityPeriod und ValidityPeriodUnits verwendet werden.|Datum oder Datum und Uhrzeit|NotBefore = "7/24/2012 10:31 am"</br>Tipp: NotBefore und NotAfter sind nur für RequestType = CERT vorgesehen. Beim Auswerten von Datumsangaben wird Gebiets Schema unterschieden. Die Verwendung von Monatsnamen wird unterschieden und sollte in jedem Gebiets Schema funktionieren.|
|NotAfter|Gibt ein Datum oder ein Datum und eine Uhrzeit an, nach der die Anforderung nicht mehr ausgegeben werden kann. NotAfter kann nicht mit ValidityPeriod oder ValidityPeriodUnits verwendet werden.|Datum oder Datum und Uhrzeit|NotAfter = "9/23/2014 10:31 am"</br>Tipp: NotBefore und NotAfter sind nur für RequestType = CERT vorgesehen. Beim Auswerten von Datumsangaben wird Gebiets Schema unterschieden. Die Verwendung von Monatsnamen wird unterschieden und sollte in jedem Gebiets Schema funktionieren.|
|Privatekeyarchive|Die privatekeyarchive-Einstellung kann nur verwendet werden, wenn der entsprechende RequestType auf "CMC" festgelegt ist, da nur das Anforderungs Format "Certificate Management messages over CMS (CMC)" die sichere Übertragung des privaten Schlüssels des Anforderers an die Zertifizierungsstelle für die Schlüssel Archivierung ermöglicht.|true, false|Privatekeyarchive = true|
|EncryptionAlgorithm|Der zu verwendende Verschlüsselungsalgorithmus.|Mögliche Optionen sind abhängig von der Betriebssystemversion und dem Satz installierter Kryptografieanbieter. Um die Liste der verfügbaren Algorithmen anzuzeigen, führen Sie den Befehl aus, <code>certutil -oid 2 &#124; findstr pwszCNGAlgid</code> der angegebene CSP auch den angegebenen symmetrischen Verschlüsselungsalgorithmus und die angegebene Länge unterstützen muss.|Verschlüsselungsalgorithmus = 3DES|
|Verschlüsselungs Dauer|Die Länge des zu verwendenden Verschlüsselungsalgorithmus.|Jede vom angegebenen Verschlüsselungsalgorithmus zulässige Länge.|Verschlüsselungslänge = 128|
|ProviderName|Der Anbieter Name ist der Anzeige Name des CSP.|Wenn Sie den Anbieter Namen des von Ihnen verwendeten CSP nicht kennen, führen Sie certutil – csplist über eine Befehlszeile aus. Mit dem Befehl werden die Namen aller CSPs angezeigt, die auf dem lokalen System verfügbar sind.|ProviderName = "Microsoft RSA SChannel Cryptographic Provider"|
|ProviderType|Der Anbietertyp wird verwendet, um bestimmte Anbieter basierend auf einer bestimmten algorithmusfunktion, z. b. "RSA Full", auszuwählen.|Wenn Sie den Anbietertyp des von Ihnen verwendeten CSP nicht kennen, führen Sie certutil – csplist über eine Eingabeaufforderung aus. Der Befehl zeigt den Anbietertyp aller CSPs an, die auf dem lokalen System verfügbar sind.|ProviderType = 1|
|Erneuerungs Zertifikat|Wenn Sie ein Zertifikat erneuern müssen, das auf dem System vorhanden ist, auf dem die Zertifikat Anforderung generiert wird, müssen Sie den Zertifikat Hash als Wert für diesen Schlüssel angeben.|Der Zertifikat Hash eines beliebigen Zertifikats, das auf dem Computer verfügbar ist, auf dem die Zertifikat Anforderung erstellt wurde. Wenn Sie den Zertifikat Hash nicht kennen, verwenden Sie das MMC-Snap-in "Zertifikate", und überprüfen Sie das Zertifikat, das erneuert werden soll. Öffnen Sie die Zertifikat Eigenschaften, und sehen Sie sich das "Thumbprint"-Attribut des Zertifikats an. Für die Zertifikat Erneuerung ist entweder ein PKCS # 7-oder ein CMC-Anforderungs Format erforderlich.|Renewalcert = 4edf 274bd2919c6e9ec6a522f 0F e9b1582d|
|RequesterName</br>Hinweis: Dies bewirkt, dass die Anforderung für eine andere Benutzer Anforderung registriert wird. Die Anforderung muss auch mit einem Registrierungs-Agent-Zertifikat signiert werden, oder die Zertifizierungsstelle lehnt die Anforderung ab. Verwenden Sie die Option-CERT, um das Registrierungs-Agent-Zertifikat anzugeben.|Der Anforderer Name kann für Zertifikat Anforderungen angegeben werden, wenn RequestType auf PKCS # 7 oder CMC festgelegt ist. Wenn RequestType auf PKCS # 10 festgelegt ist, wird dieser Schlüssel ignoriert. Der requestername kann nur als Teil der Anforderung festgelegt werden. Sie können den requestername nicht in einer ausstehenden Anforderung bearbeiten.|Domäne \ Benutzer|Requestername = "contoso\bsmith"|
|RequestType|Bestimmt den Standard, der verwendet wird, um die Zertifikat Anforderung zu generieren und zu senden.|PKCS10--1</br>PKCS7-2</br>CMC--3</br>CERT--4</br>SCEP--fd00 (64768)</br>Tipp: mit dieser Option wird ein selbst signiertes oder selbst ausgestelltes Zertifikat angegeben. Es wird keine Anforderung, sondern ein neues Zertifikat generiert, und das Zertifikat wird installiert. Der Standardwert ist selbst signiert. Geben Sie ein Signaturzertifikat an, indem Sie die Option – CERT verwenden, um ein selbst ausgestelltes Zertifikat zu erstellen, das nicht selbst signiert ist.|RequestType = CMC|
|SecurityDescriptor</br>Tipp: Dies ist nur für Computer Kontext-nicht-Smartcardschlüssel relevant.|Enthält die Sicherheitsinformationen, die Sicherungs fähigen Objekten zugeordnet sind. Bei den meisten Sicherungs fähigen Objekten können Sie die Sicherheits Beschreibung eines Objekts im Funktionsaufruf angeben, von dem das Objekt erstellt wird.|Zeichen folgen, die auf der [Sicherheits Deskriptor-Definitions Sprache](https://msdn.microsoft.com/library/aa379567(v=vs.85).aspx)basieren.|SecurityDescriptor = "d:p (A;; GA;;; SY) (A;; GA;;; BA) "|
|AlternateSignatureAlgorithm|Gibt einen booleschen Wert an, der angibt, ob der Signatur Algorithmus-Objekt Bezeichner (OID) für eine PKCS # 10-Anforderung oder Zertifikat Signatur diskret oder kombiniert ist, oder ruft diesen ab.|true, false|Alternativen Wert von "Alternativen Benutzer" = "false"</br>Tipp: bei einer RSA-Signatur weist false auf eine Pkcs1 v 1.5 hin. True gibt eine v 2.1-Signatur an.|
|Unbeaufsichtigt|Standardmäßig ermöglicht diese Option dem CSP-Zugriff auf den interaktiven Benutzer Desktop und das Anfordern von Informationen, z. b. eine Smartcard-PIN vom Benutzer. Wenn dieser Schlüssel auf true festgelegt ist, darf der CSP nicht mit dem Desktop interagieren und wird daran gehindert, eine Benutzeroberfläche für den Benutzer anzuzeigen.|true, false|Unbeaufsichtigt = true|
|SMIME|Wenn dieser Parameter auf true festgelegt ist, wird der Anforderung eine Erweiterung mit dem Objektbezeichnerwert 1.2.840.113549.1.9.15 hinzugefügt. Die Anzahl der Objekt Bezeichner hängt von der installierten Betriebssystemversion und der CSP-Funktion ab, die auf symmetrische Verschlüsselungsalgorithmen verweisen, die möglicherweise von Secure Multipurpose Internet Mail Extensions (S/MIME)-Anwendungen wie Outlook verwendet werden.|true, false|SMIME = true|
|Useexistingkeyset|Dieser Parameter wird verwendet, um anzugeben, dass ein vorhandenes Schlüsselpaar beim Aufbau einer Zertifikat Anforderung verwendet werden soll. Wenn dieser Schlüssel auf true festgelegt ist, müssen Sie auch einen Wert für den renewalcert-Schlüssel oder den keycontainer-Namen angeben. Der exportierbare Schlüssel darf nicht festgelegt werden, da Sie die Eigenschaften eines vorhandenen Schlüssels nicht ändern können. In diesem Fall wird kein Schlüsselmaterial generiert, wenn die Zertifikat Anforderung erstellt wird.|true, false|Useexistingkeyset = true|
|Keyprotection|Gibt einen Wert an, der angibt, wie ein privater Schlüssel vor der Verwendung geschützt wird.|XCN_NCRYPT_UI_NO_PROTCTION_FLAG--0</br>XCN_NCRYPT_UI_PROTECT_KEY_FLAG--1</br>XCN_NCRYPT_UI_FORCE_HIGH_PROTECTION_FLAG--2|Keyprotection = NCRYPT_UI_FORCE_HIGH_PROTECTION_FLAG|
|Suppressdefaults|Gibt einen booleschen Wert an, der angibt, ob die Standard Erweiterungen und Attribute in der Anforderung enthalten sind. Die Standardwerte werden durch ihre Objekt-IDs (OIDs) dargestellt.|true, false|Suppressdefaults = true|
|FriendlyName|Ein Anzeige Name für das neue Zertifikat.|Text|FriendlyName = "Server1"|
|ValidityPeriodUnits</br>Hinweis: Dies wird nur verwendet, wenn der Request Type = CERT lautet.|Gibt eine Anzahl von Einheiten an, die mit ValidityPeriod verwendet werden sollen.|Numerisch|ValidityPeriodUnits = 3|
|ValidityPeriod</br>Hinweis: Dies wird nur verwendet, wenn der Request Type = CERT lautet.|Vvalidityperiod muss ein US-englischer Plural Zeitraum sein.|Jahre, Monate, Wochen, Tage, Stunden, Minuten, Sekunden|ValidityPeriod = Jahre|

Zurück zum [Inhalt](#BKMK_Contents)

**Extensions**

Dieser Abschnitt ist optional.


|  Erweiterungs-OID   | Definition | Value |                                                                                                                                                                                                                                                                                                                                                                                                                      Beispiel                                                                                                                                                                                                                                                                                                                                                                                                                       |
|------------------|------------|-------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    2.5.29.17     |            |       |                                                                                                                                                                                                                                                                                                                                                                                                                2.5.29.17 = "{Text}"                                                                                                                                                                                                                                                                                                                                                                                                                |
|    *continue*    |            |       |                                                                                                                                                                                                                                                                                                                                                                                                        *Continue* = "UPN =User@Domain.com&"                                                                                                                                                                                                                                                                                                                                                                                                         |
|    *continue*    |            |       |                                                                                                                                                                                                                                                                                                                                                                                                       *Continue* = "Email =User@Domain.com&"                                                                                                                                                                                                                                                                                                                                                                                                        |
|    *continue*    |            |       |                                                                                                                                                                                                                                                                                                                                                                                                        *Continue* = "DNS = Host. Domain. com &"                                                                                                                                                                                                                                                                                                                                                                                                         |
|    *continue*    |            |       |                                                                                                                                                                                                                                                                                                                                                                                               *Continue* = "Directoren Name = CN = Name, DC = Domain, DC = com &"                                                                                                                                                                                                                                                                                                                                                                                               |
|    *continue*    |            |       |                                                                                                                                                                                                                                                                                                                                                                                             *Continue* = "URL =<http://host.domain.com/default.html&>"                                                                                                                                                                                                                                                                                                                                                                                              |
|    *continue*    |            |       |                                                                                                                                                                                                                                                                                                                                                                                                         *Continue* = "IPAddress = 10.0.0.1 &"                                                                                                                                                                                                                                                                                                                                                                                                         |
|    *continue*    |            |       |                                                                                                                                                                                                                                                                                                                                                                                                       *Continue* = "registeredid = 1.2.3.4.5 &"                                                                                                                                                                                                                                                                                                                                                                                                       |
|    *continue*    |            |       |                                                                                                                                                                                                                                                                                                                                                                                                      *Continue* = "1.2.3.4.6.1 = {UTF8} String &"                                                                                                                                                                                                                                                                                                                                                                                                      |
|    *continue*    |            |       |                                                                                                                                                                                                                                                                                                                                                                                                  *Continue* = "1.2.3.4.6.2 = {Octett} aaecawqf BGC = &"                                                                                                                                                                                                                                                                                                                                                                                                   |
|    *continue*    |            |       |                                                                                                                                                                                                                                                                                                                                                                                          *Continue* = "1.2.3.4.6.2 = {Octett} {Hex} 00 01 02 03 04 05 06 07 &"                                                                                                                                                                                                                                                                                                                                                                                           |
|    *continue*    |            |       |                                                                                                                                                                                                                                                                                                                                                                                                 *Continue* = "1.2.3.4.6.3 = {ASN} bagaaqidbaugbw = = &"                                                                                                                                                                                                                                                                                                                                                                                                  |
|    *continue*    |            |       |                                                                                                                                                                                                                                                                                                                                                                                           *Continue* = "1.2.3.4.6.3 = {Hex} 04 08 00 01 02 03 04 05 06 07"                                                                                                                                                                                                                                                                                                                                                                                            |
|    2.5.29.37     |            |       |                                                                                                                                                                                                                                                                                                                                                                                                                 2.5.29.37 = "{Text}"                                                                                                                                                                                                                                                                                                                                                                                                                 |
|    *continue*    |            |       |                                                                                                                                                                                                                                                                                                                                                                                                            *Continue* = "1.3.6.1.5.5.7.                                                                                                                                                                                                                                                                                                                                                                                                            |
|    *continue*    |            |       |                                                                                                                                                                                                                                                                                                                                                                                                          *Continue* = "1.3.6.1.5.5.7.3.1"                                                                                                                                                                                                                                                                                                                                                                                                          |
|    2.5.29.19     |            |       |                                                                                                                                                                                                                                                                                                                                                                                                              "{Text} ca = 0pathlength = 3"                                                                                                                                                                                                                                                                                                                                                                                                              |
|     Kritisch     |            |       |                                                                                                                                                                                                                                                                                                                                                                                                                 Kritisch = 2.5.29.19                                                                                                                                                                                                                                                                                                                                                                                                                 |
|     KeySpec      |            |       |                                                                                                                                                                                                                                                                                                                                                                                             AT_NONE--0</br>AT_SIGNATURE--2</br>AT_KEYEXCHANGE--1                                                                                                                                                                                                                                                                                                                                                                                             |
|   RequestType    |            |       |                                                                                                                                                                                                                                                                                                                                                                                   PKCS10--1</br>PKCS7-2</br>CMC--3</br>CERT--4</br>SCEP--fd00 (64768)                                                                                                                                                                                                                                                                                                                                                                                   |
|     Endeinheits Zertifikaten der     |            |       |                                                                                                                                                                                                       CERT_DIGITAL_SIGNATURE_KEY_USAGE--80 (128)</br>CERT_NON_REPUDIATION_KEY_USAGE--40 (64)</br>CERT_KEY_ENCIPHERMENT_KEY_USAGE--20 (32)</br>CERT_DATA_ENCIPHERMENT_KEY_USAGE--10 (16)</br>CERT_KEY_AGREEMENT_KEY_USAGE--8</br>CERT_KEY_CERT_SIGN_KEY_USAGE--4</br>CERT_OFFLINE_CRL_SIGN_KEY_USAGE--2</br>CERT_CRL_SIGN_KEY_USAGE--2</br>CERT_ENCIPHER_ONLY_KEY_USAGE--1</br>CERT_DECIPHER_ONLY_KEY_USAGE--8000 (32768)                                                                                                                                                                                                       |
| Keyusageproperty |            |       |                                                                                                                                                                                                                                                                                                                                            NCRYPT_ALLOW_DECRYPT_FLAG--1</br>NCRYPT_ALLOW_SIGNING_FLAG--2</br>NCRYPT_ALLOW_KEY_AGREEMENT_FLAG--4</br>NCRYPT_ALLOW_ALL_USAGES--FFFFFF (16777215)                                                                                                                                                                                                                                                                                                                                             |
|  Keyprotection   |            |       |                                                                                                                                                                                                                                                                                                                                                                NCRYPT_UI_NO_PROTECTION_FLAG--0</br>NCRYPT_UI_PROTECT_KEY_FLAG--1</br>NCRYPT_UI_FORCE_HIGH_PROTECTION_FLAG--2                                                                                                                                                                                                                                                                                                                                                                 |
| "Subjetnameflags" |  Vorlage  |       |                                                                           CT_FLAG_SUBJECT_REQUIRE_COMMON_NAME--40 Millionen (1073741824)</br>CT_FLAG_SUBJECT_REQUIRE_DIRECTORY_PATH--80 Millionen (2147483648)</br>CT_FLAG_SUBJECT_REQUIRE_DNS_AS_CN--10 Millionen (268435456)</br>CT_FLAG_SUBJECT_REQUIRE_EMAIL--20 Millionen (536870912)</br>CT_FLAG_OLD_CERT_SUPPLIES_SUBJECT_AND_ALT_NAME--8</br>CT_FLAG_SUBJECT_ALT_REQUIRE_DIRECTORY_GUID--1 Million (16777216)</br>CT_FLAG_SUBJECT_ALT_REQUIRE_DNS--8 Millionen (134217728)</br>CT_FLAG_SUBJECT_ALT_REQUIRE_DOMAIN_DNS--400000 (4194304)</br>CT_FLAG_SUBJECT_ALT_REQUIRE_EMAIL--4 Millionen (67108864)</br>CT_FLAG_SUBJECT_ALT_REQUIRE_SPN--800000 (8388608)</br>CT_FLAG_SUBJECT_ALT_REQUIRE_UPN--2 Millionen (33554432)                                                                            |
|  X500NameFlags   |            |       | CERT_NAME_STR_NONE--0</br>CERT_OID_NAME_STR--2</br>CERT_X500_NAME_STR-3</br>CERT_NAME_STR_SEMICOLON_FLAG--40 Millionen (1073741824)</br>CERT_NAME_STR_NO_PLUS_FLAG--20 Millionen (536870912)</br>CERT_NAME_STR_NO_QUOTING_FLAG--10 Millionen (268435456)</br>CERT_NAME_STR_CRLF_FLAG--8 Millionen (134217728)</br>CERT_NAME_STR_COMMA_FLAG--4 Millionen (67108864)</br>CERT_NAME_STR_REVERSE_FLAG--2 Millionen (33554432)</br>CERT_NAME_STR_FORWARD_FLAG--1 Million (16777216)</br>CERT_NAME_STR_DISABLE_IE4_UTF8_FLAG--10000 (65536)</br>CERT_NAME_STR_ENABLE_T61_UNICODE_FLAG--20000 (131072)</br>CERT_NAME_STR_ENABLE_UTF8_UNICODE_FLAG--40000 (262144)</br>CERT_NAME_STR_FORCE_UTF8_DIR_STR_FLAG--80000 (524288)</br>CERT_NAME_STR_DISABLE_UTF8_DIR_STR_FLAG--100000 (1048576)</br>CERT_NAME_STR_ENABLE_PUNYCODE_FLAG--200000 (2097152) |

Zurück zum [Inhalt](#BKMK_Contents)

> [!NOTE]
> Mithilfe von "subjetnameflags" kann die INF-Datei angeben, welche Antragsteller-und Subjektname-Erweiterungs Felder automatisch von "Certreq" basierend auf den Eigenschaften des aktuellen Benutzers oder der aktuellen Computer ausgefüllt werden sollen: DNS-Name, UPN usw. Die Verwendung des Literals "Template" bedeutet, dass stattdessen die Vorlagen Namen-Flags verwendet werden. Dadurch kann eine einzelne INF-Datei in mehreren Kontexten verwendet werden, um Anforderungen mit kontextspezifischen Betreffinformationen zu generieren.
>
> X500NameFlags gibt die Flags an, die direkt an die certstrintoname-API geleitet werden sollen, wenn der Wert des INF-Schlüssel Subjekts in einen ASN. 1-codierten Distinguished Name konvertiert wird.

Verwenden Sie die Schritte aus dem folgenden Beispiel, um ein Zertifikat mit certreq-new anzufordern:

> [!WARNING]
> Der Inhalt dieses Themas basiert auf den Standardeinstellungen für Windows Server 2008 AD CS; Legen Sie z. b. die Schlüssellänge auf 2048 fest, wählen Sie Microsoft Software Key Storage Provider als CSP aus, und verwenden Sie Secure-Hash-Algorithmus 1 (SHA1). Bewerten Sie diese Auswahl mit den Anforderungen der Sicherheitsrichtlinie Ihres Unternehmens.

Zum Erstellen einer Richtlinien Datei (. inf) kopieren Sie das unten stehende Beispiel in Notepad, und speichern Sie es als RequestConfig. inf:
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
Geben Sie auf dem Computer, für den Sie ein Zertifikat anfordern, den folgenden Befehl ein:
```
CertReq –New RequestConfig.inf CertRequest.req 
```
Im folgenden Beispiel wird veranschaulicht, wie die [Strings]-Abschnitts Syntax für OIDs und andere schwer zu interpretierende Daten implementiert werden. Das neue {Text}-Syntax Beispiel für die EKU-Erweiterung, das eine durch Trennzeichen getrennte Liste von OIDs verwendet:
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
Zurück zum [Inhalt](#BKMK_Contents)

## <a name="BKMK_accept"></a>Certreq-Accept

```
CertReq -accept [Options] [CertChainFileIn | FullResponseFileIn | CertFileIn]
```
Der Parameter "– Accept" verknüpft den zuvor generierten privaten Schlüssel mit dem ausgestellten Zertifikat und entfernt die ausstehende Zertifikat Anforderung aus dem System, auf dem das Zertifikat angefordert wird (wenn eine übereinstimmende Anforderung vorliegt).

Sie können dieses Beispiel verwenden, um ein Zertifikat manuell zu akzeptieren:
```
certreq -accept certnew.cer 
```

> [!WARNING]
> Das Verb-Accept-Verb, die-User-und –-Computer Optionen geben an, ob das zu installierende Zertifikat im Benutzer-oder Computer Kontext installiert werden soll. Wenn in einem Kontext eine ausstehende Anforderung vorhanden ist, die mit dem installierten öffentlichen Schlüssel übereinstimmt, werden diese Optionen nicht benötigt. Wenn keine ausstehende Anforderung vorhanden ist, muss eine dieser Angaben angegeben werden.

Zurück zum [Inhalt](#BKMK_Contents)

## <a name="BKMK_policy"></a>Certreq: Richtlinie

```
certreq -policy [-attrib AttributeString] [-binary] [-cert CertID] [RequestFileIn [PolicyFileIn [RequestFileOut [PKCS10FileOut]]]]
```
-   Die Konfigurationsdatei, die die Einschränkungen definiert, die auf ein Zertifizierungsstellen Zertifikat angewendet werden, wenn eine qualifizierte Unterordnung definiert ist, wird als Policy. inf bezeichnet.
-   Ein Beispiel für die Datei Policy. inf finden Sie im [Anhang A des Whitepaper planen und Implementieren der Kreuz Zertifizierung und der qualifizierten Unterordnung](https://technet.microsoft.com/library/cc738878(WS.10).aspx) .
-   Wenn Sie die Certreq-Richtlinie ohne zusätzlichen Parameter eingeben, wird ein Dialogfeld geöffnet, in dem Sie das angeforderte fie (req, CMC, txt, der, CER oder CRT) auswählen können. Nachdem Sie die angeforderte Datei ausgewählt und auf die Schaltfläche Öffnen geklickt haben, wird ein weiteres Dialogfeld geöffnet, in dem Sie die INF-Datei auswählen können.

Sie können dieses Beispiel verwenden, um eine Zertifikat übergreifende Anforderung zu erstellen:
```
certreq -policy Certsrv.req Policy.inf newcertsrv.req 
```
Zurück zum [Inhalt](#BKMK_Contents)

## <a name="BKMK_sign"></a>Certreq-Sign

```
certreq -sign [Options] [RequestFileIn [RequestFileOut]]
```
-   Wenn Sie certreq-Sign ohne zusätzlichen Parameter eingeben, wird ein Dialogfeld geöffnet, in dem Sie die angeforderte Datei (req, CMC, txt, der, CER oder CRT) auswählen können.
-   Das Signieren der qualifizierten Unterordnung erfordert möglicherweise Unternehmens Administrator-Anmelde Informationen. Dies ist eine bewährte Vorgehensweise zum Ausstellen von Signatur Zertifikaten für die qualifizierte Unterordnung.
-   Das Zertifikat, das zum Signieren der qualifizierten Unterordnungs Anforderung verwendet wird, wird mithilfe der qualifizierten Unterordnung Vorlage erstellt. Organisations-Admins müssen die Anforderung signieren oder Benutzerberechtigungen für die Personen erteilen, die das Zertifikat signieren.
-   Wenn Sie die CMC-Anforderung signieren, müssen Sie möglicherweise mehrere Mitarbeiter diese Anforderung signieren, abhängig von der Sicherheitsstufe, die mit der qualifizierten Unterordnung verknüpft ist.
-   Wenn die übergeordnete ZS der qualifizierten untergeordneten Zertifizierungsstelle, die Sie installieren, offline ist, müssen Sie das Zertifizierungsstellen Zertifikat für die qualifizierte untergeordnete Zertifizierungsstelle von der übergeordneten Offline-Zertifizierungsstelle abrufen Wenn die übergeordnete ZS Online ist, geben Sie das Zertifizierungsstellen Zertifikat für die qualifizierte untergeordnete Zertifizierungsstelle während des Installations-Assistenten für die Zertifikat Dienste an.

Die Abfolge der folgenden Befehle zeigt, wie eine neue Zertifikat Anforderung erstellt, signiert und gesendet wird:
```
certreq -new policyfile.inf MyRequest.req
certreq -sign MyRequest.req MyRequest_Sign.req
certreq -submit MyRequest_Sign.req MyRequest_cert.cer 
```
Zurück zum [Inhalt](#BKMK_Contents)

## <a name="BKMK_enroll"></a>Certreq-registrieren

So registrieren Sie sich für ein Zertifikat
```
certreq –enroll [Options] TemplateName
```
So erneuern Sie ein vorhandenes Zertifikat
```
certreq –enroll –cert CertId [Options] Renew [ReuseKeys]
```
Sie können nur Zertifikate erneuern, die Zeit gültig sind. Abgelaufene Zertifikate können nicht erneuert werden und müssen durch ein neues Zertifikat ersetzt werden.

Hier ein Beispiel für das Erneuern eines Zertifikats mit seiner Seriennummer:
```
certreq –enroll -machine –cert "61 2d 3c fe 00 00 00 00 00 05" Renew
```
Hier finden Sie ein Beispiel für die Anmeldung bei einer Zertifikat Vorlage namens Webserver mithilfe von Sternchen (*), um den Richtlinien Server über U/I auszuwählen:
```
certreq -enroll –machine –policyserver * "WebServer"
```
Zurück zum [Inhalt](#BKMK_Contents)

## <a name="BKMK_Options"></a>Optionen

|Optionen|Beschreibung|
|-------|-----------|
|-beliebig|Erzwingen Sie ICertRequest:: Submit, um den Codierungstyp zu bestimmen.|
|-attrb \<AttributeString->|Gibt die Name-Wert-Zeichen folgen Paare an, getrennt durch einen Doppelpunkt.</br>Getrennte Name-Wert-Zeichen folgen Paare mit \n (z. b. Name1: Value1\nName2: Value2).|
|-Binary|Formatiert Ausgabedateien als Binärdaten anstelle von Base64-codiert.|
|-Policyserver *\<policyserver->*|"LDAP: *\<Pfad >* "</br>Fügen Sie den URI oder die eindeutige ID eines Computers ein, auf dem der Zertifikatregistrierungsrichtlinien-Webdienst ausgeführt wird.</br>Um anzugeben, dass Sie eine Anforderungs Datei beim Durchsuchen verwenden möchten, verwenden Sie einfach ein Minuszeichen (-) für *\<policyserver->* .|
|-config \<ConfigString >|Verarbeitet den Vorgang mit der in der Konfigurations Zeichenfolge angegebenen Zertifizierungsstelle, die "cahostname\caname" ist. Geben Sie für eine HTTPS-Verbindung den Registrierungs Server-URI an. Verwenden Sie für die lokale Computerspeicher Zertifizierungsstelle ein Minuszeichen (-).|
|-Anonymous|Verwenden Sie anonyme Anmelde Informationen für Zertifikatregistrierungs-Webdienste.|
|-Kerberos|Verwenden Sie die Kerberos-Anmelde Informationen (Domäne) für Zertifikatregistrierungs-Webdienste.|
|-ClientCertificate *\<clientcertid >*|Sie können den *\<clientcertid->* durch einen Zertifikat Fingerabdruck, CN, EKU, Template, Email, UPN und die neue Syntax Name = Value ersetzen.|
|-Username *\<username >*|Wird mit Zertifikatregistrierungs-Webdiensten verwendet. Sie können *\<username->* durch den SAM-Namen oder "domain\user" ersetzen. Diese Option ist für die Verwendung mit der Option-p vorgesehen.|
|-p *\<Kennwort >*|Wird mit Zertifikatregistrierungs-Webdiensten verwendet. Ersetzen Sie *\<Kennwort >* durch das tatsächliche Benutzer Kennwort. Diese Option ist für die Verwendung mit der Option-username vorgesehen.|
|-Benutzer|Konfiguriert den-Benutzer Kontext für eine neue Zertifikat Anforderung oder gibt den Kontext für eine Zertifikat Annahme an. Dies ist der Standardkontext, wenn kein Wert in der INF-oder-Vorlage angegeben ist.|
|-Computer|Konfiguriert eine neue Zertifikat Anforderung oder gibt den Kontext für eine Zertifikat Annahme für den Computer Kontext an. Bei neuen Anforderungen muss Sie mit dem machinekeyset-INF-Schlüssel und dem Vorlagen Kontext konsistent sein. Wenn diese Option nicht festgelegt ist und die Vorlage keinen Kontext festgelegt, ist der Standardwert der Benutzer Kontext.|
|-CRL|Schließt Zertifikat Sperr Listen (CRLs) in der Ausgabe in die Base64-codierten PKCS-#7 Datei ein, die von "certchainfinileout" angegeben wird, oder in die Base64-codierte Datei, die durch RequestFileOut angegeben wird.|
|-RPC|Weist Active Directory Zertifikat Dienste (AD CS) an, anstelle von verteiltem com eine RPC-Server Verbindung (Remote Procedure Aufruf) zu verwenden.|
|-Adminforcemachine|Verwenden Sie den Schlüsseldienst oder den Identitätswechsel, um die Anforderung aus dem lokalen System Kontext zu übermitteln. Erfordert, dass der Benutzer, der diese Option aufruft, ein Mitglied der lokalen Administratoren ist.|
|-Renewonbehalfof|Übermitteln Sie eine Verlängerung für den Antragsteller, der im Signaturzertifikat identifiziert wird. Dadurch wird CR_IN_ROBO festgelegt, wenn [ICertRequest:: Submit](https://technet.microsoft.com/subscriptions/aa385040.aspx) aufgerufen wird.|
|-f|Erzwingen, dass vorhandene Dateien überschrieben werden. Dadurch werden auch cachingvorlagen und Richtlinien umgangen.|
|-q|Unbeaufsichtigten Modus verwenden; alle interaktiven Eingabe Aufforderungen unterdrücken.|
|-Unicode|Schreibt die Unicode-Ausgabe, wenn die Standardausgabe umgeleitet oder an einen anderen Befehl weitergeleitet wird, was beim Aufrufen von Windows PowerShell-® Skripts hilft).|
|-UnicodeText|Sendet eine Unicode-Ausgabe beim Schreiben von Base64-codierten Daten-blobdaten in Dateien.|

Zurück zum [Inhalt](#BKMK_Contents)

## <a name="BKMK_Formats"></a>Media

|Formate|Beschreibung|
|-------|-----------|
|RequestFileIn|Base64-codierter oder binärer Eingabe Dateiname: PKCS #10 Zertifikat Anforderung, CMS-Zertifikat Anforderung, PKCS #7 Zertifikat Erneuerungs Anforderung, X. 509-Zertifikat für eine Kreuz Zertifizierung oder eine Zertifikat Anforderung im KeyGen-Tagformat.|
|RequestFileOut|Name der Base64-codierten Ausgabedatei|
|CertFileOut|Base64-codierter X-509-Dateiname.|
|PKCS10FileOut|Nur für die Verwendung mit dem [certreq-policy-](#BKMK_policy) Verb. Base64-codierter PKCS10-Ausgabe Dateiname.|
|Certchainfinileout|Base64-codierter PKCS-#7 Dateiname.|
|Fullresponse FileOut|Base64-codierter vollständiger Antwort Dateiname.|
|PolicyFileIn|Nur für die Verwendung mit dem [certreq-policy-](#BKMK_policy) Verb. INF-Datei, die eine Textdarstellung der Erweiterungen enthält, die zum qualifizieren einer Anforderung verwendet werden.|

## <a name="BKMK_Examples"></a>Weitere Certreq-Beispiele

Die folgenden Artikel enthalten Beispiele für die Verwendung von Certreq:
-   [Anfordern eines Zertifikats mit einem benutzerdefinierten Alternativen Antragsteller Namen](https://technet.microsoft.com/library/ff625722.aspx)
-   [Test Umgebungs Anleitung: Bereitstellen einer AD CS-PKI-Hierarchie mit zwei Ebenen](https://technet.microsoft.com/library/hh831348.aspx)
-   [Anhang 3: Syntax von "Certreq. exe"](https://technet.microsoft.com/library/cc736326.aspx)
-   [Manuelles Erstellen eines Webserver-SSL-Zertifikats](https://blogs.technet.com/b/pki/archive/2009/08/05/how-to-create-a-web-server-ssl-certificate-manually.aspx)
-   [Anfordern eines AMT-Bereitstellungs Zertifikats mithilfe einer Windows Server 2008-Zertifizierungsstelle](https://social.technet.microsoft.com/wiki/contents/articles/request-an-amt-provisioning-certificate-using-a-windows-server-2008-ca.aspx)
-   [Zertifikat Registrierung für System Center Operations Manager-Agent](https://social.technet.microsoft.com/wiki/contents/articles/certificate-enrollment-for-system-center-operations-manager-agent.aspx)
-   [Schritt-für-Schritt-Anleitung für AD CS: Bereitstellung der PKI-Hierarchie](https://social.technet.microsoft.com/wiki/contents/articles/15037.ad-cs-step-by-step-guide-two-tier-pki-hierarchy-deployment.aspx)
-   [Aktivieren von LDAP über SSL mit einer Zertifizierungsstelle von Drittanbietern](https://support.microsoft.com/kb/321051)

Zurück zum [Inhalt](#BKMK_Contents)
