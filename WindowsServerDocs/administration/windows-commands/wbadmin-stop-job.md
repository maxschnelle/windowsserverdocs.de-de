---
title: Auftrag zum Beenden des Wbadmin
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3b83b398-39c7-4410-bf17-5c1fb1a4f46d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7a9e71fe2e4883c52c2418e21fc8764fd14e6c81
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59889721"
---
# <a name="wbadmin-stop-job"></a>Auftrag zum Beenden des Wbadmin



Bricht ab, der Backup- oder Recovery-Vorgang, der derzeit ausgeführt wird. Abgebrochenen Vorgänge nicht neu gestartet werden – Sie müssen erneut ausführen, einen abgebrochenen Backup- oder Recovery-Vorgang ab.

Um einen sicherungs- oder Wiederherstellungsaufgaben-Vorgang mit diesen Unterbefehl zu beenden, müssen Sie Mitglied werden die **Sicherungs-Operatoren** Gruppe oder die **Administratoren** Gruppe, oder Sie wurde die entsprechende Berechtigung delegiert. Darüber hinaus müssen Sie ausführen **Wbadmin** eine Eingabeaufforderung mit erhöhten Rechten. (Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten mit der rechten Maustaste **Eingabeaufforderung** , und klicken Sie dann auf **als Administrator ausführen**.)

## <a name="syntax"></a>Syntax

```
wbadmin stop job
[-quiet]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|-quiet|Wird keine aufforderungen den Unterbefehl für dem Benutzer ausgeführt.|

#### <a name="additional-references"></a>Weitere Verweise

-   [Befehlszeilensyntax](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)