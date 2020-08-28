---
title: certreq
description: Referenz Artikel für den Certreq-Befehl der Zertifikate von einer Zertifizierungsstelle (ca) anfordert, eine Antwort auf eine vorherige Anforderung von einer Zertifizierungsstelle abruft, eine neue Anforderung aus einer INF-Datei erstellt, eine Antwort auf eine Anforderung akzeptiert und installiert, eine Kreuz Zertifizierung oder eine qualifizierte Unterordnung von einem vorhandenen Zertifizierungsstellen Zertifikat oder einer vorhandenen Zertifizierungsstelle erstellt und eine Kreuz Zertifizierung oder eine qualifizierte Unterordnungs Anforderung signiert.
ms.topic: reference
ms.assetid: 7a04e51f-f395-4bff-b57a-0e9efcadf973
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: eb910415c46a57353eeffe7168ce71c055d82eca
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89031248"
---
# <a name="certreq"></a>certreq

Der Befehl "Certreq" kann zum Anfordern von Zertifikaten von einer Zertifizierungsstelle (Certification Authority, ca) verwendet werden. so rufen Sie eine Antwort auf eine vorherige Anforderung von einer Zertifizierungsstelle ab, um eine neue Anforderung aus einer INF-Datei zu erstellen, eine Antwort auf eine Anforderung zu akzeptieren und zu installieren, um eine Kreuz Zertifizierung oder eine qualifizierte Unterordnungs Anforderung von einem vorhandenen Zertifizierungsstellen Zertifikat oder einer vorhandenen Zertifizierungsstelle zu erstellen und eine Kreuz Zertifizierung oder eine qualifizierte Unterordnungs Anforderung zu signieren.

> [!IMPORTANT]
> In früheren Versionen des Certreq-Befehls werden möglicherweise nicht alle hier beschriebenen Optionen bereitgestellt. Um die unterstützten Optionen auf der Grundlage bestimmter Versionen von Certreq anzuzeigen, führen Sie die Befehlszeilen Hilfe-Option aus `certreq -v -?` .
>
> Der Certreq-Befehl unterstützt das Erstellen einer neuen Zertifikat Anforderung auf Grundlage einer Schlüssel Nachweis Vorlage nicht, wenn in einer CEP/CES-Umgebung.

> [!WARNING]
> Der Inhalt dieses Themas basiert auf den Standardeinstellungen für Windows Server. Legen Sie z. b. die Schlüssellänge auf 2048 fest, wählen Sie Microsoft Software Key Storage Provider als CSP aus, und verwenden Sie Secure-Hash-Algorithmus 1 (SHA1). Bewerten Sie diese Auswahl mit den Anforderungen der Sicherheitsrichtlinie Ihres Unternehmens.

## <a name="syntax"></a>Syntax

