---
ms.assetid: 21225c11-7c72-4ea2-96bd-e63d4beb3be5
title: Fsutil quota
ms.prod: windows-server-threshold
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 2daa2f6253a406ccad68677e1877215a1c610328
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59835291"
---
# <a name="fsutil-quota"></a>Fsutil quota
>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, WindowsServer 2012, Windows 8, Windows Server 2008 R2, Windows 7

Verwaltet Datenträgerkontingente auf NTFS-Volumes, um eine genauere Steuerung der Netzwerk-basierten Speicher bereitzustellen.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
fsutil quota [disable] <VolumePath>
fsutil quota [enforce] <VolumePath>
fsutil quota [modify] <VolumePath> <Threshold> <Limit> <UserName>
fsutil quota [query] <VolumePath>
fsutil quota [track] <VolumePath>
fsutil quota [violations]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|-------------|---------------|
|Deaktivieren|Deaktiviert die Kontingente, die nachverfolgung und Erzwingung auf dem angegebenen Volume.|
|erzwingen|Erzwingt die Speicherverwendung auf dem angegebenen Volume.|
|ändern|Ändert ein vorhandenes Datenträgerkontingent aus, oder erstellt ein neues Kontingent.|
|query|Listet vorhandene Datenträgerkontingente.|
|Nachverfolgen|Verfolgt die Datenträgerverwendung auf dem angegebenen Volume.|
|Leistungsverletzungen|Sucht die System- und Anwendungsprotokolle, und zeigt eine Meldung, um anzugeben, dass es sich bei kontingentverletzungen erkannt wurden oder dass ein Benutzer eine Kontingentgrenze Schwellenwert oder das Kontingent erreicht hat.|
|\<VolumePath>|Erforderlich. Gibt den Namen des Laufwerks, gefolgt von einem Doppelpunkt oder die GUID im Format **Volume {***GUID***}**.|
|\<Threshold>|Legt das Limit (in Byte), an dem Warnungen ausgegeben werden. Dieser Parameter ist erforderlich, damit die **Fsutil Kontingent ändern** Befehl.|
|\<Limit>|Legt die maximale zulässige Datenträgerverwendung (in Bytes) fest. Dieser Parameter ist erforderlich, damit die **Fsutil Kontingent ändern** Befehl.|
|\<Benutzername >|Gibt die Namen der Domäne oder Benutzer an. Dieser Parameter ist erforderlich, damit die **Fsutil Kontingent ändern** Befehl.|

## <a name="remarks"></a>Hinweise

-   Datenträgerkontingente werden individuell pro Volume implementiert, und beide harten und weichen Speicherlimits auf pro-Benutzer implementiert werden können.

-   Können Sie Skripts schreiben, mit denen **Fsutil Kontingent** jedes Mal, wenn Sie einen neuen Benutzer hinzuzufügen, legen Sie die Kontingentgrenzen überschritten oder Kontingentgrenzen automatisch nachverfolgen, in einem Bericht kompilieren und diese automatisch an den Systemadministrator per E-mail zu senden.

### <a name="BKMK_examples"></a>Beispiele für
Geben Sie zum Auflisten der vorhandenen Datenträgers Kontingente für Volumes, die mit der GUID, {928842df-5a01-11de-a85c-806e6f6e6963}, angegeben wird:

```
fsutil quota query Volume{928842df-5a01-11de-a85c-806e6f6e6963}
```

Vorhandenen Datenträgerkontingente für ein Datenträgervolume aufgelistet, die mit dem Laufwerkbuchstaben angegeben wird **C:**, Typ:

```
Fsutil quota query C:
```

#### <a name="additional-references"></a>Weitere Verweise
[Befehlszeilensyntax](Command-Line-Syntax-Key.md)

[Fsutil](Fsutil.md)


