---
title: ksetup:delkpasswd
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2db0bfcd-bc08-48e3-9f30-65b6411839c6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e487389e0f27f58aacaea2b81d573dc9a965e42f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59889081"
---
# <a name="ksetupdelkpasswd"></a>ksetup:delkpasswd

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Entfernt einen Kerberos-Kennwort-Server (Kpasswd) für einen Bereich. Beispiele wie dieser Befehl verwendet werden kann, finden Sie unter [Beispiele](#BKMK_Examples).
## <a name="syntax"></a>Syntax
```
ksetup /delkpasswd <RealmName> <KpasswdName>
```
### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|<RealmName>|Der Bereichsname ist als Großbuchstaben DNS-Name, wie z. B. CORP. angegeben. "Contoso.com", und als Standard-Bereich oder einen Bereich = Wenn **Ksetup** ausgeführt wird.|
|<KpasswdName>|Der KDC-Name, der als Kerberos-Kennwort-Server verwendet werden, die als Groß-/Kleinschreibung, den vollqualifizierten Domänennamen, z. B. mitkdc.contoso.com angegeben ist. Der KDC-Name fehlt, möglicherweise DNS verwendet werden, um KDCs zu suchen.|
## <a name="remarks"></a>Hinweise
Führen Sie den Befehl **Ksetup** den KDC-Namen überprüfen. Wenn **Kpasswd =** wird nicht in der Ausgabe angezeigt, und klicken Sie dann die Zuordnung nicht konfiguriert wurde. Mehrere Zuordnungen werden ebenfalls aufgelistet, wenn festgelegt.
## <a name="BKMK_Examples"></a>Beispiele für
Überprüfen Sie den Bereich CORP. "Contoso.com" verwendet den nicht - Windows-KDC-Server-mitkdc.contoso.com wie der Kennwortserver:
```
ksetup /delkpasswd CORP.CONTOSO.COM mitkdc.contoso.com
```
Führen Sie zum Überprüfen der Befehl erfolgreich ausgeführt wurde wie vorgesehen **Ksetup** auf dem Windows-Computer, um zu überprüfen, ob den Bereich CORP. "Contoso.com" ist nicht mit einem Kerberos-Kennwort-Server (der KDC-Name) zugeordnet.
## <a name="additional-references"></a>Zusätzliche Referenzen
-   [ksetup](ksetup.md)
-   [ksetup:delkpasswd](ksetup-delkpasswd.md)
-   [Befehlszeilensyntax](command-line-syntax-key.md)
