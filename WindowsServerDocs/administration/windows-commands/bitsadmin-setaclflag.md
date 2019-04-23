---
title: bitsadmin setaclflag
description: Windows-Befehle Thema **Bitsadmin Setaclflag** -legt die Zugriffssteuerung Liste zur Weitergabe von Würmern Flags.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6e3bcda0-827d-4dfd-8384-d1da018f3e10
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 89d825a4bc4512022fed98a3188537d3977fa3c3
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59867401"
---
# <a name="bitsadmin-setaclflag"></a>bitsadmin setaclflag

Legt die Access Control-Zugriffssteuerungsliste (ACL) zur Weitergabe von Würmern-Flags für den Auftrag fest. Die Flags geben an, dass Sie den Besitzer und die ACL-Informationen mit den herunterzuladenden Datei beibehalten möchten. Um den Besitzer und die Gruppe mit der Datei zu gewährleisten, legen Sie z. B. **Flags** zu `OG`.

## <a name="syntax"></a>Syntax

```
bitsadmin /SetAclFlags <Job> <Flags>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Anzeigenamen oder die GUID des Auftrags|
|Flags|Geben Sie eine oder mehrere der folgenden Flags Werte an:</br>-O: Kopieren Sie Informationen über den sperrbesitzer-Datei.</br>-   G: Kopieren Sie Informationen zur Datei.</br>-   D: Kopieren Sie DACL-Informationen, mit der Datei.</br>-S: Kopie SACL Informationen mit der Datei.|

## <a name="remarks"></a>Hinweise

Der SetAclFlags-Schalter wird verwendet, um Informationen für Besitzer und Access Control List zu verwalten, beim Herunterladen eines Auftrags Daten von einer Freigabe (SMB)-Windows.

## <a name="BKMK_examples"></a>Beispiele für

Im folgenden Beispiel wird die Zugriffssteuerung Liste Weitergabeflags für den Auftrag mit dem Namen *MyDownloadJob* können Sie den Besitzer und die Gruppe Informationen mit den heruntergeladenen Dateien zu verwalten.
```
C:\>bitsadmin /setaclflags myDownloadJob OG
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)