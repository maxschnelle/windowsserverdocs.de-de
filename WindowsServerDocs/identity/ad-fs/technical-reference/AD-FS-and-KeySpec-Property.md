---
title: "Active Directory-Verbunddienste und Zertifikat Schlüssel-Spezifikation Eigenschaft Informationen"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: a5307da5-02ff-4c31-80f0-47cb17a87272
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: db58fcce054f34c4b0a3f6725456badae9fd0468
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="ad-fs-and-certificate-keyspec-property-information"></a>AD FS und das Zertifikat von Schlüsselspezifikationen Eigenschaft Informationen
Schlüssel-Spezifikation ("von Schlüsselspezifikationen") ist eine Eigenschaft eines Zertifikats und Schlüssels zugeordnet. Es gibt an, ob ein mit einem Zertifikat verknüpften privater Schlüssel für die Signierung, Verschlüsselung oder beides verwendet werden kann.   

AD FS und Web Application Proxy-Fehler kann z.B. ein falscher Wert für die von Schlüsselspezifikationen verursacht werden:


- Fehler beim Herstellen eine SSL/TLS-Verbindung mit AD FS oder das Web Application Proxy mit keine AD FS-Ereignisse protokolliert (obwohl SChannel 36888 und 36874 Ereignisse protokolliert werden können)
- Fehler beim Anmelden am AD FS oder WAP forms-Seite für Authentifizierung, jedoch keine Fehlermeldung angezeigt, die auf der Seite angezeigt.

Sie können die folgenden im Ereignisprotokoll finden Sie unter:

    Log Name:      AD FS Tracing/Debug
    Source:        AD FS Tracing
    Date:          2/12/2015 9:03:08 AM
    Event ID:      67
    Task Category: None
    Level:         Error
    Keywords:      ADFSProtocol
    User:          S-1-5-21-3723329422-3858836549-556620232-1580884
    Computer:      ADFS1.contoso.com
    Description:
    Ignore corrupted SSO cookie.

## <a name="what-causes-the-problem"></a>Was das Problem verursacht wird.
Die von Schlüsselspezifikationen-Eigenschaft gibt an, wie die Schlüssel generiert oder abgerufen durch Microsoft CryptoAPI (CAPI), aus einer Microsoft ältere kryptografischen Storage Provider (CSP), verwendet werden kann.

Der Wert von Schlüsselspezifikationen **1**, oder **AT_KEYEXCHANGE**, für Signierung und Verschlüsselung verwendet werden kann.  Der Wert **2**, oder **AT_SIGNATURE**, wird nur für die Signierung verwendet.

Die am häufigsten verwendeten Fehlkonfiguration von Schlüsselspezifikationen wird der Wert 2 für ein Zertifikat als das Tokensignaturzertifikat verwendet.  

Für Zertifikate, deren Schlüssel generiert wurden Cryptography Next Generation (CNG)-Anbieter verwenden, ist es gibt kein Konzept von Schlüssel-Spezifikation, und des Werts von Schlüsselspezifikationen immer 0 (null).

Informationen Sie zum Prüfen, ob eines gültigen von Schlüsselspezifikationen Wert unter. 

### <a name="example"></a>Beispiel
Ein Beispiel für eine ältere CSP ist der Microsoft Enhanced Cryptographic Provider. 

Microsoft RSA CSP Schlüssel-BLOB-Format enthält einen Algorithmusbezeichner entweder **calg_rsa_keyx** oder **CALG_RSA_SIGN**bzw. für Serviceanfragen für entweder ** AT_KEYEXCHANGE ** oder **AT_SIGNATURE** Schlüssel.
  
Die IDs der RSA-Algorithmus wie folgt auf Werte von Schlüsselspezifikationen zugeordnet

| Anbieter unterstützten Algorithmus| Schlüssel-Spezifikation Wert für CAPI-Aufrufe |
| --- | --- |
|Calg_rsa_keyx.: RSA-Schlüssel, die zum Signieren und Verschlüsseln verwendet werden können| AT_KEYEXCHANGE (oder von Schlüsselspezifikationen = 1)|
CALG_RSA_SIGN: Nur die wichtigsten RSA-Signatur |AT_SIGNATURE (oder von Schlüsselspezifikationen = 2)|

## <a name="keyspec-values-and-associated-meanings"></a>Werte von Schlüsselspezifikationen und zugehörigen Bedeutung
Im folgenden sind die Bedeutung der verschiedenen von Schlüsselspezifikationen Werte:

