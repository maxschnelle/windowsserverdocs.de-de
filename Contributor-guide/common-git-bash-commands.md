---
title: Allgemeine git bash-Befehle für die Verwendung mit GitHub
description: Eine Liste mit einigen der am häufigsten verwendeten Befehlen in git bash bei der Arbeit mit GitHub.
author: eross-msft
ms.author: lizross
ms.date: 05/06/2019
ms.openlocfilehash: 4ce5d4d8ce382e9ba421c20595715ec473cca241
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70864999"
---
# <a name="common-git-bash-commands"></a>Allgemeine git bash-Befehle

Dies sind einige der am häufigsten verwendeten Befehle in git bash, die darauf basieren, wann Sie Sie bei der Erstellung und Bearbeitung von Inhalten verwenden werden.

## <a name="master-branch-related"></a>Master Verzweigungs bezogen

Sie müssen für jeden neuen Branch immer Master als Basis verwenden.

| Befehl | Beschreibung |
|---------|-------------|
| `git checkout master` | Zum Master aus einer beliebigen anderen Verzweigung wechseln |
| `git pull upstream master` | Aktualisieren Ihrer lokalen Master Kopie aus dem produktionsrepository |

## <a name="branch-related"></a>Verzweigungs bezogen

| Befehl | Beschreibung |
|---------|-------------|
| `git branch` | Vorhandene Verzweigungen anzeigen |
| `git checkout -B <name-of-branch>` | Neuen Branch erstellen |
| `git checkout <name-of-branch>` | Wechseln zu einer anderen Verzweigung |
| `git status` | Überprüfen Sie, was in ihrer Verzweigung passiert. |
| `git branch -D <name-of-branch>` | Löschen Sie eine vorhandene Verzweigung (stellen Sie sicher, dass Sie nicht darin vorhanden sind). |

## <a name="check-in-related-done-as-a-group-in-order"></a>Check-in-Related (als Gruppe, in der Reihenfolge ausgeführt)

| Befehl | Beschreibung |
|---------|-------------|
| `git add --all` | Nachdem Sie Ihre Arbeit gespeichert haben, fügen Sie Sie einer Verzweigung hinzu. |
| `git commit -m “public comment, including quotes”` | Commit für Ihre Änderungen in Ihrem Branch durchsetzen |
| `git pull upstream master` | Aktualisieren Ihrer lokalen Master Kopie aus dem produktionsrepository |
| `git push origin <name-of-branch>` | Push an die Remote Version Ihres lokalen Branch |