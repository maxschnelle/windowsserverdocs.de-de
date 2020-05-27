---
title: Ksetup-Delta Pass WD
description: Referenz Thema für den Ksetup-Befehl "Delta Pass WD", mit dem ein Kerberos-Kenn Wort Server (kpasswd) für einen Bereich entfernt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2db0bfcd-bc08-48e3-9f30-65b6411839c6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a84a70158ad707fb36d1ca8a4879a93fe0b7df06
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2020
ms.locfileid: "83817840"
---
# <a name="ksetup-delkpasswd"></a>Ksetup-Delta Pass WD

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Entfernt einen Kerberos-Kenn Wort Server (kpasswd) für einen Bereich.

## <a name="syntax"></a>Syntax

```
ksetup /delkpasswd <realmname> <kpasswdname>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<realmname>` |  Gibt den Großbuchstaben-DNS-Namen an, z. b. Corp. CONTOSO.com, und wird als Standardbereich bzw. **Bereich** angezeigt, wenn **Ksetup** ausgeführt wird. |
| `<kpasswdname>` | Gibt den Kerberos-Kenn Wort Server an. Sie wird als voll qualifizierter Domänen Name, wie z. b. mitkdc.contoso.com, als Nichtbeachtung der Groß-/Kleinschreibung angegeben. Wenn der KDC-Name weggelassen wird, kann DNS verwendet werden, um nach KDCs zu suchen. |

### <a name="examples"></a>Beispiele

Um sicherzustellen, dass der Bereich Corp. CONTOSO.com verwendet den nicht-Windows-KDC-Server mitkdc.contoso.com wie den Kennwort-Server, geben Sie Folgendes ein:

```
ksetup /delkpasswd CORP.CONTOSO.COM mitkdc.contoso.com
```

Um sicherzustellen, dass der Bereich Corp. CONTOSO.com ist keinem Kerberos-Kenn Wort Server (KDC-Name) zugeordnet, geben Sie `ksetup` auf dem Windows-Computer ein, und zeigen Sie die Ausgabe an.

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Ksetup-Befehl](ksetup.md)

- [Ksetup-Befehl "Delta passwd"](ksetup-delkpasswd.md)
