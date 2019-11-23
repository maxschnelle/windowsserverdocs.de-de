---
title: SC löschen
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2fe94fb3-e4d1-47b5-b999-39995ecbb644
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ad64d0f7c772b8d29a191b5f3e690d74c8765717
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71371277"
---
# <a name="sc-delete"></a>SC löschen



Löscht einen Dienst Unterschlüssel aus der Registrierung. Wenn der Dienst ausgeführt wird oder wenn ein anderer Prozess über ein geöffnetes Handle für den Dienst verfügt, wird der Dienst zum Löschen markiert.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#examples).

## <a name="syntax"></a>Syntax

```
sc [<ServerName>] delete [<ServiceName>]
```

## <a name="parameters"></a>Parameter

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

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)