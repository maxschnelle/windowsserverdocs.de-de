---
title: Authentifizierung der Gerätesteuerelemente in AD FS
description: In diesem Dokument wird beschrieben, wie Sie zum Aktivieren der Geräteauthentifizierung in AD FS für WindowsServer 2016 und 2012 R2
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 11/09/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: d66cfde20060229844c34abeea85dd83b802ddad
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59822821"
---
# <a name="device-authentication-controls-in-ad-fs"></a>Authentifizierung der Gerätesteuerelemente in AD FS
Das folgende Dokument veranschaulicht das Aktivieren der Authentifizierung der Gerätesteuerelemente in Windows Server 2016 und 2012 R2.

## <a name="device-authentication-controls-in-ad-fs-2012-r2"></a>Authentifizierung der Gerätesteuerelemente in AD FS 2012 R2
Ursprünglich unter AD FS 2012 R2 gab es eine globale Authentifizierungsrichtlinie Eigenschaft namens `DeviceAuthenticationEnabled` , kontrollierten Geräteauthentifizierung.

So konfigurieren Sie die Einstellung der `Set-AdfsGlobalAuthenticationPolicy` Cmdlet wurde verwendet, wie unten dargestellt:


``` powershell
PS:\>Set-AdfsGlobalAuthenticationPolicy –DeviceAuthenticationEnabled $true
```



Zum Deaktivieren der Geräteauthentifizierung wurde das gleiche Cmdlet verwendet, um den Wert auf $false festgelegt.

## <a name="device-authentication-controls-in-ad-fs-2016"></a>Authentifizierung der Gerätesteuerelemente in AD FS 2016
Die einzige Art von Geräteauthentifizierung unterstützt in 2012 R2 wurde ClientTLS.  In AD FS 2016 neben ClientTLS sind zwei neue Typen von Geräteauthentifizierung für moderne Geräte-Authentifizierung.  Diese lauten wie folgt:
- PKeyAuth
- PRT

Um das neue Verhalten zu steuern die `DeviceAuthenticationEnabled` -Eigenschaft wird in Kombination verwendet, wobei eine neue Eigenschaft namens `DeviceAuthenticationMethod`.  

Die Authentifizierungsmethode Gerät bestimmt den Typ der Geräteauthentifizierung, die durchgeführt wird: PRT PKeyAuth, ClientTLS oder eine Kombination.
Es hat die folgenden Werte:
 - SignedToken: Nur PRT
 - PKeyAuth: PRT + PKeyAuth
 - ClientTLS: PRT + clientTLS 
 - All: Alle obigen

Wie Sie sehen können, PRT gehört alle Gerät-Authentifizierungsmethoden, somit wirksam die Standardmethode, die immer aktiviert, wenn `DeviceAuthenticationEnabled` nastaven NA hodnotu `$true`.

Beispiel: Verwenden Sie zum Konfigurieren der Methode(n) DeviceAuthenticationEnabled Cmdlet als oben zusammen mit der neuen Eigenschaft ein:

``` powershell
PS:\>Set-AdfsGlobalAuthenticationPolicy –DeviceAuthenticationEnabled $true
```
>[!NOTE]
> Aktivieren der Geräteauthentifizierung (Einstellung `DeviceAuthenticationEnabled` zu `$true`) bedeutet, dass die `DeviceAuthenticationMethod` wird implizit festgelegt, `SignedToken`, entspricht die **PRT**.


``` powershell
PS:\>Set-AdfsGlobalAuthenticationPolicy –DeviceAuthenticationMethod All
```
>[!NOTE]
>Die Standardauthentifizierungsmethode für Geräte ist `SignedToken`.  Andere Werte sind **PKeyAuth, *** ClientTLS,** und **alle**.

Die Bedeutung des das `DeviceAuthenticationMethod` etwas Werte geändert haben, da AD FS 2016 veröffentlicht wurde.  Finden Sie in der folgenden Tabelle die Bedeutung der einzelnen Werte, je nach der UpdateStatus:


|AD FS-version|DeviceAuthenticationMethod Wert|Bedeutet, dass|
| ----- | ----- | ----- |
|2016 RTM|SignedToken|PRT + PkeyAuth|
||clientTLS|clientTLS|
||Alle|PRT + PkeyAuth + clientTLS|
|2016 RTM + bis zu dem Datum mit Windows Update|SignedToken (also geänderte Daten)|PRT (ausschließlich)|
||PkeyAuth (neu)|PRT + PkeyAuth|
||clientTLS|PRT + clientTLS|
||Alle|PRT + PkeyAuth + clientTLS|

## <a name="see-also"></a>Siehe auch
[AD FS-Vorgänge](../../ad-fs/AD-FS-2016-Operations.md)