```
certreq [-submit] [options] [requestfilein [certfileout [certchainfileout [fullresponsefileOut]]]]
certreq -retrieve [options] requestid [certfileout [certchainfileout [fullresponsefileOut]]]
certreq -new [options] [policyfilein [requestfileout]]
certreq -accept [options] [certchainfilein | fullresponsefilein | certfilein]
certreq -sign [options] [requestfilein [requestfileout]]
certreq –enroll [options] templatename
certreq –enroll –cert certId [options] renew [reusekeys]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------- | ----------- |
| -übermitteln | Sendet eine Anforderung an eine Zertifizierungsstelle. |
| -Abrufen `<requestid>` | Ruft eine Antwort auf eine vorherige Anforderung von einer Zertifizierungsstelle ab. |
| -neu | Erstellt eine neue Anforderung aus einer INF-Datei. |
| -Accept | Akzeptiert eine Antwort auf eine Zertifikat Anforderung und installiert sie. |
| -Richtlinie | Legt die Richtlinie für eine Anforderung fest. |
| -Sign | Signiert eine Kreuz Zertifizierung oder eine qualifizierte Unterordnungs Anforderung. |
| -Registrieren | Hiermit wird ein Zertifikat registriert oder erneuert. |
| -? | Zeigt eine Liste der Certreq-Syntax, Optionen und Beschreibungen an. |
| `<parameter>` -? | Zeigt die Hilfe für den angegebenen Parameter an. |
| -v-? | Zeigt eine ausführliche Liste der Certreq-Syntax, Optionen und Beschreibungen an. |

## <a name="examples"></a>Beispiele

### <a name="certreq--submit"></a>Certreq-Submit

So übermitteln Sie eine einfache Zertifikat Anforderung:

```
certreq –submit certrequest.req certnew.cer certnew.pfx
```

#### <a name="remarks"></a>Bemerkungen

- Dies ist der Standard certreq.exe Parameter. Wenn an der Eingabeaufforderung keine Option angegeben ist, wird von certreq.exe versucht, eine Zertifikat Anforderung an eine Zertifizierungsstelle zu übermitteln. Sie müssen eine Zertifikat Anforderungs Datei angeben, wenn Sie die Option **– Submit** verwenden. Wenn dieser Parameter ausgelassen wird, wird ein gemeinsames **Datei Öffnungs** Fenster angezeigt, in dem Sie die entsprechende Zertifikat Anforderungs Datei auswählen können.

- Informationen zum Anfordern eines Zertifikats durch Angabe des San-Attributs finden Sie im Abschnitt *Verwenden des certreq.exe Hilfsprogramms zum Erstellen und Übermitteln einer Zertifikat Anforderung* im Microsoft Knowledge Base-Artikel 931351 [How to Add a Subject Alternative Name to a Secure LDAP Certificate](https://support.microsoft.com/kb/931351).

### <a name="certreq--retrieve"></a>Certreq-Abruf

Zum Abrufen der Zertifikat-ID 20 und zum Erstellen einer Zertifikatsdatei (. cer) mit dem Namen *myCertificate*:

```
certreq -retrieve 20 MyCertificate.cer
```

#### <a name="remarks"></a>Bemerkungen

- Verwenden Sie certreq-retrieve *RequestId* , um das Zertifikat abzurufen, nachdem es von der Zertifizierungsstelle ausgestellt wurde. Das *RequestId-* PKC kann ein Dezimal-oder hexadezimal mit einem 0x-Präfix sein, und es kann sich um eine Zertifikat Seriennummer ohne 0x-Präfix Sie können damit auch alle Zertifikate abrufen, die jemals von der Zertifizierungsstelle ausgestellt wurden, einschließlich widerrufener oder abgelaufener Zertifikate, ohne Rücksicht darauf, ob die Anforderung des Zertifikats jemals den Status "Ausstehend" hatte.

- Wenn Sie eine Anforderung an die Zertifizierungsstelle senden, wird die Anforderung vom Richtlinien Modul der Zertifizierungsstelle möglicherweise in den Status "Ausstehend" versetzt und die *RequestId* zur Anzeige an den Certreq-Aufrufer zurückgegeben. Schließlich wird das Zertifikat vom Administrator der Zertifizierungsstelle ausgestellt, oder die Anforderung wird verweigert.

### <a name="certreq--new"></a>Certreq-New

So erstellen Sie eine neue Anforderung:

```
[newrequest]
; At least one value must be set in this section
subject = CN=W2K8-BO-DC.contoso2.com
```

Im folgenden finden Sie einige der möglichen Abschnitte, die der INF-Datei hinzugefügt werden können:

#### <a name="newrequest"></a>[newrequest]

Dieser Bereich der INF-Datei ist für alle neuen Zertifikat Anforderungs Vorlagen obligatorisch und muss mindestens einen Parameter mit einem Wert enthalten.

| Schlüssel<sup>1</sup> | Beschreibung | Wert<sup>2</sup> | Beispiel |
| --- | ---------- | ----- | ------- |
| Gegenstand | Mehrere apps basieren auf den Betreff-Informationen in einem Zertifikat. Es wird empfohlen, einen Wert für diesen Schlüssel anzugeben. Wenn der Betreff hier nicht festgelegt ist, empfiehlt es sich, einen Antragsteller Namen als Teil der Zertifikat Erweiterung für den alternativen Antragsteller Namen einzuschließen. | Relative Distinguished Name-Zeichen folgen Werte | Subject = CN = computer1. "Subject. com subject = CN = John Smith, CN = Users, DC =% $ so, DC = com" |
| Exportable | Wenn der Wert auf true festgelegt ist, kann der private Schlüssel mit dem Zertifikat exportiert werden. Um ein hohes Maß an Sicherheit sicherzustellen, sollten private Schlüssel nicht exportierbar sein. in einigen Fällen ist es jedoch möglicherweise erforderlich, wenn mehrere Computer oder Benutzer denselben privaten Schlüssel gemeinsam verwenden müssen. | `true | false` | `Exportable = TRUE`. CNG-Schlüssel können zwischen diesem und nur-Text-Text unterscheiden. CAPI1 Keys können nicht. |
| Exportableverschlüsselt | Gibt an, ob der private Schlüssel als exportierbar festgelegt werden soll. | `true | false` | `ExportableEncrypted = true`<p>**Tipp:** Nicht alle Größen und Algorithmen von öffentlichen Schlüsseln funktionieren mit allen Hash Algorithmen. Der angegebene CSP muss auch den angegebenen Hash Algorithmus unterstützen. Wenn Sie die Liste der unterstützten Hash Algorithmen anzeigen möchten, können Sie den folgenden Befehl ausführen: `certutil -oid 1 | findstr pwszCNGAlgid | findstr /v CryptOIDInfo` |
| HashAlgorithm | Der für diese Anforderung zu verwendende Hash Algorithmus. | `Sha256, sha384, sha512, sha1, md5, md4, md2` | `HashAlgorithm = sha1`. Um die Liste der unterstützten Hash Algorithmen anzuzeigen, verwenden Sie: certutil-OID 1 | findstr pwszcngalgid | findstr/v cryptoidinfo|
| KeyAlgorithm| Der Algorithmus, der vom Dienstanbieter verwendet wird, um ein paar aus einem öffentlichen und einem privaten Schlüssel zu generieren.| `RSA, DH, DSA, ECDH_P256, ECDH_P521, ECDSA_P256, ECDSA_P384, ECDSA_P521` | `KeyAlgorithm = RSA` |
| KeyContainer | Es wird nicht empfohlen, diesen Parameter für neue Anforderungen festzulegen, bei denen ein neues Schlüsselmaterial generiert wird. Der Schlüssel Container wird vom System automatisch generiert und verwaltet.<p>Bei Anforderungen, bei denen das vorhandene Schlüsselmaterial verwendet werden soll, kann dieser Wert auf den Schlüssel Container Namen des vorhandenen Schlüssels festgelegt werden. Verwenden `certutil –key` Sie den Befehl, um die Liste der verfügbaren Schlüssel Container für den Computer Kontext anzuzeigen. Verwenden Sie den `certutil –key –user` -Befehl für den Kontext des aktuellen Benutzers.| Zufälliger Zeichen folgen Wert<p>**Tipp:** Verwenden Sie doppelte Anführungszeichen um alle INF-Schlüsselwerte, die Leerzeichen oder Sonderzeichen enthalten, um potenzielle Probleme mit der INF-Verarbeitung zu vermeiden. | `KeyContainer = {C347BD28-7F69-4090-AA16-BC58CF4D749C}` |
| KeyLength | Definiert die Länge des öffentlichen und des privaten Schlüssels. Die Schlüssellänge wirkt sich auf die Sicherheitsstufe des Zertifikats aus. Eine größere Schlüssellänge bietet in der Regel eine höhere Sicherheitsstufe. Einige Anwendungen haben jedoch möglicherweise Einschränkungen hinsichtlich der Schlüssellänge. | Jede gültige Schlüssellänge, die vom Kryptografiedienstanbieter unterstützt wird. | `KeyLength = 2048` |
| KeySpec | Bestimmt, ob der Schlüssel für Signaturen, für Exchange (Verschlüsselung) oder für beides verwendet werden kann. | `AT_NONE, AT_SIGNATURE, AT_KEYEXCHANGE` | `KeySpec = AT_KEYEXCHANGE` |
| Endeinheits Zertifikaten der | Definiert, wofür der Zertifikat Schlüssel verwendet werden soll. | <ul><li>`CERT_DIGITAL_SIGNATURE_KEY_USAGE -- 80 (128)`</li><li>`CERT_NON_REPUDIATION_KEY_USAGE -- 40 (64)`</li><li>`CERT_KEY_ENCIPHERMENT_KEY_USAGE -- 20 (32)`</li><li>`CERT_DATA_ENCIPHERMENT_KEY_USAGE -- 10 (16)`</li><li>`CERT_KEY_AGREEMENT_KEY_USAGE -- 8`</li><li>`CERT_KEY_CERT_SIGN_KEY_USAGE -- 4`</li><li>`CERT_OFFLINE_CRL_SIGN_KEY_USAGE -- 2`</li><li>`CERT_CRL_SIGN_KEY_USAGE -- 2`</li><li>`CERT_ENCIPHER_ONLY_KEY_USAGE -- 1`</li><li>`CERT_DECIPHER_ONLY_KEY_USAGE -- 8000 (32768)`</li></ul> | `KeyUsage = CERT_DIGITAL_SIGNATURE_KEY_USAGE | CERT_KEY_ENCIPHERMENT_KEY_USAGE`<p>**Tipp:** Mehrere Werte verwenden eine Pipe (|) Symbol Trennzeichen. Stellen Sie sicher, dass Sie doppelte Anführungszeichen verwenden, wenn Sie mehrere Werte verwenden, um INF-Probleme zu vermeiden. Die angezeigten Werte sind hexadezimale Werte (Dezimalwerte) für jede bitdefinition. Ältere Syntax kann auch verwendet werden: ein einzelner Hexadezimalwert mit mehreren Bits, der anstelle der symbolischen Darstellung festgelegt ist. Beispielsweise `KeyUsage = 0xa0`. |
| Keyusageproperty | Ruft einen Wert ab, der den spezifischen Zweck angibt, für den ein privater Schlüssel verwendet werden kann. | <ul><li>`NCRYPT_ALLOW_DECRYPT_FLAG -- 1`</li><li>`NCRYPT_ALLOW_SIGNING_FLAG -- 2`</li><li>`NCRYPT_ALLOW_KEY_AGREEMENT_FLAG -- 4`</li><li>`NCRYPT_ALLOW_ALL_USAGES -- ffffff (16777215)`</li></ul> | `KeyUsageProperty = NCRYPT_ALLOW_DECRYPT_FLAG | NCRYPT_ALLOW_SIGNING_FLAG` |
| Machinekeyset | Dieser Schlüssel ist wichtig, wenn Sie Zertifikate erstellen müssen, die sich im Besitz des Computers befinden, nicht für einen Benutzer. Das Schlüsselmaterial, das generiert wird, wird im Sicherheitskontext des Sicherheits Prinzipals (Benutzer-oder Computer Konto) verwaltet, von dem die Anforderung erstellt wurde. Wenn ein Administrator im Auftrag eines Computers eine Zertifikat Anforderung erstellt, muss das Schlüsselmaterial im Sicherheitskontext des Computers und nicht im Sicherheitskontext des Administrators erstellt werden. Andernfalls konnte der Computer nicht auf den privaten Schlüssel zugreifen, da er sich im Sicherheitskontext des Administrators befinden würde. | `true | false`. Der Standardwert ist false. | `MachineKeySet = true` |
| NotBefore | Gibt ein Datum oder ein Datum und eine Uhrzeit an, bevor die Anforderung nicht ausgegeben werden kann. `NotBefore` kann mit und verwendet `ValidityPeriod` werden `ValidityPeriodUnits` . | Datum oder Datum und Uhrzeit | `NotBefore = 7/24/2012 10:31 AM`<p>**Tipp:** `NotBefore` und `NotAfter` sind nur für R vorgesehen `equestType=cert` . Beim Auswerten von Datumsangaben wird Gebiets Schema unterschieden. Die Verwendung von Monatsnamen wird unterschieden und sollte in jedem Gebiets Schema funktionieren. |
| NotAfter | Gibt ein Datum oder ein Datum und eine Uhrzeit an, nach der die Anforderung nicht mehr ausgegeben werden kann. `NotAfter` kann nicht mit oder verwendet werden `ValidityPeriod` `ValidityPeriodUnits` . | Datum oder Datum und Uhrzeit | `NotAfter = 9/23/2014 10:31 AM`<p>**Tipp:** `NotBefore` und `NotAfter` sind `RequestType=cert` nur für. Beim Auswerten von Datumsangaben wird Gebiets Schema unterschieden. Die Verwendung von Monatsnamen wird unterschieden und sollte in jedem Gebiets Schema funktionieren. |
| Privatekeyarchive | Die privatekeyarchive-Einstellung kann nur verwendet werden, wenn der entsprechende RequestType auf "CMC" festgelegt ist, da nur das Anforderungs Format "Certificate Management messages over CMS (CMC)" die sichere Übertragung des privaten Schlüssels des Anforderers an die Zertifizierungsstelle für die Schlüssel Archivierung ermöglicht. | `true | false` | `PrivateKeyArchive = true` |
| EncryptionAlgorithm | Der zu verwendende Verschlüsselungsalgorithmus. | Mögliche Optionen sind abhängig von der Betriebssystemversion und dem Satz installierter Kryptografieanbieter. Um die Liste der verfügbaren Algorithmen anzuzeigen, führen Sie den folgenden Befehl aus: `certutil -oid 2 | findstr pwszCNGAlgid` . Der angegebene CSP-verwendet muss auch den angegebenen symmetrischen Verschlüsselungsalgorithmus und die angegebene Länge unterstützen. | `EncryptionAlgorithm = 3des` |
| Verschlüsselungs Dauer | Die Länge des zu verwendenden Verschlüsselungsalgorithmus. | Jede vom angegebenen Verschlüsselungsalgorithmus zulässige Länge. | `EncryptionLength = 128` |
| ProviderName | Der Anbieter Name ist der Anzeige Name des CSP. | Wenn Sie den Anbieter Namen des von Ihnen verwendeten CSP nicht kennen, führen Sie den Befehl über die `certutil –csplist` Befehlszeile aus. Mit dem Befehl werden die Namen aller CSPs angezeigt, die auf dem lokalen System verfügbar sind. | `ProviderName = Microsoft RSA SChannel Cryptographic Provider` |
| ProviderType | Der Anbietertyp wird verwendet, um bestimmte Anbieter basierend auf einer bestimmten algorithmusfunktion, z. b. RSA Full, auszuwählen. | Wenn Sie den Anbietertyp des verwendeten CSP nicht kennen, führen Sie `certutil –csplist` an einer Eingabeaufforderung aus. Der Befehl zeigt den Anbietertyp aller CSPs an, die auf dem lokalen System verfügbar sind. | `ProviderType = 1` |
| Erneuerungs Zertifikat | Wenn Sie ein Zertifikat erneuern müssen, das auf dem System vorhanden ist, auf dem die Zertifikat Anforderung generiert wird, müssen Sie den Zertifikat Hash als Wert für diesen Schlüssel angeben. | Der Zertifikat Hash eines beliebigen Zertifikats, das auf dem Computer verfügbar ist, auf dem die Zertifikat Anforderung erstellt wurde. Wenn Sie den Zertifikat Hash nicht kennen, verwenden Sie das MMC-Snap-in "Zertifikate", und überprüfen Sie das Zertifikat, das erneuert werden soll. Öffnen Sie die Zertifikat Eigenschaften, und sehen Sie sich das- `Thumbprint` Attribut des Zertifikats an. Für die Zertifikat Erneuerung ist entweder ein- `PKCS#7` oder ein- `CMC` Anforderungs Format erforderlich. | `RenewalCert = 4EDF274BD2919C6E9EC6A522F0F3B153E9B1582D` |
| RequesterName | Fordert die Registrierung für eine andere Benutzer Anforderung an. Die Anforderung muss auch mit einem Registrierungs-Agent-Zertifikat signiert werden, oder die Zertifizierungsstelle lehnt die Anforderung ab. Verwenden `-cert` Sie die Option, um das Registrierungs-Agent-Zertifikat anzugeben. Der Anforderer Name kann für Zertifikat Anforderungen angegeben werden `RequestType` , wenn auf oder festgelegt ist `PKCS#7` `CMC` . Wenn `RequestType` auf festgelegt ist `PKCS#10` , wird dieser Schlüssel ignoriert. Der `Requestername` kann nur als Teil der Anforderung festgelegt werden. Sie können `Requestername` in einer ausstehenden Anforderung nicht bearbeiten. | `Domain\User` | `Requestername = Contoso\BSmith` |
| RequestType | Bestimmt den Standard, der verwendet wird, um die Zertifikat Anforderung zu generieren und zu senden. | <ul><li>`PKCS10 -- 1`</li><li>`PKCS7 -- 2`</li><li>`CMC -- 3`</li><li>`Cert -- 4`</li><li>`SCEP -- fd00 (64768)`</li></ul>**Tipp:** Mit dieser Option wird ein selbst signiertes oder selbst ausgestelltes Zertifikat angegeben. Es wird keine Anforderung, sondern ein neues Zertifikat generiert, und das Zertifikat wird installiert. Der Standardwert ist selbst signiert. Geben Sie ein Signaturzertifikat an, indem Sie die Option – CERT verwenden, um ein selbst ausgestelltes Zertifikat zu erstellen, das nicht selbst signiert ist. | `RequestType = CMC` |
| SecurityDescriptor | Enthält die Sicherheitsinformationen, die Sicherungs fähigen Objekten zugeordnet sind. Bei den meisten Sicherungs fähigen Objekten können Sie die Sicherheits Beschreibung eines Objekts im Funktionsaufruf angeben, von dem das Objekt erstellt wird. Zeichen folgen, die auf der [Sicherheits Deskriptor-Definitions Sprache](/windows/win32/secauthz/security-descriptor-definition-language)basieren.<p>**Tipp:** Dies ist nur für Computer Kontext-nicht-Smartcardschlüssel relevant. | `SecurityDescriptor = D:P(A;;GA;;;SY)(A;;GA;;;BA)` |
| AlternateSignatureAlgorithm | Gibt einen booleschen Wert an, der angibt, ob der Signatur Algorithmus-Objekt Bezeichner (OID) für eine PKCS # 10-Anforderung oder Zertifikat Signatur diskret oder kombiniert ist, oder ruft diesen ab. | `true | false` | `AlternateSignatureAlgorithm = false`<p>Gibt für eine RSA-Signatur `false` eine an `Pkcs1 v1.5` , während `true` eine `v2.1` Signatur angibt. |
| Automatisch | Standardmäßig ermöglicht diese Option dem CSP-Zugriff auf den interaktiven Benutzer Desktop und das Anfordern von Informationen, z. b. eine Smartcard-PIN vom Benutzer. Wenn dieser Schlüssel auf true festgelegt ist, darf der CSP nicht mit dem Desktop interagieren und wird daran gehindert, eine Benutzeroberfläche für den Benutzer anzuzeigen. | `true | false` | `Silent = true` |
| SMIME | Wenn dieser Parameter auf true festgelegt ist, wird der Anforderung eine Erweiterung mit dem Objektbezeichnerwert 1.2.840.113549.1.9.15 hinzugefügt. Die Anzahl der Objekt Bezeichner hängt von der installierten Betriebssystemversion und der CSP-Funktion ab, die auf symmetrische Verschlüsselungsalgorithmen verweisen, die möglicherweise von Secure Multipurpose Internet Mail Extensions (S/MIME)-Anwendungen wie Outlook verwendet werden. | `true | false` | `SMIME = true` |
| Useexistingkeyset | Dieser Parameter wird verwendet, um anzugeben, dass ein vorhandenes Schlüsselpaar beim Aufbau einer Zertifikat Anforderung verwendet werden soll. Wenn dieser Schlüssel auf true festgelegt ist, müssen Sie auch einen Wert für den renewalcert-Schlüssel oder den keycontainer-Namen angeben. Der exportierbare Schlüssel darf nicht festgelegt werden, da Sie die Eigenschaften eines vorhandenen Schlüssels nicht ändern können. In diesem Fall wird kein Schlüsselmaterial generiert, wenn die Zertifikat Anforderung erstellt wird. | `true | false` | `UseExistingKeySet = true` |
| Keyprotection | Gibt einen Wert an, der angibt, wie ein privater Schlüssel vor der Verwendung geschützt wird. | <ul><li>`XCN_NCRYPT_UI_NO_PROTCTION_FLAG -- 0`</li><li>`XCN_NCRYPT_UI_PROTECT_KEY_FLAG -- 1`</li><li>`XCN_NCRYPT_UI_FORCE_HIGH_PROTECTION_FLAG -- 2`</li></ul> | `KeyProtection = NCRYPT_UI_FORCE_HIGH_PROTECTION_FLAG` |
| Suppressdefaults | Gibt einen booleschen Wert an, der angibt, ob die Standard Erweiterungen und Attribute in der Anforderung enthalten sind. Die Standardwerte werden durch ihre Objekt-IDs (OIDs) dargestellt. | `true | false` | `SuppressDefaults = true` |
| FriendlyName | Ein Anzeige Name für das neue Zertifikat. | Text | `FriendlyName = Server1` |
| ValidityPeriodUnits | Gibt eine Anzahl von Einheiten an, die mit ValidityPeriod verwendet werden sollen. Hinweis: Dies wird nur bei der Verwendung von verwendet `request type=cert` . | Numeric | `ValidityPeriodUnits = 3` |
| ValidityPeriod | ValidityPeriod muss ein US-Englisch-Plural-Zeitraum sein. Hinweis: Dies wird nur verwendet, wenn der Request Type = CERT lautet. | `Years |  Months | Weeks | Days | Hours | Minutes | Seconds` | `ValidityPeriod = Years` |

