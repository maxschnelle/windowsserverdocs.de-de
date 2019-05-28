---
title: Allgemeine Git Bash-Befehle für die Verwendung mit GitHub
description: Eine Liste einiger der am häufigsten verwendeten Befehle in Git Bash bei der Verwendung von GitHub.
author: eross-msft
ms.author: lizross
ms.date: 05/06/2019
ms.openlocfilehash: 210acaf2b7911892bcfd81b6bbe1975f141308a1
ms.sourcegitcommit: 7e54a1bcd31cd2c6b18fd1f21b03f5cfb6165bf3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/09/2019
ms.locfileid: "65461691"
---
# <a name="common-git-bash-commands"></a>Häufig verwendete Git Bash-Befehle

Dies sind einige der am häufigsten verwendeten Befehle in Git Bash, basierend auf, wenn Sie sie in der Erstellung von Inhalten verwenden und Bearbeiten von Prozess.

## <a name="master-branch-related"></a>Master-Branch-bezogene

Sie müssen immer Master als Grundlage für alle neuen Branch verwenden.

| Befehl | Beschreibung |
|---------|-------------|
| `git checkout master` | Wechseln Sie zum Master aus einem beliebigen anderen branch |
| `git pull upstream master` | Aktualisieren Sie Ihrer lokale Kopie des Masters aus dem Repository für die Produktion |

## <a name="branch-related"></a>Branch-bezogene

| Befehl | Beschreibung |
|---------|-------------|
| `git branch` | Finden Sie unter Ihrem vorhandenen branches |
| `git checkout -B <name-of-branch>` | Einen neuen Branch erstellen |
| `git checkout <name-of-branch>` | Ändern Sie in einem anderen branch |
| `git status` | Überprüfen Sie, was in Ihrem Branch geht |
| `git branch -D <name-of-branch>` | Löschen einer vorhandenen Verzweigung (sicherstellen, dass Sie nicht darin enthalten sind) |

## <a name="check-in-related-done-as-a-group-in-order"></a>Check-in-bezogenen (ausgeführt als eine Gruppe, in Reihenfolge)

| Befehl | Beschreibung |
|---------|-------------|
| `git add --all` | Nachdem Sie Ihre Arbeit speichern, fügen sie in einen Branch hinzu |
| `git commit -m “public comment, including quotes”` | Committen Sie Ihre Änderungen in Ihren branch |
| `git pull upstream master` | Aktualisieren Sie Ihrer lokale Kopie des Masters aus dem Repository für die Produktion |
| `git push origin <name-of-branch>` | Push an die remote-Version Ihres lokalen Branch |