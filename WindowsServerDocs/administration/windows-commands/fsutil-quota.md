---
title: fsutil quota
description: Referenz Thema für den Befehl "fsutil Quota", der Datenträger Kontingente auf NTFS-Volumes verwaltet, um eine präzisere Steuerung des netzwerkbasierten Speichers zu ermöglichen.
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
ms.assetid: 21225c11-7c72-4ea2-96bd-e63d4beb3be5
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 54c4f6fe5fd5ae7a43d5057cd5837374f1b94ecd
ms.sourcegitcommit: bf887504703337f8ad685d778124f65fe8c3dc13
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/16/2020
ms.locfileid: "83435815"
---
# <a name="fsutil-quota"></a>fsutil quota

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8

Verwaltet Datenträger Kontingente auf NTFS-Volumes, um eine präzisere Steuerung des netzwerkbasierten Speichers zu ermöglichen.

## <a name="syntax"></a>Syntax

```
fsutil quota [disable] <volumepath>
fsutil quota [enforce] <volumepath>
fsutil quota [modify] <volumepath> <threshold> <limit> <username>
fsutil quota [query] <volumepath>
fsutil quota [track] <volumepath>
fsutil quota [violations]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| disable | Deaktiviert die Kontingent Verfolgung und-Erzwingung auf dem angegebenen Volume. |
| durch | Erzwingt die Kontingent Nutzung auf dem angegebenen Volume. |
| modify | Ändert ein vorhandenes Datenträger Kontingent oder erstellt ein neues Kontingent. |
| Abfrage | Listet vorhandene Datenträger Kontingente auf. |
| track | Verfolgt die Datenträger Verwendung auf dem angegebenen Volume. |
| Verletzungen | Durchsucht die System-und Anwendungsprotokolle und zeigt eine Meldung an, um anzugeben, dass Kontingent Verletzungen erkannt wurden oder ob ein Benutzer einen Kontingent Schwellenwert oder eine Kontingent Grenze erreicht hat. |
| `<volumepath>` | Erforderlich. Gibt den Namen des Laufwerks gefolgt von einem Doppelpunkt oder der GUID im Format an `volume{GUID}` . |
| `<threshold>`  | Legt den Grenzwert (in Bytes) fest, mit dem Warnungen ausgegeben werden. Dieser Parameter ist für den `fsutil quota modify` Befehl erforderlich. |
| `<limit>` | Legt die maximal zulässige Datenträger Verwendung (in Bytes) fest. Dieser Parameter ist für den `fsutil quota modify` Befehl erforderlich. |
| `<username>` | Gibt den Domänen-oder Benutzernamen an. Dieser Parameter ist für den `fsutil quota modify` Befehl erforderlich. |

#### <a name="remarks"></a>Hinweise

- Datenträger Kontingente werden pro Volume implementiert und ermöglichen die Implementierung von Hard-und Soft Storage-Limits auf Benutzerbasis.

- Mithilfe von Schreib Skripts, bei denen das **fsutil-Kontingent** verwendet wird, können Sie die Kontingent Limits jedes Mal festlegen, wenn Sie einen neuen Benutzer hinzufügen, oder Sie können Kontingent Limits automatisch nachverfolgen, in einen Bericht kompilieren und automatisch per e-Mail an den Systemadministrator senden.

### <a name="examples"></a>Beispiele

Zum Auflisten vorhandener Datenträger Kontingente für ein Datenträger Volume, das mit der GUID {928842df-5a01-11de-a85c-806e6f6e6963} angegeben ist, geben Sie Folgendes ein:

```
fsutil quota query volume{928842df-5a01-11de-a85c-806e6f6e6963}
```

Zum Auflisten vorhandener Datenträger Kontingente für ein Datenträger Volume, das mit dem Laufwerk Buchstaben " **C:**" angegeben ist, geben Sie Folgendes ein:

```
fsutil quota query C:
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [fsutil](fsutil.md)
