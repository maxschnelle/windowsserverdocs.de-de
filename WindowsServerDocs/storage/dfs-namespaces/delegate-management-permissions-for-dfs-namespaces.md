---
title: Delegieren von Verwaltungsberechtigungen für DFS-Namespaces
description: In diesem Artikel wird beschrieben, wie Verwaltungs Berechtigungen für DFS-Namespaces delegiert werden und welche Gruppen Namespace Aufgaben standardmäßig ausführen können.
ms.date: 6/5/2017
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: a986c47416de79c9ff24d9104a2fa599dd5f8640
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87954787"
---
# <a name="delegate-management-permissions-for-dfs-namespaces"></a>Delegieren von Verwaltungs Berechtigungen für DFS-Namespaces

> Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

In der folgenden Tabelle werden die Gruppen beschrieben, die standardmäßig grundlegende Namespace Aufgaben ausführen können, und die-Methode zum Delegieren der Fähigkeit zum Ausführen dieser Aufgaben:

|Aufgabe | Gruppen, die diese Aufgabe standardmäßig ausführen können | Delegierungs Methode |
|---|---|---|
|Erstellen eines domänenbasierten Namespace|Gruppe "Domänen-Admins" in der Domäne, in der der Namespace konfiguriert ist|Klicken Sie in der Konsolen Struktur mit der rechten Maustaste auf den Knoten **Namespaces** , und klicken Sie dann auf **Verwaltungs Berechtigungen delegieren**. Oder verwenden Sie " [Set-dfsnroot grantadminaccounts](/powershell/module/dfsn/set-dfsnroot?view=win10-ps) " und " [Set-dfsnroot revokeadminaccounts](/powershell/module/dfsn/set-dfsnroot?view=win10-ps)". Windows PowerShell-Cmdlets (eingeführt in Windows Server 2012). Außerdem müssen Sie der lokalen Gruppe Administratoren auf dem Namespaceserver den Benutzer hinzufügen.|
|Hinzufügen eines Namespace Servers zu einem domänenbasierten Namespace|Gruppe "Domänen-Admins" in der Domäne, in der der Namespace konfiguriert ist| Klicken Sie in der Konsolen Struktur mit der rechten Maustaste auf den domänenbasierten Namespace, und klicken Sie dann auf **Verwaltungs Berechtigungen delegieren**. Oder verwenden Sie " [Set-dfsnroot grantadminaccounts](/powershell/module/dfsn/set-dfsnroot?view=win10-ps) " und " [Set-dfsnroot revokeadminaccounts](/powershell/module/dfsn/set-dfsnroot?view=win10-ps)". Windows PowerShell-Cmdlets (eingeführt in Windows Server 2012). Außerdem müssen Sie den Benutzer der lokalen Gruppe Administratoren auf dem hinzu zufügenden Namespace Server hinzufügen.|
|Verwalten eines domänenbasierten Namespace|Lokale Gruppe "Administratoren" auf jedem Namespace Server| Klicken Sie in der Konsolen Struktur mit der rechten Maustaste auf den domänenbasierten Namespace, und klicken Sie dann auf **Verwaltungs Berechtigungen delegieren**. |
|Erstellen eines eigenständigen Namespace|Lokale Gruppe "Administratoren" auf dem Namespace Server| Fügen Sie den Benutzer der lokalen Administrator Gruppe auf dem Namespace Server hinzu. |
|Verwalten eines eigenständigen Namespace *|Lokale Gruppe "Administratoren" auf dem Namespace Server| Klicken Sie in der Konsolen Struktur mit der rechten Maustaste auf den eigenständigen Namespace, und klicken Sie dann auf **Verwaltungs Berechtigungen delegieren**. Oder verwenden Sie " [Set-dfsnroot grantadminaccounts](/powershell/module/dfsn/set-dfsnroot?view=win10-ps) " und " [Set-dfsnroot revokeadminaccounts](/powershell/module/dfsn/set-dfsnroot?view=win10-ps)". Windows PowerShell-Cmdlets (eingeführt in Windows Server 2012).|
|Erstellen einer Replikations Gruppe oder Aktivieren von DFS-Replikation in einem Ordner|Gruppe "Domänen-Admins" in der Domäne, in der der Namespace konfiguriert ist| Klicken Sie in der Konsolen Struktur mit der rechten Maustaste auf den Knoten Replikation, und klicken Sie dann auf **Verwaltungs Berechtigungen delegieren**. |

<br />

\*Das Delegieren von Verwaltungs Berechtigungen zum Verwalten eines eigenständigen Namespace gewährt dem Benutzer nicht die Möglichkeit, die Sicherheit auf der Registerkarte **Delegierung** anzuzeigen und zu verwalten, es sei denn, der Benutzer ist ein Mitglied der lokalen Administratoren Gruppe auf dem Namespace Server. Dieses Problem tritt auf, weil das DFS-Verwaltungs-Snap-in keine freigegebenen Zugriffs Steuerungs Listen (DACLs) für den eigenständigen Namespace aus der Registrierung abrufen kann. Um das Snap-in zum Anzeigen von Delegierungs Informationen zu aktivieren, müssen Sie die Schritte im Microsoft<sup>®</sup> Knowledge Base-Artikel ausführen: [KB314837: Verwalten des Remote Zugriffs auf die Registrierung](https://go.microsoft.com/fwlink?linkid=46803) .
