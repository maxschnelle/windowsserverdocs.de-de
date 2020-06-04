---
title: msdt
description: Referenz Thema für den MSDT-Befehl, der ein Problem Behandlungspaket in der Befehlszeile oder als Teil eines automatisierten Skripts aufruft und zusätzliche Optionen ohne Benutzereingaben ermöglicht.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ead1b672-a120-4e16-94aa-a8e13602c1d0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 47eaf859c86a939777ce8878937d36f2c581ab31
ms.sourcegitcommit: 5e313a004663adb54c90962cfdad9ae889246151
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/04/2020
ms.locfileid: "84354371"
---
# <a name="msdt"></a>msdt

Ruft ein Problem Behandlungspaket in der Befehlszeile oder als Teil eines automatisierten Skripts auf und ermöglicht zusätzliche Optionen ohne Benutzereingaben.

## <a name="syntax"></a>Syntax

```
msdt </id <name> | /path <name> | /cab < name>> <</parameter> [options] … <parameter> [options]>>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| /ID`<packagename>` | Gibt an, welches Diagnosepaket ausgeführt werden soll. Eine Liste der verfügbaren Pakete finden Sie unter [Verfügbare Problem Behandlungspakete](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/ee424379(v=ws.11)#available-troubleshooting-packs). |
| /Path`<directory|.diagpkg file|.diagcfg file>` | Gibt den vollständigen Pfad zu einem Diagnosepaket an. Wenn Sie ein Verzeichnis angeben, muss das Verzeichnis ein Diagnosepaket enthalten. Der **/path** -Parameter kann nicht in Verbindung mit den Parametern * */ID * *, **/DCI**oder **/CAB** verwendet werden. |                                                                                   |
| /dci`<passkey>` | Füllt das Hauptschlüssel-Feld vorab auf. Dieser Parameter wird nur verwendet, wenn ein Support Anbieter einen Passkey bereitgestellt hat. |
| /dt`<directory>` | Zeigt den Verlauf der Problembehandlung im angegebenen Verzeichnis an. Diagnoseergebnisse werden in den Verzeichnissen " **%LocalAppData%\diagnostics** " oder " **%LocalAppData%\elevateddiagnostics** " des Benutzers gespeichert. |
| /af`<answerfile>` | Gibt eine Antwortdatei im XML-Format an, die Antworten auf eine oder mehrere Diagnose Interaktionen enthält. |
| /modal`<ownerHWND>` | Vereinfacht das Problembehandlungs Paket in einem vom übergeordneten Konsolenfenster handle (HWND) festgelegten Fenster im Dezimal Format. Dieser Parameter wird in der Regel von Anwendungen verwendet, die ein Problem Behandlungspaket starten. Weitere Informationen zum Abrufen von Konsolenfenster Handles finden [Sie unter Abrufen eines Konsolenfenster Handles (HWND)](https://support.microsoft.com/help/124103/how-to-obtain-a-console-window-handle-hwnd). |
| /moreoptions`<true|false>` | Aktiviert (true) oder unterdrückt (false) der abschließende Fehler Behebungs Bildschirm, der fragt, ob der Benutzer zusätzliche Optionen untersuchen möchte. Dieser Parameter wird normalerweise verwendet, wenn das Problem Behandlungspaket von einer Problembehandlung gestartet wird, die nicht Teil des Betriebssystems ist. |
| /param Returns`<parameters>` | Gibt einen Satz von Interaktions Antworten in der Befehlszeile an, ähnlich wie eine Antwortdatei. Dieser Parameter wird in der Regel nicht im Kontext von Problem Behandlungs Paketen verwendet, die mit TSP-Designer erstellt wurden. Weitere Informationen zum Entwickeln von benutzerdefinierten Parametern finden Sie unter [Windows-Problem Behandlungs Plattform](https://docs.microsoft.com/previous-versions/windows/desktop/wintt/windows-troubleshooting-toolkit-portal). |
| > Erweiterte | Erweitert den Link erweitert auf der Willkommensseite standardmäßig, wenn das Problem Behandlungspaket gestartet wird. |
| /custom | Fordert den Benutzer auf, jede mögliche Auflösung zu bestätigen, bevor diese angewendet wird. |

### <a name="return-codes"></a>Rückgabecodes

Die Problembehandlung von Paketen besteht aus einer Reihe von Hauptursachen, von denen jedes ein bestimmtes technisches Problem beschreibt. Nach Abschluss der Tasks "Problembehandlung" gibt jede Ursache den Status "Fixed", "Fixed", "found" (aber nicht fixiert) oder "nicht gefunden" zurück. Zusätzlich zu den auf der Benutzeroberfläche von Problembehandlung gemeldeten Ergebnissen gibt die Problembehandlungs-Engine einen Code in den Ergebnissen zurück, der in der Regel beschreibt, ob die Problembehandlung das ursprüngliche Problem behoben hat oder nicht. Folgende Codes sind möglich:

| Code | BESCHREIBUNG |
| ---- | ----------- |
| -1 | Unter **Brechung:** Die Problembehandlung wurde geschlossen, bevor die Aufgaben zur Problembehandlung abgeschlossen wurden. |
| 0 | **Korrigiert:** Die Problembehandlung hat mindestens eine Ursache identifiziert und korrigiert, und keine Hauptursachen sind in einem nicht festgelegten Zustand. |
| 1 | **Vorhanden, aber nicht korrigiert:** Die Problembehandlung hat eine oder mehrere Grundursachen identifiziert, die in einem nicht festgelegten Zustand bleiben. Dieser Code wird auch dann zurückgegeben, wenn eine andere Ursache korrigiert wurde. |
| 2 | **Nicht gefunden:** Die Problembehandlung hat keine Grundursachen identifiziert. |

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Verfügbare Problem Behandlungspakete](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/ee424379(v=ws.11)#available-troubleshooting-packs)

- [PowerShell-Referenz zu Problem Behandlungs Paketen](https://docs.microsoft.com/powershell/module/troubleshootingpack/?view=win10-ps)