<sup>1</sup> -Parameter auf der linken Seite des Gleichheitszeichens (=)

<sup>2</sup> -Parameter auf der rechten Seite des Gleichheitszeichens (=)

#### <a name="extensions"></a>Extensions

Dieser Abschnitt ist optional.

| Erweiterungs-OID | Definition | Beispiel |
| ------------- | ---------- | ----- | ------- |
| 2.5.29.17 | | 2.5.29.17 = {Text} |
| *continue* | | `continue = UPN=User@Domain.com&` |
| *continue* | | `continue = EMail=User@Domain.com&` |
| *continue* | | `continue = DNS=host.domain.com&` |
| *continue* | | `continue = DirectoryName=CN=Name,DC=Domain,DC=com&` |
| *continue* | | `continue = URL=<http://host.domain.com/default.html&>` |
| *continue* | | `continue = IPAddress=10.0.0.1&` |
| *continue* | | `continue = RegisteredId=1.2.3.4.5&` |
| *continue* | | `continue = 1.2.3.4.6.1={utf8}String&` |
| *continue* | | `continue = 1.2.3.4.6.2={octet}AAECAwQFBgc=&` |
| *continue* | | `continue = 1.2.3.4.6.2={octet}{hex}00 01 02 03 04 05 06 07&` |
| *continue* | | `continue = 1.2.3.4.6.3={asn}BAgAAQIDBAUGBw==&` |
| *continue* | | `continue = 1.2.3.4.6.3={hex}04 08 00 01 02 03 04 05 06 07` |
| 2.5.29.37 | | `2.5.29.37={text}` |
| *continue* | | `continue = 1.3.6.1.5.5.7` |
| *continue* | | `continue = 1.3.6.1.5.5.7.3.1` |
| 2.5.29.19 | | `{text}ca=0pathlength=3` |
| Kritisch | | `Critical=2.5.29.19` |
| KeySpec | | <ul><li>`AT_NONE -- 0`</li><li>`AT_SIGNATURE -- 2`</li><li>`AT_KEYEXCHANGE -- 1`</ul></li> |
| RequestType | | <ul><li>`PKCS10 -- 1`</li><li>`PKCS7 -- 2`</li><li>`CMC -- 3`</li><li>`Cert -- 4`</li><li>`SCEP -- fd00 (64768)`</li></ul> |
| Endeinheits Zertifikaten der | | <ul><li>`CERT_DIGITAL_SIGNATURE_KEY_USAGE -- 80 (128)`</li><li>`CERT_NON_REPUDIATION_KEY_USAGE -- 40 (64)`</li><li>`CERT_KEY_ENCIPHERMENT_KEY_USAGE -- 20 (32)`</li><li>`CERT_DATA_ENCIPHERMENT_KEY_USAGE -- 10 (16)`</li><li>`CERT_KEY_AGREEMENT_KEY_USAGE -- 8`</li><li>`CERT_KEY_CERT_SIGN_KEY_USAGE -- 4`</li><li>`CERT_OFFLINE_CRL_SIGN_KEY_USAGE -- 2`</li><li>`CERT_CRL_SIGN_KEY_USAGE -- 2`</li><li>`CERT_ENCIPHER_ONLY_KEY_USAGE -- 1`</li><li>`CERT_DECIPHER_ONLY_KEY_USAGE -- 8000 (32768)`</li></ul> |
| Keyusageproperty | | <ul><li>`NCRYPT_ALLOW_DECRYPT_FLAG -- 1`</li><li>`NCRYPT_ALLOW_SIGNING_FLAG -- 2`</li><li>`NCRYPT_ALLOW_KEY_AGREEMENT_FLAG -- 4`</li><li>`NCRYPT_ALLOW_ALL_USAGES -- ffffff (16777215)`</li></ul> |
| Keyprotection | | <ul><li>`NCRYPT_UI_NO_PROTECTION_FLAG -- 0`</li><li>`NCRYPT_UI_PROTECT_KEY_FLAG -- 1`</li><li>`NCRYPT_UI_FORCE_HIGH_PROTECTION_FLAG -- 2`</li></ul> |
| "Subjetnameflags" | Vorlage | <ul><li>`CT_FLAG_SUBJECT_REQUIRE_COMMON_NAME -- 40000000 (1073741824)`</li><li>`CT_FLAG_SUBJECT_REQUIRE_DIRECTORY_PATH -- 80000000 (2147483648)`</li><li>`CT_FLAG_SUBJECT_REQUIRE_DNS_AS_CN -- 10000000 (268435456)`</li><li>`CT_FLAG_SUBJECT_REQUIRE_EMAIL -- 20000000 (536870912)`</li><li>`CT_FLAG_OLD_CERT_SUPPLIES_SUBJECT_AND_ALT_NAME -- 8`</li><li>`CT_FLAG_SUBJECT_ALT_REQUIRE_DIRECTORY_GUID -- 1000000 (16777216)`</li><li>`CT_FLAG_SUBJECT_ALT_REQUIRE_DNS -- 8000000 (134217728)`</li><li>`CT_FLAG_SUBJECT_ALT_REQUIRE_DOMAIN_DNS -- 400000 (4194304)`</li><li>`CT_FLAG_SUBJECT_ALT_REQUIRE_EMAIL -- 4000000 (67108864)`</li><li>`CT_FLAG_SUBJECT_ALT_REQUIRE_SPN -- 800000 (8388608)`</li><li>`CT_FLAG_SUBJECT_ALT_REQUIRE_UPN -- 2000000 (33554432)`</li></ul> |
| X500NameFlags | | <ul><li>`CERT_NAME_STR_NONE -- 0`</li><li>`CERT_OID_NAME_STR -- 2`</li><li>`CERT_X500_NAME_STR -- 3`</li><li>`CERT_NAME_STR_SEMICOLON_FLAG -- 40000000 (1073741824)`</li><li>`CERT_NAME_STR_NO_PLUS_FLAG -- 20000000 (536870912)`</li><li>`CERT_NAME_STR_NO_QUOTING_FLAG -- 10000000 (268435456)`</li><li>`CERT_NAME_STR_CRLF_FLAG -- 8000000 (134217728)`</li><li>`CERT_NAME_STR_COMMA_FLAG -- 4000000 (67108864)`</li><li>`CERT_NAME_STR_REVERSE_FLAG -- 2000000 (33554432)`</li><li>`CERT_NAME_STR_FORWARD_FLAG -- 1000000 (16777216)`</li><li>`CERT_NAME_STR_DISABLE_IE4_UTF8_FLAG -- 10000 (65536)`</li><li>`CERT_NAME_STR_ENABLE_T61_UNICODE_FLAG -- 20000 (131072)`</li><li>`CERT_NAME_STR_ENABLE_UTF8_UNICODE_FLAG -- 40000 (262144)`</li><li>`CERT_NAME_STR_FORCE_UTF8_DIR_STR_FLAG -- 80000 (524288)`</li><li>`CERT_NAME_STR_DISABLE_UTF8_DIR_STR_FLAG -- 100000 (1048576)`</li><li>`CERT_NAME_STR_ENABLE_PUNYCODE_FLAG -- 200000 (2097152)`</li></ul> |

