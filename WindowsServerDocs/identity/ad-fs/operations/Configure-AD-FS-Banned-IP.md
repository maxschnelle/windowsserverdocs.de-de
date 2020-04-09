---
title: Konfigurieren AD FS gesperrten IP-Adressen
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 06/28/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 1a1e8a9e668caa0c766f6fe3012d5ae6ecaddb50
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80859923"
---
# <a name="ad-fs-and-banned-ip-addresses"></a>AD FS und verbotene IP-Adressen


Im Juni 2018 führte AD FS unter Windows Server 2016 die **gesperrten IPS** mit dem Update von AD FS Juni 2018 ein.  Mit diesem Update können Sie einen Satz von IP-Adressen Global in AD FS konfigurieren, sodass Anforderungen, die von diesen IP-Adressen stammen oder die diese IP-Adressen in den Header **x-weitergeleitet-für** oder **x-ms-weitergeleitete Client-IP** aufweisen, durch AD FS blockiert werden.

## <a name="adding-banned-ips"></a>Hinzufügen von gesperrten IPS
Verwenden Sie das folgende PowerShell-Cmdlet, um der globalen Liste verbotene IPS hinzuzufügen:

``` powershell
PS C:\ >Set-AdfsProperties -AddBannedIps "1.2.3.4", "::3", "1.2.3.4/16"
```

Zulässige Formate

1.  IPv4
2.  IPv6
3.  CIDR-Format mit IPv4 oder V6

Es gibt ein Limit von 300 Einträgen für gesperrte IP-Adressen. Sie können CIDR oder das Bereichs Format verwenden, um einen großen Block von Einträgen mit einem einzigen Eintrag zu verweigern.

## <a name="removing-banned-ips"></a>Entfernen von gesperrten IPS
Verwenden Sie das folgende PowerShell-Cmdlet, um die gesperrten IPS aus der globalen Liste zu entfernen:

``` powershell
PS C:\ >Set-AdfsProperties -RemoveBannedIps "1.2.3.4"
```

#### <a name="read-banned-ips"></a>Lesen von gesperrten IPS
Verwenden Sie das folgende PowerShell-Cmdlet, um den aktuellen Satz der gesperrten IP-Adressen zu lesen:

``` powershell
PS C:\ >Get-AdfsProperties 
```

Beispielausgabe:

```
BannedIpList                   : {1.2.3.4, ::3,1.2.3.4/16}
```



## <a name="additional-references"></a>Weitere Verweise  
[Bewährte Methoden zum Sichern von Active Directory-Verbunddienste (AD FS)](../../ad-fs/deployment/best-practices-securing-ad-fs.md)

[Set-ADF sproperties](https://technet.microsoft.com/itpro/powershell/windows/adfs/set-adfsproperties)

[AD FS-Vorgänge](../../ad-fs/AD-FS-2016-Operations.md)
