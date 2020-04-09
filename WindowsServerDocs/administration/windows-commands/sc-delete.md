---
title: SC löschen
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2fe94fb3-e4d1-47b5-b999-39995ecbb644
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 05b276de04d4250cc03e4b2976bf8c1330ef82ce
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80835383"
---
# <a name="sc-delete"></a>SC löschen



Löscht einen Dienst Unterschlüssel aus der Registrierung. Wenn der Dienst ausgeführt wird oder wenn ein anderer Prozess über ein geöffnetes Handle für den Dienst verfügt, wird der Dienst zum Löschen markiert.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#examples).

## <a name="syntax"></a>Syntax

```
sc [<ServerName>] delete [<ServiceName>]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<Servername >|Gibt den Namen des Remote Servers an, auf dem sich der Dienst befindet. Der Name muss das Universal Naming Convention Format (UNC) verwenden (z. b. \\\\MyServer). Wenn Sie "SC. exe" lokal ausführen möchten, lassen Sie diesen Parameter Weg.|
|\<ServiceName >|Gibt den Dienstnamen an, der vom **getkeyname** -Vorgang zurückgegeben wird.|
|?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

Verwenden **Sie** die Option "Software" in der **Systemsteuerung** , um DHCP, DNS oder andere integrierte Betriebssystem Dienste zu löschen. Beachten Sie, dass durch **Hinzufügen oder entfernen** von Software nicht nur der Registrierungs Unterschlüssel für den Dienst entfernt, sondern auch der Dienst deinstalliert und Verknüpfungen zu diesem Dienst gelöscht werden.

## <a name="examples"></a>Beispiele

Um den Dienst Unterschlüssel **newserv** aus der Registrierung auf dem lokalen Computer zu löschen, geben Sie Folgendes ein:
```
sc delete newserv
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)