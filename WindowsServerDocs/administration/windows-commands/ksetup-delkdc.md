---
title: ksetup delkdc
description: Referenz Artikel zum Befehl "Ksetup Delta DC", der Instanzen von Schlüsselverteilungscenter Namen (KDC) für den Kerberos-Bereich löscht.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7d6ec389-094c-4a7b-a78b-605497ddc289
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2d0477fd7317b0b9424fd6199cfde268c00dd1d6
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85926127"
---
# <a name="ksetup-delkdc"></a>ksetup delkdc

Löscht Instanzen von Schlüsselverteilungscenter Namen (KDC) für den Kerberos-Bereich.

Die Zuordnung wird in der Registrierung unter gespeichert `HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\LSA\Kerberos\Domains` . Nachdem Sie diesen Befehl ausgeführt haben, sollten Sie sicherstellen, dass der KDC entfernt wurde und nicht mehr in der Liste angezeigt wird.

> [!NOTE]
> Um Bereichs Konfigurationsdaten von mehreren Computern zu entfernen, verwenden Sie das Snap-in " **Sicherheits Konfigurations Vorlage** " mit der Richtlinien Verteilung, anstatt den **Ksetup** -Befehl explizit auf einzelnen Computern zu verwenden.

## <a name="syntax"></a>Syntax

```
ksetup /delkdc <realmname> <KDCname>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| `<realmname>` | Gibt den Großbuchstaben-DNS-Namen an, z. b. Corp. CONTOSO.com. Dies ist der Standardbereich, der angezeigt wird, wenn Sie den Befehl " **Ksetup** " ausführen, und es handelt sich um den Bereich, aus dem Sie den KDC löschen möchten. |
| `<KDCname>` | Gibt den voll qualifizierten Domänen Namen für die Groß-und Kleinschreibung an, z. b. mitkdc.contoso.com. |

### <a name="examples"></a>Beispiele

Um alle Zuordnungen zwischen dem Windows-Bereich und dem nicht-Windows-Bereich anzuzeigen und zu bestimmen, welche entfernt werden sollen, geben Sie Folgendes ein:

```
ksetup
```

Um die Zuordnung zu entfernen, geben Sie Folgendes ein:

```
ksetup /delkdc CORP.CONTOSO.COM mitkdc.contoso.com
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Ksetup-Befehl](ksetup.md)

- [Befehl "Ksetup addkdc"](ksetup-addkdc.md)