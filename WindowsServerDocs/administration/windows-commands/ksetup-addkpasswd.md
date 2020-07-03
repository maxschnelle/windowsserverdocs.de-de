---
title: ksetup addkpasswd
description: Referenz Artikel für den Befehl "Ksetup addkpasswd", mit dem ein Kerberos-Kennwort (kpasswd)-Server Adresse für einen Bereich hinzugefügt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d3196995-1b38-48ff-ba08-911cfab77317
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2db728684e713df35a39995c8ca95196f0b745ed
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85925552"
---
# <a name="ksetup-addkpasswd"></a>ksetup addkpasswd

Fügt ein Kerberos-Kennwort (kpasswd)-Server Adresse für einen Bereich hinzu.

## <a name="syntax"></a>Syntax

```
ksetup /addkpasswd <realmname> [<kpasswdname>]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| `<realmname>` | Gibt den Großbuchstaben-DNS-Namen an, z. b. Corp. CONTOSO.com, und wird als Standardbereich bzw. **Bereich** angezeigt, wenn **Ksetup** ausgeführt wird. |
| `<kpasswdname>` | Gibt den Kerberos-Kenn Wort Server an. Sie wird als voll qualifizierter Domänen Name, wie z. b. mitkdc.contoso.com, als Nichtbeachtung der Groß-/Kleinschreibung angegeben. Wenn der KDC-Name weggelassen wird, kann DNS verwendet werden, um nach KDCs zu suchen. |

#### <a name="remarks"></a>Hinweise

- Wenn der Kerberos-Bereich, bei dem die Arbeitsstation authentifiziert wird, das Kerberos-Änderungs Kennwort-Protokoll unterstützt, können Sie einen Client Computer mit dem Windows-Betriebssystem für die Verwendung eines Kerberos-Kenn Wort Servers konfigurieren.

- Sie können weitere KDC-Namen einzeln hinzufügen.

### <a name="examples"></a>Beispiele

Zum Konfigurieren des Corp. CONTOSO.com Bereich zum Verwenden des nicht-Windows-KDC-Servers, mitkdc.contoso.com, als Kennwort-Server, geben Sie Folgendes ein:

```
ksetup /addkpasswd CORP.CONTOSO.COM mitkdc.contoso.com
```

Um sicherzustellen, dass der KDC-Name festgelegt ist, geben Sie ein, und zeigen Sie `ksetup` die Ausgabe an, und suchen Sie nach dem Text **kpasswd =** Wenn der Text nicht angezeigt wird, bedeutet dies, dass die Zuordnung nicht konfiguriert wurde.

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Ksetup-Befehl](ksetup.md)

- [Ksetup-Befehl "Delta passwd"](ksetup-delkpasswd.md)
