---
title: Steuerelemente für die Geräte Authentifizierung in AD FS
description: In diesem Dokument wird beschrieben, wie Sie die Geräte Authentifizierung in AD FS für Windows Server 2016 und 2012 R2 aktivieren.
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 11/09/2017
ms.topic: article
ms.openlocfilehash: 976a8db89d8ffdb08f5f453619b7a341fb4dcdb4
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87949694"
---
# <a name="device-authentication-controls-in-ad-fs"></a>Steuerelemente für die Geräte Authentifizierung in AD FS
Das folgende Dokument zeigt, wie Sie Geräte Authentifizierungs Steuerelemente in Windows Server 2016 und 2012 R2 aktivieren.

## <a name="device-authentication-controls-in-ad-fs-2012-r2"></a>Geräte Authentifizierungs Steuerelemente in AD FS 2012 R2
Ursprünglich in AD FS 2012 R2 gab es eine globale Authentifizierungs Eigenschaft mit `DeviceAuthenticationEnabled` dem Namen, die die Geräte Authentifizierung gesteuert hat.

Zum Konfigurieren der Einstellung wurde das `Set-AdfsGlobalAuthenticationPolicy` Cmdlet wie unten gezeigt verwendet:


``` powershell
PS:\>Set-AdfsGlobalAuthenticationPolicy –DeviceAuthenticationEnabled $true
```



Zum Deaktivieren der Geräte Authentifizierung wurde das gleiche Cmdlet verwendet, um den Wert auf $false festzulegen.

## <a name="device-authentication-controls-in-ad-fs-2016"></a>Geräte Authentifizierungs Steuerelemente in AD FS 2016
Der einzige in 2012 R2 unterstützte Geräte Authentifizierungstyp war clienttls.  In AD FS 2016 sind neben clienttls zwei neue Arten der Geräte Authentifizierung für die Authentifizierung moderner Geräte vorhanden.  Diese lauten wie folgt:
- Pkeyauth
- PRT

Um das neue Verhalten zu steuern, `DeviceAuthenticationEnabled` wird die-Eigenschaft in Kombination mit einer neuen Eigenschaft namens verwendet `DeviceAuthenticationMethod` .

Die Geräte Authentifizierungsmethode bestimmt den Typ der Geräte Authentifizierung, die ausgeführt wird: PRT, pkeyauth, clienttls oder eine Kombination.
Die folgenden Werte sind möglich:
 - Signedtoken: nur PRT
 - Pkeyauth: PRT + pkeyauth
 - Clienttls: PRT + clienttls
 - Alle: alle oben genannten

Wie Sie sehen können, ist PRT Teil aller Geräte Authentifizierungsmethoden, sodass es die Standardmethode ist, die immer aktiviert ist, wenn `DeviceAuthenticationEnabled` auf festgelegt ist `$true` .

Beispiel: Verwenden Sie zum Konfigurieren der Methode (en) das deviceauthenticationaktivierte-Cmdlet zusammen mit der neuen Eigenschaft:

``` powershell
PS:\>Set-AdfsGlobalAuthenticationPolicy –DeviceAuthenticationEnabled $true
```

>[!NOTE]
> In ADFS 2019 `DeviceAuthenticationMethod` kann mit dem Befehl verwendet werden `Set-AdfsRelyingPartyTrust` .

``` powershell
PS:\>Set-AdfsRelyingPartyTrust -DeviceAuthenticationMethod ClientTLS
```

>[!NOTE]
> Das Aktivieren der Geräte Authentifizierung (festlegen `DeviceAuthenticationEnabled` auf `$true` ) bedeutet `DeviceAuthenticationMethod` , dass implizit auf festgelegt ist `SignedToken` , was dem **PRT**entspricht.


``` powershell
PS:\>Set-AdfsGlobalAuthenticationPolicy –DeviceAuthenticationMethod All
```
> [!NOTE]
> Die Standardmethode für die Geräte Authentifizierung ist `SignedToken` .  Andere Werte sind **pkeyauth,**<strong>clienttls</strong> und **all**.

Die Bedeutung der `DeviceAuthenticationMethod` Werte hat sich seit der Veröffentlichung von AD FS 2016 geringfügig geändert.  In der folgenden Tabelle finden Sie die Bedeutung der einzelnen Werte, abhängig von der Update Ebene:


|AD FS Version|Deviceauthenticationmethod-Wert|Damit|
| ----- | ----- | ----- |
|2016 RTM|Signedtoken|PRT + pkeyauth|
||clientTLS|clientTLS|
||Alle|PRT + pkeyauth + clienttls|
|2016 RTM + aktuell mit Windows Update|Signedtoken (geänderte Bedeutung)|PRT (nur)|
||Pkeyauth (neu)|PRT + pkeyauth|
||clientTLS|PRT + clienttls|
||Alle|PRT + pkeyauth + clienttls|

## <a name="see-also"></a>Weitere Informationen
[AD FS-Vorgänge](../ad-fs-operations.md)