> [!NOTE]
> `SubjectNameFlags` ermöglicht der INF- **Datei, anzugeben, welche Antrags** Teller-und **Subjektname** -Erweiterungs Felder von Certreq automatisch aufgefüllt werden sollen, basierend auf den Eigenschaften des aktuellen Benutzers oder der aktuellen Computer: DNS-Name, UPN usw. Die Verwendung der literalvorlage bedeutet, dass stattdessen die Vorlagen Namen-Flags verwendet werden. Dadurch kann eine einzelne INF-Datei in mehreren Kontexten verwendet werden, um Anforderungen mit kontextspezifischen Betreffinformationen zu generieren.
>
> `X500NameFlags` Gibt die Flags an, die direkt an die API übermittelt werden sollen, `CertStrToName` Wenn der `Subject INF keys` Wert in einen ASN. 1-codierten Distinguished **Name**konvertiert wird.

#### <a name="example"></a>Beispiel

So erstellen Sie eine Richtlinien Datei (. inf) in Notepad und speichern Sie als *RequestConfig. inf*:

```
[NewRequest]
Subject = CN=<FQDN of computer you are creating the certificate>
Exportable = TRUE
KeyLength = 2048
KeySpec = 1
KeyUsage = 0xf0
MachineKeySet = TRUE
[RequestAttributes]
CertificateTemplate=WebServer
[Extensions]
OID = 1.3.6.1.5.5.7.3.1
OID = 1.3.6.1.5.5.7.3.2
```

