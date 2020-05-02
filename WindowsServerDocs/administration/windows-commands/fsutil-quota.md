---
ms.assetid: 21225c11-7c72-4ea2-96bd-e63d4beb3be5
title: Nicht-Kontingent
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 8079bacaa54282a1dd1091ffacd427ddaf74cc59
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725470"
---
# <a name="fsutil-quota"></a>Nicht-Kontingent
> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8, Windows Server 2008 R2, Windows 7

Verwaltet Datenträger Kontingente auf NTFS-Volumes, um eine präzisere Steuerung des netzwerkbasierten Speichers zu ermöglichen.



## <a name="syntax"></a>Syntax

```
fsutil quota [disable] <VolumePath>
fsutil quota [enforce] <VolumePath>
fsutil quota [modify] <VolumePath> <Threshold> <Limit> <UserName>
fsutil quota [query] <VolumePath>
fsutil quota [track] <VolumePath>
fsutil quota [violations]
```

### <a name="parameters"></a>Parameter

|   Parameter   |                                                                                    BESCHREIBUNG                                                                                    |
|---------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    disable    |                                                         Deaktiviert die Kontingent Verfolgung und-Erzwingung auf dem angegebenen Volume.                                                          |
|    durch    |                                                                   Erzwingt die Kontingent Nutzung auf dem angegebenen Volume.                                                                   |
|    modify     |                                                              Ändert ein vorhandenes Datenträger Kontingent oder erstellt ein neues Kontingent.                                                              |
|     Abfrage     |                                                                            Listet vorhandene Datenträger Kontingente auf.                                                                            |
|     track     |                                                                    Verfolgt die Datenträger Verwendung auf dem angegebenen Volume.                                                                     |
|  Verletzungen   | Durchsucht die System-und Anwendungsprotokolle und zeigt eine Meldung an, um anzugeben, dass Kontingent Verletzungen erkannt wurden oder ob ein Benutzer einen Kontingent Schwellenwert oder eine Kontingent Grenze erreicht hat. |
| \<Volumepath-> |                                  Erforderlich. Gibt den Namen des Laufwerks an, gefolgt von einem Doppelpunkt oder der GUID im Format **Volume {**<em>GUID</em>**}**.                                  |
| \<Schwellenwert>  |                            Legt den Grenzwert (in Bytes) fest, mit dem Warnungen ausgegeben werden. Dieser Parameter ist für den Befehl zum Ändern des Befehls " **ssutil Quota** " erforderlich.                            |
|   \<Limit>    |                                Legt die maximal zulässige Datenträger Verwendung (in Bytes) fest. Dieser Parameter ist für den Befehl zum Ändern des Befehls " **ssutil Quota** " erforderlich.                                |
|  \<Benutzername>  |                                      Gibt den Domänen-oder Benutzernamen an. Dieser Parameter ist für den Befehl zum Ändern des Befehls " **ssutil Quota** " erforderlich.                                       |

## <a name="remarks"></a>Bemerkungen

-   Datenträger Kontingente werden pro Volume implementiert und ermöglichen die Implementierung von Hard-und Soft Storage-Limits auf Benutzerbasis.

-   Mithilfe von Schreib Skripts, bei denen das **fsutil-Kontingent** verwendet wird, können Sie die Kontingent Limits jedes Mal festlegen, wenn Sie einen neuen Benutzer hinzufügen, oder Sie können Kontingent Limits automatisch nachverfolgen, in einen Bericht kompilieren und automatisch per e-Mail an den Systemadministrator senden.

### <a name="examples"></a><a name="BKMK_examples"></a>Beispiele
Zum Auflisten vorhandener Datenträger Kontingente für ein Datenträger Volume, das mit der GUID {928842df-5a01-11de-a85c-806e6f6e6963} angegeben ist, geben Sie Folgendes ein:

```
fsutil quota query Volume{928842df-5a01-11de-a85c-806e6f6e6963}
```

Zum Auflisten vorhandener Datenträger Kontingente für ein Datenträger Volume, das mit dem Laufwerk Buchstaben " **C:**" angegeben ist, geben Sie Folgendes ein:

```
Fsutil quota query C:
```

## <a name="additional-references"></a>Zusätzliche Referenzen
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

[Fsutil](Fsutil.md)


