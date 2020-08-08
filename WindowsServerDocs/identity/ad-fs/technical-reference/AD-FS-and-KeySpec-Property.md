---
title: Eigenschaften Informationen für die Active Directory-Verbunddienste (AD FS)-und Zertifikat Schlüssel Spezifikation
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.assetid: a5307da5-02ff-4c31-80f0-47cb17a87272
ms.author: billmath
ms.openlocfilehash: a78f989230450bcf59f86add66bdcfe91fa23c77
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87938118"
---
# <a name="ad-fs-and-certificate-keyspec-property-information"></a>Eigenschaften Informationen für die AD FS-und Zertifikat KeySpec
Key Specification ("KeySpec") ist eine Eigenschaft, die einem Zertifikat und einem Schlüssel zugeordnet ist. Hiermit wird angegeben, ob ein mit einem Zertifikat verknüpften privaten Schlüssel zum Signieren, verschlüsseln oder beides verwendet werden kann.

Ein falscher KeySpec-Wert kann zu AD FS-und webanwendungsproxy-Fehlern führen. Beispiele:


- Fehler beim Herstellen einer SSL/TLS-Verbindung mit AD FS oder dem webanwendungsproxy, ohne dass AD FS Ereignisse protokolliert werden (obwohl SChannel 36888-und 36874-Ereignisse protokolliert werden können).
- Fehler bei der Anmeldung auf der Formular basierten Authentifizierungsseite für AD FS oder WAP, ohne dass auf der Seite eine Fehlermeldung angezeigt wird.

Im Ereignisprotokoll wird möglicherweise Folgendes angezeigt:

```
Log Name:   AD FS Tracing/Debug
Source: AD FS Tracing
Date:   2/12/2015 9:03:08 AM
Event ID:   67
Task Category: None
Level:  Error
Keywords:   ADFSProtocol
User:   S-1-5-21-3723329422-3858836549-556620232-1580884
Computer:   ADFS1.contoso.com
Description:
Ignore corrupted SSO cookie.
```

## <a name="what-causes-the-problem"></a>Ursache des Problems
Die KeySpec-Eigenschaft gibt an, wie ein Schlüssel, der von Microsoft CryptoAPI (CAPI) generiert oder abgerufen wurde, von einem Microsoft Legacy-Kryptografiespeicheranbieter (CSP) verwendet werden kann.

Der KeySpec-Wert **1**oder **AT_KEYEXCHANGE**kann zum Signieren und Verschlüsseln verwendet werden.  Der Wert **2**oder **AT_SIGNATURE**wird nur für die Signierung verwendet.

Bei der gängigsten KeySpec-Fehlkonfiguration wird der Wert 2 für ein anderes Zertifikat als das Tokensignaturzertifikat verwendet.

Für Zertifikate, deren Schlüssel mit CNG-Anbietern (Cryptography Next Generation) generiert wurden, gibt es kein Konzept der Schlüssel Spezifikation, und der KeySpec-Wert ist immer 0 (null).

Weitere Informationen finden Sie unter Überprüfen auf einen gültigen KeySpec-Wert weiter unten.

### <a name="example"></a>Beispiel
Ein Beispiel für einen Legacy-CSP ist der Microsoft Enhanced Cryptographic Provider.

Das Microsoft RSA CSP-Schlüssel-BLOB-Format enthält einen Algorithmusbezeichner (entweder **CALG_RSA_KEYX** oder **CALG_RSA_SIGN**), um Anforderungen für <strong>AT_KEYEXCHANGE * *-oder * *-AT_SIGNATURE</strong> Schlüssel zu bedienen.

Die RSA-schlüsselalgorithmusbezeichner werden KeySpec-Werten folgendermaßen zugeordnet:

| Anbieter unterstützter Algorithmus| Schlüssel Spezifikations Wert für CAPI-Aufrufe |
| --- | --- |
|CALG_RSA_KEYX: RSA-Schlüssel, der zum Signieren und entschlüsseln verwendet werden kann| AT_KEYEXCHANGE (oder KeySpec = 1)|
CALG_RSA_SIGN: Schlüssel nur für RSA-Signatur |AT_SIGNATURE (oder KeySpec = 2)|

