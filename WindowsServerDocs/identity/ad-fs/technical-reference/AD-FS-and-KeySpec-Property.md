---
title: Active Directory-Verbunddienste und Zertifikat, Schlüssel-Spezifikation Eigenschaft Informationen
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: a5307da5-02ff-4c31-80f0-47cb17a87272
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: db58fcce054f34c4b0a3f6725456badae9fd0468
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59879311"
---
# <a name="ad-fs-and-certificate-keyspec-property-information"></a>AD FS und Zertifikat KeySpec-Eigenschaft Informationen
Schlüssel-Spezifikation ("KeySpec") ist, eine Eigenschaft, die ein Zertifikat und Schlüssel zugeordnet wird. Es gibt an, ob es sich bei ein privater Schlüssel, der einem Zertifikat zugeordnet, die für die Signierung, Verschlüsselung oder beides verwendet werden kann.   

AD FS und Webanwendungsproxy-Fehler kann z. B. ein falscher Wert für die KeySpec verursacht werden:


- Fehler beim Herstellen eine SSL/TLS-Verbindung mit AD FS oder den Webanwendungsproxy ohne AD FS-Ereignisse protokolliert (obwohl SChannel 36888 und 36874 Ereignisse möglicherweise protokolliert werden)
- Fehler bei der Anmeldung auf dem AD FS oder WAP forms-Seite für Authentifizierung, jedoch keine Fehlermeldung angezeigt, die auf der Seite angezeigt.

Sie können Folgendes in das Ereignisprotokoll angezeigt werden:

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

## <a name="what-causes-the-problem"></a>Was bewirkt, dass das problem
Die KeySpec-Eigenschaft gibt an, wie ein Schlüssel generiert, oder aus dieser abgerufen durch Microsoft CryptoAPI (CAPI), aus einer Microsoft ältere kryptografischen Storage Provider (CSP), verwendet werden kann.

Wert KeySpec **1**, oder **AT_KEYEXCHANGE**, kann für Signierung und Verschlüsselung verwendet werden.  Der Wert **2**, oder **AT_SIGNATURE**, wird nur für die Signierung verwendet.

Die häufigste Fehlkonfiguration KeySpec verwendet den Wert 2 für ein anderes Zertifikat als das Tokensignaturzertifikat.  

Für Zertifikate, deren Schlüssel mit Anbietern von Cryptography Next Generation (CNG) generiert wurden, ist es kein Konzept für die Schlüssel-Spezifikation, und die KeySpec-Wert wird immer 0 (null) sein.

Erfahren Sie, wie für einen gültigen KeySpec-Wert, der unten überprüfen. 

### <a name="example"></a>Beispiel
Ein Beispiel für eine ältere CSP ist das Microsoft Enhanced Cryptographic Provider. 

Microsoft RSA CSP Schlüssel-BLOB-Format umfasst einen Algorithmusbezeichner entweder **CALG_RSA_KEYX** oder **CALG_RSA_SIGN**, Anforderungen für eine ** "AT_KEYEXCHANGE" ** oder **AT_ Signatur** Schlüssel.
  
Die RSA-Algorithmus für Schlüssel-IDs wie folgt auf KeySpec Werte zugeordnet

| Unterstützten Anbieter-Algorithmus| Spezifikation der Schlüssel-Wert für den CAPI-Aufrufe |
| --- | --- |
|CALG_RSA_KEYX : RSA-Schlüssel, der zum Signieren und Verschlüsseln verwendet werden kann| "AT_KEYEXCHANGE" (oder KeySpec = 1)|
CALG_RSA_SIGN: Schlüssel RSA-Signatur |AT_SIGNATURE (oder KeySpec = 2)|

## <a name="keyspec-values-and-associated-meanings"></a>KeySpec-Werte und zugehörigen Bedeutung
Im folgenden sind die Bedeutung der verschiedenen KeySpec-Werte:

|KeySpec-Wert|Bedeutet, dass|Empfohlene Verwendung von AD FS|
| --- | --- | --- |
|0|Das Zertifikat ist ein CNG-Zertifikat|Nur die SSL-Zertifikat|
|1|Der Schlüssel kann für eine ältere CAPI (nicht-CNG)-Zertifikat zum Signieren und Verschlüsseln verwendet werden|    SSL "," Token "Signierung", "token entschlüsseln, dienstkommunikationszertifikate|
|2|Für eine ältere CAPI (nicht-CNG)-Zertifikat kann der Schlüssel nur zum Signieren verwendet werden|nicht empfohlen.|

## <a name="how-to-check-the-keyspec-value-for-your-certificates--keys"></a>So prüfen Sie die KeySpec-Wert für die Zertifikate / Schlüssel
Um einen Wert für die Zertifikate anzuzeigen, Sie können, die **Certutil** -Befehlszeilentools.  

Im folgenden finden Sie ein Beispiel: **Certutil-v – speichern Sie meine**.  Dadurch wird die Zertifikatsinformationen auf dem Bildschirm sichern.

![KeySpec-Zertifikat](media/AD-FS-and-KeySpec-Property/keyspec1.png)

Unter CERT_KEY_PROV_INFO_PROP_ID suchen für zwei Dinge:


1. **ProviderType:** Dies gibt an, ob das Zertifikat, eine ältere kryptografischen Storage Provider (CSP verwendet) oder einen Schlüsselspeicheranbieter auf neuere Zertifikat Next Generation (CNG) APIs basierend.  Jeder Wert ungleich Null gibt an, einen legacy-Anbieter.
2.  **KeySpec:** Die folgenden sind Werte gültig KeySpec für eine AD FS-Zertifikat:

    Legacy-CSP-Anbieter (ProviderType ungleich 0):
    
    |AD FS-Zertifikat den Zertifizierungszweck|Gültige KeySpec-Werte|
    | --- | --- |
    |Dienstkommunikation|1|
    |Tokenentschlüsselungszertifikat|1|
    |Tokensignatur|1 und 2|
    |SSL|1|

    CNG provider (ProviderType = 0):
    |AD FS-Zertifikat den Zertifizierungszweck|Gültige KeySpec-Werte|
    | --- | --- |   
    |SSL|0|

## <a name="how-to-change-the-keyspec-for-your-certificate-to-a-supported-value"></a>Wie Sie Keyspec für Ihr Zertifikat in einen unterstützten Wert ändern
Ändern des Werts KeySpec erfordert keine das Zertifikat erneut generiert oder erneut von der Zertifizierungsstelle ausgegeben werden soll.  Die KeySpec kann geändert werden, durch einen erneuten Import der vollständiges Zertifikat und den privaten Schlüssel aus einer PFX-Datei in den Zertifikatspeicher, verwenden die folgenden Schritte aus:


1. Zuerst überprüfen Sie, und notieren Sie die Berechtigungen für den privaten Schlüssel auf das vorhandene Zertifikat, damit sie neu konfiguriert bei Bedarf nach der erneut importieren können.
2. Exportieren Sie das Zertifikat, einschließlich des privaten Schlüssels in eine PFX-Datei.
3. Führen Sie die folgenden Schritte aus, für jeden AD FS- und WAP-server
    1. Löschen Sie das Zertifikat (von der AD FS / WAP-Server)
    2. Öffnen Sie eine PowerShell-Eingabeaufforderung, und importieren Sie die PFX-Datei auf jedem AD FS- und WAP-Server mithilfe der folgenden Cmdlet-Syntax, die Angabe des Werts von "AT_KEYEXCHANGE" (die für alle Zwecke der AD FS-Zertifikat funktioniert):
        1. C:\>certutil –importpfx certfile.pfx AT_KEYEXCHANGE
        2. Geben Sie ein PFX-Kennwort
    3. Wenn die oben genannten abgeschlossen ist, führen Sie folgende Schritte
        1. Überprüfen Sie die Berechtigungen für den privaten Schlüssel
        2. Starten Sie den AD FS oder Wap-Dienst