Auf dem Computer, für den Sie ein Zertifikat anfordern:

```
certreq –new requestconfig.inf certrequest.req
```

, Wenn die Syntax des [Zeichen folgen]-Abschnitts für OIDs und andere schwer zu verwendende Daten verwendet werden soll. Das neue {Text}-Syntax Beispiel für die EKU-Erweiterung, das eine durch Trennzeichen getrennte Liste von OIDs verwendet:

```
[Version]
Signature=$Windows NT$

[Strings]
szOID_ENHANCED_KEY_USAGE = 2.5.29.37
szOID_PKIX_KP_SERVER_AUTH = 1.3.6.1.5.5.7.3.1
szOID_PKIX_KP_CLIENT_AUTH = 1.3.6.1.5.5.7.3.2

[NewRequest]
Subject = CN=TestSelfSignedCert
Requesttype = Cert

[Extensions]
%szOID_ENHANCED_KEY_USAGE%={text}%szOID_PKIX_KP_SERVER_AUTH%,
_continue_ = %szOID_PKIX_KP_CLIENT_AUTH%
```

### <a name="certreq--accept"></a>Certreq-Accept

Der `–accept` -Parameter verknüpft den zuvor generierten privaten Schlüssel mit dem ausgestellten Zertifikat und entfernt die ausstehende Zertifikat Anforderung aus dem System, auf dem das Zertifikat angefordert wird (wenn eine übereinstimmende Anforderung vorliegt).

