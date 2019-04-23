---
title: ksetup:addkpasswd
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d3196995-1b38-48ff-ba08-911cfab77317
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2a85eb6dfe30c33126504744a7659fe2cc573087
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59856821"
---
# <a name="ksetupaddkpasswd"></a>ksetup:addkpasswd



Fügt eine Kerberos-Kennwort (Kpasswd)-Serveradresse für einen Bereich hinzu. Beispiele wie dieser Befehl verwendet werden kann, finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
ksetup /addkpasswd <RealmName> [<KpasswdName>]
```

### <a name="parameters"></a>Parameter

Wenn die Kerberos-Bereich, dass die Arbeitsstation für die Unterstützung der Kerberos authentifiziert wird Password Protokoll ändern, können Sie einen Clientcomputer mit dem Windows-Betriebssystem um ein Kerberos-Kennwort-Server verwenden konfigurieren. Diese Einstellung wird auf der Seite Bereich konfiguriert.

|Parameter|Beschreibung|
|---------|-----------|
|\<RealmName>|Der Bereichsname ist als Großbuchstaben DNS-Name, wie z. B. CORP. angegeben. "Contoso.com", und als Standard-Bereich oder einen Bereich = Wenn **Ksetup** ausgeführt wird.|
|\<KpasswdName>|Der KDC-Name, der als Kerberos-Kennwort-Server verwendet werden soll, die als Groß-und Kleinschreibung den vollqualifizierten Domänennamen, z. B. mitkdc.microsoft.com angegeben ist. Der KDC-Name fehlt, möglicherweise DNS verwendet werden, um KDCs zu suchen.|

## <a name="remarks"></a>Hinweise

Wenn die Kerberos-Bereich, dass die Arbeitsstation für die Unterstützung der Kerberos authentifiziert wird Password Protokoll ändern, können Sie einen Clientcomputer mit dem Windows-Betriebssystem um ein Kerberos-Kennwort-Server verwenden konfigurieren.

Führen Sie den Befehl **Ksetup** den KDC-Namen überprüfen. Wenn **Kpasswd =** erscheint nicht in der Ausgabe die Zuordnung wurde nicht konfiguriert.

Sie können zusätzliche KDC Namen einer zu einem Zeitpunkt hinzufügen.

## <a name="BKMK_Examples"></a>Beispiele für

Konfigurieren Sie den Bereich, CORP. "Contoso.com", und die It den nicht - Windows-KDC-Server, mitkdc.contoso.com, als die Kennwort-Server verwendet:
```
ksetup /addkpasswd CORP.CONTOSO.COM mitkdc.contoso.com
```
Dies führt zu einem nicht - Windows-Kerberos Kennwortserver, der alle Kennwörter für die Authentifizierung zwischen diesem und den Bereich steuert.

#### <a name="additional-references"></a>Weitere Verweise

-   [Ksetup](ksetup.md)
-   [Ksetup:delkpasswd](ksetup-delkpasswd.md)
-   [Befehlszeilensyntax](command-line-syntax-key.md)