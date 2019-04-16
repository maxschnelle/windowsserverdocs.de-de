---
title: "Steuerelemente des Aufnahmegeräts Authentifizierung in AD FS"
description: "Dieses Dokument enthält Informationen zum Aktivieren von Geräteauthentifizierung in AD FS für Windows Server 2016 und 2012 R2"
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 11/09/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: d66cfde20060229844c34abeea85dd83b802ddad
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="device-authentication-controls-in-ad-fs"></a>Steuerelemente des Aufnahmegeräts Authentifizierung in AD FS
Das folgende Dokument veranschaulicht, wie Steuerelemente des Aufnahmegeräts Authentifizierung in Windows Server2016 und 2012 R2 zu aktivieren.

## <a name="device-authentication-controls-in-ad-fs-2012-r2"></a>Steuerelemente des Aufnahmegeräts Authentifizierung in AD FS 2012 R2
Ursprünglich in AD FS 2012 R2 ist eine globale Eigenschaft mit der Bezeichnung `DeviceAuthenticationEnabled`, kontrollierten Geräteauthentifizierung.

So konfigurieren Sie die Einstellung der `Set-AdfsGlobalAuthenticationPolicy`Cmdlet verwendet wurde, wie unten dargestellt:


``` powershell
PS:\>Set-AdfsGlobalAuthenticationPolicy –DeviceAuthenticationEnabled $true
```



Zum Deaktivieren der Geräteauthentifizierung wurde das gleiche Cmdlet verwendet, um den Wert auf $false festgelegt.

## <a name="device-authentication-controls-in-ad-fs-2016"></a>Steuerelemente des Aufnahmegeräts Authentifizierung in AD FS 2016
Die einzige Art von Geräteauthentifizierung in 2012 R2 unterstützt wurde ClientTLS.  In AD FS 2016 zusätzlich zu ClientTLS stehen zwei neue Typen von Geräteauthentifizierung für die Authentifizierung des moderner Geräte.  Dies sind:
- PKeyAuth
- PRT

Das neue Verhalten steuern die `DeviceAuthenticationEnabled` -Eigenschaft wird in Kombination mit eine neue Eigenschaft namens verwendet `DeviceAuthenticationMethod`.  

Die Authentifizierungsmethode Gerät bestimmt den Typ der Geräteauthentifizierung, die durchgeführt wird: Druck, PKeyAuth, ClientTLS, oder einer Kombination aus beidem.
Es verfügt über die folgenden Werte:
 - SignedToken: Nur PRT
 - PKeyAuth: PRT + PKeyAuth
 - ClientTLS: PRT + clientTLS 
 - Alle: Alle oben genannten

Wie Sie sehen, PRT gehört Authentifizierungsmethoden für alle Geräte, somit aktiviert die Standardmethode, die immer ist aktiviert, wenn `DeviceAuthenticationEnabled`festgelegt ist `$true`.

Beispiel: Verwenden Sie DeviceAuthenticationEnabled Cmdlet als oben, und neue Eigenschaft, um die Methoden konfigurieren:

``` powershell
PS:\>Set-AdfsGlobalAuthenticationPolicy –DeviceAuthenticationEnabled $true
```
>[!NOTE]
> Durch das Aktivieren der Geräteauthentifizierung (Einstellung `DeviceAuthenticationEnabled`auf `$true`) bedeutet, dass die `DeviceAuthenticationMethod`implizit festgelegt ist `SignedToken`, entspricht die **PRT **.


``` powershell
PS:\>Set-AdfsGlobalAuthenticationPolicy –DeviceAuthenticationMethod All
```
>[!NOTE]
>Die Standardauthentifizierungsmethode für Geräte ist `SignedToken`.  Andere Werte sind **PKeyAuth, *** ClientTLS,** und **alle **.

Die Bedeutung der der `DeviceAuthenticationMethod`leicht Werte geändert haben, seit der Freigabe von AD FS 2016.  Weitere Informationen finden Sie in der folgenden Tabelle für die Bedeutung der einzelnen Werte, je nachdem, welche Update:


|AD FS-Version|DeviceAuthenticationMethod Wert|Bedeutet, dass|
| ----- | ----- | ----- |
|2016 RTM|SignedToken|PRT + PkeyAuth|
||clientTLS|clientTLS|
||Alle|PRT PkeyAuth + clientTLS|
|2016 RTM und Windows Update auf dem neuesten Stand|SignedToken (Bedeutung)|PRT (nur)|
||PkeyAuth (neu)|PRT + PkeyAuth|
||clientTLS|PRT + clientTLS|
||Alle|PRT PkeyAuth + clientTLS|

## <a name="see-also"></a>Siehe auch
[AD FS-Vorgänge](../../ad-fs/AD-FS-2016-Operations.md)