So akzeptieren Sie ein Zertifikat manuell

```
certreq -accept certnew.cer
```

> [!WARNING]
> Die Verwendung des `-accept` -Parameters mit den `-user` `–machine` Optionen und gibt an, ob das Installations Zertifikat im **Benutzer** -oder **Computer** Kontext installiert werden soll. Wenn eine ausstehende Anforderung in einem der beiden Kontext vorhanden ist, die mit dem installierten öffentlichen Schlüssel übereinstimmt, sind diese Optionen nicht erforderlich. Wenn keine ausstehende Anforderung vorhanden ist, muss eine dieser Angaben angegeben werden.

### <a name="certreq--policy"></a>Certreq: Richtlinie

Die Policy. inf-Datei ist eine Konfigurationsdatei, die die Einschränkungen definiert, die für eine Zertifizierungsstellen Zertifizierung gelten, wenn eine qualifizierte Unterordnung definiert ist.

So erstellen Sie eine Zertifikat übergreifende Anforderung:

```
certreq -policy certsrv.req policy.inf newcertsrv.req
```

Wenn `certreq -policy` Sie ohne zusätzlichen Parameter verwenden, wird ein Dialogfeld geöffnet, in dem Sie die angeforderte "fie" (. req,. CMC,. txt,. der,. cer oder. CRT) auswählen können. Nachdem Sie die angeforderte Datei ausgewählt und auf **Öffnen**klicken, wird ein weiteres Dialogfeld geöffnet, in dem Sie die INF-Richtlinien Datei auswählen können.