## <a name="keyspec-values-and-associated-meanings"></a>KeySpec-Werte und zugehörige Bedeutungen
Im folgenden sind die Bedeutungen der verschiedenen KeySpec-Werte aufgeführt:

|KeySpec-Wert|Damit|Empfohlene AD FS Verwendung|
| --- | --- | --- |
|0|Das Zertifikat ist ein CNG-Zertifikat.|Nur SSL-Zertifikat|
|1|Für ein Legacy-CAPI-Zertifikat (nicht CNG) kann der Schlüssel zum Signieren und entschlüsseln verwendet werden.|    SSL, Tokensignatur, tokenentschlüsselungsdienst, Dienst Kommunikations Zertifikate|
|2|Für ein Legacy-CAPI-Zertifikat (nicht CNG) kann der Schlüssel nur für die Signierung verwendet werden.|nicht empfohlen|

## <a name="how-to-check-the-keyspec-value-for-your-certificates--keys"></a>Überprüfen des KeySpec-Werts für Ihre Zertifikate/Schlüssel
Um einen Zertifikat Wert anzuzeigen, können Sie das **certutil** -Befehlszeilen Tool verwenden.

Im folgenden finden Sie ein Beispiel: **certutil – v – Store My**.  Dadurch werden die Zertifikat Informationen auf dem Bildschirm angezeigt.

![KeySpec-Zertifikat](media/AD-FS-and-KeySpec-Property/keyspec1.png)

Wählen Sie unter CERT_KEY_PROV_INFO_PROP_ID zwei Dinge aus:


1. **ProviderType:** Hiermit wird angegeben, ob das Zertifikat einen Legacy-Kryptografiespeicheranbieter (CSP) oder einen Schlüsselspeicher Anbieter verwendet, der auf den neueren CNG-APIs (Certificate Next Generation) basiert.  Ein Wert ungleich 0 (null) gibt einen Legacy Anbieter an.
2. **KeySpec:** Im folgenden sind gültige KeySpec-Werte für ein AD FS Zertifikat aufgeführt:

   Legacy-CSP-Anbieter (ProviderType ist nicht gleich 0):

   |AD FS Zertifikat Zweck|Gültige KeySpec-Werte|
   | --- | --- |
   |Dienst Kommunikation|1|
   |Tokenentschlüsselung|1|
   |Tokensignaturen|1 und 2|
   |SSL|1|

   CNG-Anbieter (ProviderType = 0):

   |AD FS Zertifikat Zweck|Gültige KeySpec-Werte|
   | --- | --- |
   |SSL|0|

## <a name="how-to-change-the-keyspec-for-your-certificate-to-a-supported-value"></a>Ändern der KeySpec für Ihr Zertifikat in einen unterstützten Wert
Das Ändern des KeySpec-Werts erfordert nicht, dass das Zertifikat erneut generiert oder von der Zertifizierungsstelle erneut ausgestellt wird.  Die KeySpec kann geändert werden, indem Sie das gesamte Zertifikat und den privaten Schlüssel aus einer PFX-Datei erneut in den Zertifikat Speicher importieren, indem Sie die folgenden Schritte ausführen:


1. Überprüfen und notieren Sie zunächst die Berechtigungen für den privaten Schlüssel für das vorhandene Zertifikat, damit diese nach dem erneuten Importieren neu konfiguriert werden können.
2. Exportieren Sie das Zertifikat mit dem privaten Schlüssel in eine PFX-Datei.
3. Führen Sie die folgenden Schritte für jeden AD FS und jeden WAP-Server aus.
    1. Löschen des Zertifikats (vom AD FS/WAP-Server)
    2. Öffnen Sie eine PowerShell-Eingabeaufforderung mit erhöhten Rechten, und importieren Sie die PFX-Datei auf jedem AD FS-und WAP-Server, indem Sie die folgende Cmdlet-Syntax verwenden. Geben Sie dabei den AT_KEYEXCHANGE Wert an (der für alle AD FS Zertifikat Zwecke
        1. C: \> certutil – importpfx CertFile. pfx AT_KEYEXCHANGE
        2. PFX-Kennwort eingeben
    3. Gehen Sie nach Abschluss der obigen Schritte folgendermaßen vor:
        1. Überprüfen der Berechtigungen für den privaten Schlüssel
        2. Starten Sie den ADFS-oder WAP-Dienst neu.





