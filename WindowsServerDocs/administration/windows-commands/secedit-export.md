---
title: secedit export
description: Referenz Artikel für den secedit-Export, der Sicherheitseinstellungen exportiert, die in einer mit Sicherheits Vorlagen konfigurierten Datenbank gespeichert sind.
ms.topic: reference
ms.assetid: 49a8b241-aa8c-45b7-844d-67a29fab708e
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: dfd766674a4e4ac2e9552d36b4cb706117c173bd
ms.sourcegitcommit: e164aeffc01069b8f1f3248bf106fcdb7f64f894
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/26/2020
ms.locfileid: "91388243"
---
# <a name="secedit-export"></a>secedit/Export

Exportiert Sicherheitseinstellungen, die in einer Datenbank gespeichert sind, die mit Sicherheits Vorlagen konfiguriert wurde. Sie können diesen Befehl verwenden, um Ihre Sicherheitsrichtlinien auf einem lokalen Computer zu sichern, zusätzlich zum Importieren der Einstellungen auf einen anderen Computer.

## <a name="syntax"></a>Syntax

```
secedit /export /db <database file name> [/mergedpolicy] /cfg <configuration file name> [/areas [securitypolicy | group_mgmt | user_rights | regkeys | filestore | services]] [/log <log file name>] [/quiet]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| /db | Erforderlich. Gibt den Pfad und den Dateinamen der Datenbank an, die die gespeicherte Konfiguration enthält, für die der Export ausgeführt wird. Wenn der Dateiname eine Datenbank angibt, der keine Sicherheits Vorlage (wie durch die Konfigurationsdatei dargestellt) zugeordnet ist, muss die `/cfg <configuration file name>` Option ebenfalls angegeben werden. |
| /mergedpolicy | Führt die Sicherheitseinstellungen für die Domäne und die lokale Richtlinie zusammen. |
| /cfg | Erforderlich. Gibt den Pfad und den Dateinamen für die Sicherheits Vorlage an, die zur Analyse in die Datenbank importiert werden. Diese Option ist nur gültig, wenn Sie mit dem-Parameter verwendet wird `/db <database file name>` . Wenn dieser Parameter nicht auch angegeben wird, wird die Analyse für jede Konfiguration ausgeführt, die bereits in der Datenbank gespeichert ist. |
| /areas | Gibt die Sicherheitsbereiche an, die auf das System angewendet werden sollen. Wenn dieser Parameter nicht angegeben wird, werden alle in der Datenbank definierten Sicherheitseinstellungen auf das System angewendet. Zum Konfigurieren mehrerer Bereiche trennen Sie jeden Bereich durch ein Leerzeichen. Die folgenden Sicherheitsbereiche werden unterstützt:<ul><li>**SecurityPolicy:** Lokale Richtlinie und Domänen Richtlinie für das System, einschließlich Konto Richtlinien, Überwachungs Richtlinien, Sicherheitsoptionen usw.</li><li>  **GROUP_MGMT:** Eingeschränkte Gruppeneinstellungen für alle Gruppen, die in der Sicherheits Vorlage angegeben sind.</li><li>**USER_RIGHTS:** Benutzer Anmelde Rechte und erteilen von Berechtigungen.</li><li>**Regkeys:** Sicherheit für lokale Registrierungsschlüssel.</li><li>**Dateispeicher:** Sicherheit im lokalen Dateispeicher.</li><li>**Dienste:** Sicherheit für alle definierten Dienste.</li></ul> |
| /Log | Gibt den Pfad und den Dateinamen der Protokolldatei an, die im Prozess verwendet werden soll. Wenn Sie keinen Speicherort für die Datei angeben, wird die Standardprotokoll Datei `<systemroot>\Documents and Settings\<UserAccount>\My Documents\Security\Logs\<databasename>.log` verwendet. |
| /quiet | Unterdrückt die Bildschirm-und Protokoll Ausgabe. Sie können weiterhin Analyseergebnisse anzeigen, indem Sie das Snap-in "Sicherheitskonfiguration und-Analyse" in der Microsoft Management Console (MMC) verwenden. |

## <a name="examples"></a>Beispiele

Wenn Sie die Sicherheitsdatenbank und die Domänen Sicherheitsrichtlinien in eine INF-Datei exportieren und diese Datei dann in eine andere Datenbank importieren möchten, um die Sicherheitsrichtlinien Einstellungen auf einem anderen Computer zu replizieren, geben Sie Folgendes ein:

```
secedit /export /db C:\Security\FY11\SecDbContoso.sdb /mergedpolicy /cfg SecContoso.inf /log C:\Security\FY11\SecAnalysisContosoFY11.log /quiet
```

Um die Beispieldatei in eine andere Datenbank auf einem anderen Computer zu importieren, geben Sie Folgendes ein:

```
secedit /import /db C:\Security\FY12\SecDbContoso.sdb /cfg SecContoso.inf /log C:\Security\FY11\SecAnalysisContosoFY12.log /quiet
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [secedit/analyze](secedit-analyze.md)

- [secedit/configure](secedit-configure.md)

- [secedit/generaterollback](secedit-generaterollback.md)

- [secedit/Import](secedit-import.md)

- [secedit/Validate](secedit-validate.md)