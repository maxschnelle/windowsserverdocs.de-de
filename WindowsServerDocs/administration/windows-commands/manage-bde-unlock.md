---
title: "\"manage-bde Unlock\""
description: Referenz Artikel für den Befehl manage-bde Unlock, mit dem ein durch BitLocker geschütztes Laufwerk mithilfe eines Wiederherstellungs Kennworts oder eines Wiederherstellungs Schlüssels entsperrt wird.
ms.topic: article
ms.assetid: 7852bf7d-9102-40be-adcb-71e8f4dfde72
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d9b13e4ac27ab77a522d223749cd84e3b1bb11a6
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87886648"
---
# <a name="manage-bde-unlock"></a>"manage-bde Unlock"

Entsperrt ein durch BitLocker geschütztes Laufwerk mit einem Wiederherstellungs Kennwort oder einem Wiederherstellungs Schlüssel.

## <a name="syntax"></a>Syntax

```
manage-bde -unlock {-recoverypassword <password>|-recoverykey <pathtoexternalkeyfile>} <drive> [-certificate {-cf pathtocertificatefile | -ct certificatethumbprint} {-pin}] [-password] [-computername <name>] [{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| -wiederherstellungkennwort | Gibt an, dass ein Wiederherstellungs Kennwort verwendet wird, um das Laufwerk zu entsperren. Sie können auch **-RP** als abgekürzte Version dieses Befehls verwenden. |
| `<password>` | Stellt das Wiederherstellungs Kennwort dar, das verwendet werden kann, um das Laufwerk zu entsperren. |
| -Wiederherstellungsschlüssel | Gibt an, dass eine externe Wiederherstellungs Schlüsseldatei verwendet wird, um das Laufwerk zu entsperren. Sie können " **-RK** " auch als abgekürzte Version dieses Befehls verwenden. |
| `<pathtoexternalkeyfile>` | Stellt die externe Wiederherstellungs Schlüsseldatei dar, die zum Entsperren des Laufwerks verwendet werden kann. |
| `<drive>` | Stellt einen von einem Doppelpunkt gefolgten Laufwerkbuchstaben dar. |
| -Zertifikat | Das lokale Benutzerzertifikat für ein BitLocker-Zertifikat zum Entsperren des Volumes befindet sich im lokalen Zertifikat Speicher des Benutzers. Sie können auch **-CERT** als abgekürzte Version dieses Befehls verwenden. |
| -CF`<pathtocertificatefile>` | Pfad zur Zertifikatsdatei |
| -CT`<certificatethumbprint>` | Der Zertifikat Fingerabdruck, der optional die PIN (-PIN) enthalten kann. |
| -password | Zeigt eine Eingabeaufforderung für das Kennwort zum Entsperren des Volumes an. Sie können auch **-PW** als abgekürzte Version dieses Befehls verwenden. |
| -Computername | Gibt an, dass manage-bde.exe zum Ändern des BitLocker-Schutzes auf einem anderen Computer verwendet wird. Sie können auch **-CN** als abgekürzte Version dieses Befehls verwenden. |
| `<name>` | Stellt den Namen des Computers dar, auf dem der BitLocker-Schutz geändert werden soll. Akzeptierte Werte sind der NetBIOS-Name des Computers und die IP-Adresse des Computers. |
| -? oder /? | Zeigt eine kurze Hilfe an der Eingabeaufforderung an. |
| -Help oder-h | Zeigt die gesamte Hilfe an der Eingabeaufforderung an. |

### <a name="examples"></a>Beispiele

Zum Entsperren von Laufwerk E mit einer Wiederherstellungs Schlüsseldatei, die in einem Sicherungsordner auf einem anderen Laufwerk gespeichert wurde, geben Sie Folgendes ein:

```
manage-bde –unlock E: -recoverykey F:\Backupkeys\recoverykey.bek
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "Manage-BDE"](manage-bde.md)