#### <a name="examples"></a>Beispiele

Hier finden Sie ein Beispiel für die "Policy. inf"-Datei in der [CAPolicy. inf-Syntax](../../networking/core-network-guide/cncg/server-certs/prepare-the-capolicy-inf-file.md).

### <a name="certreq--sign"></a>Certreq-Sign

So erstellen Sie eine neue Zertifikat Anforderung, Signieren Sie und übermitteln diese:

```
certreq -new policyfile.inf myrequest.req
certreq -sign myrequest.req myrequest.req
certreq -submit myrequest_sign.req myrequest_cert.cer
```

#### <a name="remarks"></a>Bemerkungen

- Wenn Sie `certreq -sign` ohne zusätzlichen Parameter verwenden, wird ein Dialogfenster geöffnet, in dem Sie die angeforderte Datei (req, CMC, txt, der, CER oder CRT) auswählen können.

- Das Signieren der qualifizierten Unterordnung erfordert möglicherweise **Unternehmens Administrator** -Anmelde Informationen. Dies ist eine bewährte Vorgehensweise zum Ausstellen von Signatur Zertifikaten für die qualifizierte Unterordnung.

- Das Zertifikat zum Signieren der qualifizierten Unterordnungs Anforderung verwendet die Vorlage für die qualifizierte Unterordnung. Unternehmens Administratoren müssen die Anforderung signieren oder den Personen, die das Zertifikat signieren, Benutzerberechtigungen erteilen.

- Möglicherweise müssen Sie über zusätzliche Mitarbeiter verfügen, die die CMC-Anforderung nach Ihnen signieren müssen. Dies hängt von der Sicherheitsstufe ab, die mit der qualifizierten Unterordnung verknüpft ist.

- Wenn die übergeordnete ZS der qualifizierten untergeordneten Zertifizierungsstelle, die Sie installieren, offline ist, müssen Sie das Zertifizierungsstellen Zertifikat für die qualifizierte untergeordnete Zertifizierungsstelle von der übergeordneten Offline-Zertifizierungsstelle abrufen Wenn die übergeordnete ZS Online ist, geben Sie das Zertifizierungsstellen Zertifikat für die qualifizierte untergeordnete Zertifizierungsstelle während des Installations-Assistenten für die **Zertifikat Dienste** an.

### <a name="certreq--enroll"></a>Certreq-registrieren

Sie können diesen Kommentar verwenden, um Ihre Zertifikate zu registrieren oder zu erneuern.

#### <a name="examples"></a>Beispiele

So registrieren Sie ein Zertifikat mithilfe der Vorlage " *Webserver* " und durch Auswählen des Richtlinien Servers mithilfe von "U/I":

```
certreq -enroll –machine –policyserver * WebServer
```

So erneuern Sie ein Zertifikat mit einer Seriennummer:

```
certreq –enroll -machine –cert 61 2d 3c fe 00 00 00 00 00 05 renew
```

Sie können nur gültige Zertifikate erneuern. Abgelaufene Zertifikate können nicht erneuert werden und müssen durch ein neues Zertifikat ersetzt werden.

## <a name="options"></a>Optionen