|Von Schlüsselspezifikationen Wert|Bedeutet, dass|Empfohlene Verwendung von AD FS|
| --- | --- | --- |
|0|Das Zertifikat ist ein CNG-Zertifikat|Nur SSL-Zertifikat|
|1|Für eine ältere CAPI (Nicht-CNG)-Zertifikat kann der Schlüssel zum Signieren und Verschlüsseln verwendet werden|    SSL, Tokensignaturzertifikat, Token entschlüsseln, dienstkommunikationszertifikate|
|2|Für eine ältere CAPI (Nicht-CNG)-Zertifikat kann der Schlüssel nur für das Signieren verwendet werden|Nicht empfohlen.|

## <a name="how-to-check-the-keyspec-value-for-your-certificates--keys"></a>Überprüfen Sie den Wert von Schlüsselspezifikationen für Ihre Zertifikate / Schlüssel
Um einen Wert für die Zertifikate anzuzeigen, können Sie, die **Certutil** Befehlszeilentool.  

Im folgenden finden Sie ein Beispiel: **Certutil-v – store mein**.  Dadurch wird die Zertifikatinformationen auf dem Bildschirm ausgeben.

![Von Schlüsselspezifikationen cert](media/AD-FS-and-KeySpec-Property/keyspec1.png)

Unter CERT_KEY_PROV_INFO_PROP_ID suchen für zwei Dinge:


1. **ProviderType:** Dies gibt an, ob das Zertifikat eine ältere kryptografischen Storage Provider (CSP verwendet) oder einen Key Storage Provider auf neuere Zertifikat Next Generation (CNG) APIs basierend.  Alle Nicht-NULL-Wert gibt einen Legacy-Anbieter an.
2.  **Von Schlüsselspezifikationen:** die folgenden Werte sind gültig von Schlüsselspezifikationen für ein AD FS-Zertifikat:

    Ältere Kryptografiedienstanbieter (ProviderType ungleich 0):
    
    |AD FS-Zertifikatzweck|Gültige von Schlüsselspezifikationen Werte|
    | --- | --- |
    |Die Kommunikation zwischen der|1|
    |Entschlüsseln von Token|1|
    |Signieren von Token|1 und 2|
    |SSL|1|

    CNG-Anbieter (ProviderType = 0):
    |AD FS-Zertifikatzweck|Gültige von Schlüsselspezifikationen Werte|
    | --- | --- |   
    |SSL|0|

## <a name="how-to-change-the-keyspec-for-your-certificate-to-a-supported-value"></a>Zum Ändern der von Schlüsselspezifikationen für das Zertifikat auf einem unterstützten Wert
Ändern des Werts von Schlüsselspezifikationen erfordert keine das Zertifikat neu erstellt oder erneut von der Zertifizierungsstelle ausgestellt werden.  Die von Schlüsselspezifikationen kann geändert werden, durch einen erneuten Import die vollständige Zertifikat und den privaten Schlüssel in eine PFX-Datei in den Zertifikatspeicher, verwenden die folgenden Schritteaus:


1. Zuerst überprüfen Sie und notieren Sie die privaten Schlüssel Berechtigungen für das vorhandene Zertifikat, damit sie neu konfigurierten bei Bedarf nach der erneut importiert werden können.
2. Exportieren Sie das Zertifikat, einschließlich des privaten Schlüssels in eine PFX-Datei.
3. Führen Sie die folgenden Schrittefür jeden Server, AD FS und WAP
    1. Löschen Sie das Zertifikat (aus der AD FS / WAP-Server)
    2. Öffnen Sie ein Eingabeaufforderungsfenster mit erhöhten Rechten PowerShell, und importieren Sie die PFX-Datei auf jedem AD FS und WAP-Server das folgende Cmdlet-Syntax verwenden, der AT_KEYEXCHANGE Wert (die für alle Zwecke der AD FS-Zertifikat kann):
        1. C:\ > Certutil – Importpfx certfile.pfx AT_KEYEXCHANGE
        2. Geben Sie die PFX-Kennwort
    3. Wenn die oben genannten abgeschlossen ist, führen Sie folgende Schritte
        1. Überprüfen Sie die Berechtigungen für privaten Schlüssel
        2. Starten Sie den AD FS oder Wap-Dienst





