---
title: Steuerelemente für die Geräte Authentifizierung in AD FS
description: In diesem Dokument wird beschrieben, wie Sie die Geräte Authentifizierung in AD FS für Windows Server 2016 und 2012 R2 aktivieren.
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 11/09/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 87c011b18ad4a1d464072c1ea90b09a44e831378
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407366"
---
# <a name="device-authentication-controls-in-ad-fs"></a>Steuerelemente für die Geräte Authentifizierung in AD FS
Das folgende Dokument zeigt, wie Sie Geräte Authentifizierungs Steuerelemente in Windows Server 2016 und 2012 R2 aktivieren.

## <a name="device-authentication-controls-in-ad-fs-2012-r2"></a>Geräte Authentifizierungs Steuerelemente in AD FS 2012 R2
Ursprünglich in AD FS 2012 R2 gab es eine globale Authentifizierungs Eigenschaft mit dem Namen "`DeviceAuthenticationEnabled`", die die Geräte Authentifizierung gesteuert hat.

Zum Konfigurieren der Einstellung wurde das Cmdlet "`Set-AdfsGlobalAuthenticationPolicy`" wie unten gezeigt verwendet:


``` powershell
PS:\>Set-AdfsGlobalAuthenticationPolicy –DeviceAuthenticationEnabled $true
```



Zum Deaktivieren der Geräte Authentifizierung wurde das gleiche Cmdlet verwendet, um den Wert auf $false festzulegen.

## <a name="device-authentication-controls-in-ad-fs-2016"></a>Geräte Authentifizierungs Steuerelemente in AD FS 2016
Der einzige in 2012 R2 unterstützte Geräte Authentifizierungstyp war clienttls.  In AD FS 2016 sind neben clienttls zwei neue Arten der Geräte Authentifizierung für die Authentifizierung moderner Geräte vorhanden.  Diese lauten wie folgt:
- Pkeyauth
- PRT

Um das neue Verhalten zu steuern, wird die `DeviceAuthenticationEnabled`-Eigenschaft in Kombination mit der neuen Eigenschaft `DeviceAuthenticationMethod` verwendet.  

Die Geräte Authentifizierungsmethode bestimmt den Typ der Geräte Authentifizierung, die durchgeführt wird: PRT, pkeyauth, clienttls oder eine Kombination.
Die folgenden Werte sind möglich:
 - Signedtoken: Nur PRT
 - Pkeyauth: PRT + pkeyauth
 - ClientTLS PRT + clienttls
 - All: Alle obigen

Wie Sie sehen können, ist PRT Teil aller Geräte Authentifizierungsmethoden, sodass die Standardmethode, die immer aktiviert ist, wenn `DeviceAuthenticationEnabled` auf `$true` festgelegt ist, wirksam ist.

Beispiel: Verwenden Sie zum Konfigurieren der Methode (en) das deviceauthenticationaktivierte Cmdlet zusammen mit der neuen Eigenschaft:

``` powershell
PS:\>Set-AdfsGlobalAuthenticationPolicy –DeviceAuthenticationEnabled $true
```

>[!NOTE]
> In ADFS 2019 können `DeviceAuthenticationMethod` mit dem Befehl `Set-AdfsRelyingPartyTrust` verwendet werden.

``` powershell
PS:\>Set-AdfsRelyingPartyTrust -DeviceAuthenticationMethod ClientTLS
```

>[!NOTE]
> Das Aktivieren der Geräte Authentifizierung (durch Festlegen von `DeviceAuthenticationEnabled` auf `$true`) bedeutet, dass die `DeviceAuthenticationMethod` implizit auf `SignedToken` festgelegt ist, was dem **PRT**entspricht.


``` powershell
PS:\>Set-AdfsGlobalAuthenticationPolicy –DeviceAuthenticationMethod All
```
> [!NOTE]
> Die Standardmethode für die Geräte Authentifizierung ist `SignedToken`.  Andere Werte sind **pkeyauth,** <strong>clienttls</strong> und **all**.

Die Bedeutung der `DeviceAuthenticationMethod`-Werte hat sich seit der Veröffentlichung von AD FS 2016 geringfügig geändert.  In der folgenden Tabelle finden Sie die Bedeutung der einzelnen Werte, abhängig von der Update Ebene:


|AD FS Version|Deviceauthenticationmethod-Wert|Damit|
| ----- | ----- | ----- |
|2016 RTM|Signedtoken|PRT + pkeyauth|
||clientTLS|clientTLS|
||All|PRT + pkeyauth + clienttls|
|2016 RTM + aktuell mit Windows Update|Signedtoken (geänderte Bedeutung)|PRT (nur)|
||Pkeyauth (neu)|PRT + pkeyauth|
||clientTLS|PRT + clienttls|
||All|PRT + pkeyauth + clienttls|

## <a name="see-also"></a>Siehe auch
[AD FS-Vorgänge](../../ad-fs/AD-FS-2016-Operations.md)
