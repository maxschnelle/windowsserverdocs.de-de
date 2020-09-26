---
title: secedit import
description: Referenz Artikel für den Befehl secedit Import, der die Sicherheitseinstellungen (INF-Datei) importiert, die zuvor aus der mit Sicherheits Vorlagen konfigurierten Datenbank exportiert wurden.
ms.topic: reference
ms.assetid: 1dd59d4c-9d48-444a-871b-b957eb682597
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 35705012d32a196934c0834b3de0c67f7210270b
ms.sourcegitcommit: e164aeffc01069b8f1f3248bf106fcdb7f64f894
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/26/2020
ms.locfileid: "91388233"
---
# <a name="secedit-import"></a>secedit/Import

Importiert Sicherheitseinstellungen (INF-Datei), die zuvor aus der mit Sicherheits Vorlagen konfigurierten Datenbank exportiert wurden.

> [!IMPORTANT]
> Bevor Sie eine INF-Datei auf einen anderen Computer importieren, müssen Sie den `secedit /generaterollback` Befehl in der Datenbank ausführen, für die der Import ausgeführt wird.
>
> Sie müssen auch den `secedit /validate` Befehl für die Import Datei ausführen, um deren Integrität zu überprüfen.

## <a name="syntax"></a>Syntax

```
secedit /import /db <database file name> /cfg <configuration file name> [/overwrite] [/areas [securitypolicy | group_mgmt | user_rights | regkeys | filestore | services]] [/log <log file name>] [/quiet]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| /db | Erforderlich. Gibt den Pfad und den Dateinamen der Datenbank an, die die gespeicherte Konfiguration enthält, für die der Import ausgeführt wird. Wenn der Dateiname eine Datenbank angibt, der keine Sicherheits Vorlage (wie durch die Konfigurationsdatei dargestellt) zugeordnet ist, muss die `/cfg <configuration file name>` Option ebenfalls angegeben werden. |
| /overwrite | Gibt an, ob die Sicherheits Vorlage im **/cfg** -Parameter alle Vorlagen oder Verbund Vorlagen überschreiben soll, die in der Datenbank gespeichert sind, anstatt die Ergebnisse an die gespeicherte Vorlage zu anhängen. Diese Option ist nur gültig, wenn der- `/cfg <configuration file name>` Parameter ebenfalls verwendet wird. Wenn dieser Parameter nicht auch angegeben wird, wird die Vorlage im **/cfg** -Parameter an die gespeicherte Vorlage angehängt. |
| /cfg | Erforderlich. Gibt den Pfad und den Dateinamen für die Sicherheits Vorlage an, die zur Analyse in die Datenbank importiert werden. Diese Option ist nur gültig, wenn Sie mit dem-Parameter verwendet wird `/db <database file name>` . Wenn dieser Parameter nicht auch angegeben wird, wird die Analyse für jede Konfiguration ausgeführt, die bereits in der Datenbank gespeichert ist. |
| /areas | Gibt die Sicherheitsbereiche an, die auf das System angewendet werden sollen. Wenn dieser Parameter nicht angegeben wird, werden alle in der Datenbank definierten Sicherheitseinstellungen auf das System angewendet. Zum Konfigurieren mehrerer Bereiche trennen Sie jeden Bereich durch ein Leerzeichen. Die folgenden Sicherheitsbereiche werden unterstützt:<ul><li>**SecurityPolicy:** Lokale Richtlinie und Domänen Richtlinie für das System, einschließlich Konto Richtlinien, Überwachungs Richtlinien, Sicherheitsoptionen usw.</li><li>  **GROUP_MGMT:** Eingeschränkte Gruppeneinstellungen für alle Gruppen, die in der Sicherheits Vorlage angegeben sind.</li><li>**USER_RIGHTS:** Benutzer Anmelde Rechte und erteilen von Berechtigungen.</li><li>**Regkeys:** Sicherheit für lokale Registrierungsschlüssel.</li><li>**Dateispeicher:** Sicherheit im lokalen Dateispeicher.</li><li>**Dienste:** Sicherheit für alle definierten Dienste.</li></ul> |
| /Log | Gibt den Pfad und den Dateinamen der Protokolldatei an, die im Prozess verwendet werden soll. Wenn Sie keinen Speicherort für die Datei angeben, wird die Standardprotokoll Datei `<systemroot>\Documents and Settings\<UserAccount>\My Documents\Security\Logs\<databasename>.log` verwendet. |
| /quiet | Unterdrückt die Bildschirm-und Protokoll Ausgabe. Sie können weiterhin Analyseergebnisse anzeigen, indem Sie das Snap-in "Sicherheitskonfiguration und-Analyse" in der Microsoft Management Console (MMC) verwenden. |

## <a name="examples"></a>Beispiele

Wenn Sie die Sicherheitsdatenbank und die Domänen Sicherheitsrichtlinien in eine INF-Datei exportieren und diese Datei dann in eine andere Datenbank importieren möchten, um die Richtlinien Einstellungen auf einem anderen Computer zu replizieren, geben Sie Folgendes ein:

```
secedit /export /db C:\Security\FY11\SecDbContoso.sdb /mergedpolicy /cfg NetworkShare\Policies\SecContoso.inf /log C:\Security\FY11\SecAnalysisContosoFY11.log /quiet
```

Geben Sie Folgendes ein, um nur den Sicherheitsrichtlinien Teil der Datei in eine andere Datenbank auf einem anderen Computer zu importieren:

```
secedit /import /db C:\Security\FY12\SecDbContoso.sdb /cfg NetworkShare\Policies\SecContoso.inf /areas securitypolicy /log C:\Security\FY11\SecAnalysisContosoFY12.log /quiet
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [secedit/analyze](secedit-analyze.md)

- [secedit/configure](secedit-configure.md)

- [secedit/Export](secedit-export.md)

- [secedit/generaterollback](secedit-generaterollback.md)

- [secedit/Validate](secedit-validate.md)