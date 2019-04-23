---
title: Verwalten von-Bde forcerecovery
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: eecae37c-c9a3-46c5-b615-a0ace1f1d778
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5bf7a913c9c496aebded349731ef965a53c98ac7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59858641"
---
# <a name="manage-bde-forcerecovery"></a>Verwalten von-Bde: Forcerecovery



Erzwingt, dass ein mit BitLocker geschütztes Laufwerk in den Wiederherstellungsmodus beim Neustart. Dieser Befehl löscht alle TPM Trusted Platform Module-bezogene Schlüsselschutzvorrichtungen aus dem Laufwerk. Wenn der Computer neu gestartet wird, kann nur ein Wiederherstellungskennwort oder Wiederherstellungsschlüssel zum Entsperren des Laufwerks verwendet werden. Beispiele wie dieser Befehl verwendet werden kann, finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
manage-bde –forcerecovery <Drive> [-computername <Name>] [{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<Drive>|Stellt einen von einem Doppelpunkt gefolgten Laufwerkbuchstaben dar.|
|-computername|Gibt an, dass bde.exe verwendet wird, um die BitLocker-Schutz auf einem anderen Computer zu ändern. Sie können auch **- Cn** als eine verkürzte Version des mit diesem Befehl.|
|\<Name>|Stellt den Namen des Computers, auf dem BitLocker-Schutz zu ändern. Akzeptierte Werte sind die NetBIOS-Namen des Computers und die IP-Adresse des Computers.|
|-? oder /?|Zeigt eine kurze Hilfe an der Eingabeaufforderung.|
|---Help oder-h|Führen Sie zeigt Hilfe an der Eingabeaufforderung ein.|

## <a name="BKMK_Examples"></a>Beispiele für

Das folgende Beispiel veranschaulicht die Verwendung der **- Forcerecovery** Befehl aus, um BitLocker im Wiederherstellungsmodus befinden, auf dem Laufwerk c: zu verursachen
```
manage-bde –forcerecovery C:
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Befehlszeilensyntax](command-line-syntax-key.md)
-   [Verwalten von-bde](manage-bde.md)