| Optionen | Beschreibung |
| ------- | ----------- |
| -beliebig | `Force ICertRequest::Submit` um den Codierungstyp zu bestimmen.|
| -atungb `<attributestring>` | Gibt die **Name** - **Wert** -Zeichen folgen Paare an, getrennt durch einen Doppelpunkt.<p>Getrennte **Name** - **Wert** -Zeichen folgen Paare mit `\n` (z. b. Name1: value1\nName2: Value2). |
| -Binary | Formatiert Ausgabedateien als Binärdaten anstelle von Base64-codiert. |
| -policyserver `<policyserver>` | standardi `<path>`<br>Fügen Sie den URI oder die eindeutige ID für einen Computer ein, auf dem der Zertifikat Registrierungsrichtlinien-Webdienst ausgeführt wird.<p>Um anzugeben, dass Sie eine Anforderungs Datei beim Durchsuchen verwenden möchten, verwenden Sie einfach ein Minuszeichen (-) für `<policyserver>` . |
| -config `<ConfigString>` | Verarbeitet den Vorgang mit der in der Konfigurations Zeichenfolge angegebenen Zertifizierungsstelle ( **cahostname\caname**). Geben Sie für https: \\ \ Connection den Registrierungs Server-URI an. Verwenden Sie für die lokale Computerspeicher Zertifizierungsstelle ein Minuszeichen (-). |
| -Anonym | Verwenden Sie anonyme Anmelde Informationen für Zertifikatregistrierungs-Webdienste. |
| -Kerberos | Verwenden Sie die Kerberos-Anmelde Informationen (Domäne) für Zertifikatregistrierungs-Webdienste. |
| -ClientCertificate `<ClientCertId>` | Sie können den `<ClientCertId>` durch einen Zertifikat Fingerabdruck, CN, EKU, Template, Email, UPN oder die neue Syntax ersetzen `name=value` . |
| -username `<username>` | Wird mit Zertifikatregistrierungs-Webdiensten verwendet. Sie können `<username>` durch den SAM-Namen oder den Wert von " **Domäne \ Benutzer** " ersetzen. Diese Option ist für die Verwendung mit der `-p` Option vorgesehen. |
| -p `<password>` | Wird mit Zertifikatregistrierungs-Webdiensten verwendet. Ersetzen Sie `<password>` durch das tatsächliche Kennwort des Benutzers. Diese Option ist für die Verwendung mit der `-username` Option vorgesehen. |
| -Benutzer | Konfiguriert den `-user` Kontext für eine neue Zertifikat Anforderung oder gibt den Kontext für eine Zertifikat Annahme an. Dies ist der Standardkontext, wenn kein Wert in der INF-oder-Vorlage angegeben ist. |
| -Computer | Konfiguriert eine neue Zertifikat Anforderung oder gibt den Kontext für eine Zertifikat Annahme für den Computer Kontext an. Bei neuen Anforderungen muss Sie mit dem machinekeyset-INF-Schlüssel und dem Vorlagen Kontext konsistent sein. Wenn diese Option nicht festgelegt ist und die Vorlage keinen Kontext festgelegt, ist der Standardwert der Benutzer Kontext. |
| -CRL | Schließt Zertifikat Sperr Listen (CRLs) in der Ausgabe an die Base64-codierten PKCS-#7 Datei, die durch angegeben wird `certchainfileout` , oder in die Base64-codierte Datei ein, die durch angegeben wird `requestfileout` . |
| -RPC | Weist Active Directory Zertifikat Dienste (AD CS) an, anstelle von verteiltem com eine RPC-Server Verbindung (Remote Procedure Aufruf) zu verwenden. |
| -adminforcemachine | Verwenden Sie den Schlüsseldienst oder den Identitätswechsel, um die Anforderung aus dem lokalen System Kontext zu übermitteln. Erfordert, dass der Benutzer, der diese Option aufruft, ein Mitglied der lokalen Administratoren ist. |
| -renewonbehalfof | Übermitteln Sie eine Verlängerung für den Antragsteller, der im Signaturzertifikat identifiziert wird. Dies legt CR_IN_ROBO fest, wenn die [ICertRequest:: Submit-Methode](/windows/win32/api/certcli/nf-certcli-icertrequest-submit) aufgerufen wird. |
| -f | Erzwingen, dass vorhandene Dateien überschrieben werden. Dadurch werden auch cachingvorlagen und Richtlinien umgangen. |
| -q | Unbeaufsichtigten Modus verwenden; alle interaktiven Eingabe Aufforderungen unterdrücken. |
| -Unicode | Schreibt die Unicode-Ausgabe, wenn die Standardausgabe umgeleitet oder an einen anderen Befehl weitergeleitet wird, was beim Aufrufen von Windows PowerShell-Skripts hilft. |
| -UnicodeText | Sendet eine Unicode-Ausgabe beim Schreiben von Base64-codierten Daten-blobdaten in Dateien. |

## <a name="formats"></a>Formate

| Formate | Beschreibung |
| ------- | ----------- |
| RequestFileIn | Base64-codierter oder binärer Eingabe Dateiname: PKCS #10 Zertifikat Anforderung, CMS-Zertifikat Anforderung, PKCS #7 Zertifikat Erneuerungs Anforderung, X. 509-Zertifikat für eine Kreuz Zertifizierung oder eine Zertifikat Anforderung im KeyGen-Tagformat. |
| RequestFileOut | Name der Base64-codierten Ausgabedatei. |
| CertFileOut | Base64-codierter X-509-Dateiname. |
| PKCS10fileout | Nur für die Verwendung mit dem- `certreq -policy` Parameter. Base64-codierter PKCS10-Ausgabe Dateiname. |
| certchainfinileout | Base64-codierter PKCS-#7 Dateiname. |
| fullresponse FileOut | Base64-codierter vollständiger Antwort Dateiname. |
| PolicyFileIn | Nur für die Verwendung mit dem- `certreq -policy` Parameter. INF-Datei, die eine Textdarstellung der Erweiterungen enthält, die zum qualifizieren einer Anforderung verwendet werden. |

## <a name="additional-resources"></a>Weitere Ressourcen

Die folgenden Artikel enthalten Beispiele für die Verwendung von Certreq:

- [Vorgehensweise beim Hinzufügen eines alternativen Antragsteller namens zu einem sicheren LDAP-Zertifikat](https://support.microsoft.com/help/931351/how-to-add-a-subject-alternative-name-to-a-secure-ldap-certificate)

- [Test Lab Guide: Deploying an AD CS Two-Tier PKI Hierarchy](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831348(v=ws.11))

- [Anhang 3: Certreq.exe Syntax](/previous-versions/windows/it-pro/windows-server-2003/cc736326(v=ws.10))

- [Manuelles Erstellen eines Webserver-SSL-Zertifikats](https://techcommunity.microsoft.com/t5/core-infrastructure-and-security/how-to-create-a-web-server-ssl-certificate-manually/ba-p/1128529)

- [Zertifikat Registrierung für System Center Operations Manager-Agent](/system-center/scom/plan-planning-agent-deployment?view=sc-om-2019)

- [Active Directory-Zertifikatdienste: Übersicht](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831740(v=ws.11))

- [Aktivieren von LDAP über SSL mit einer Zertifizierungsstelle von Drittanbietern](https://support.microsoft.com/help/321051/how-to-enable-ldap-over-ssl-with-a-third-party-certification-authority)