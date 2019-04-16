---
title: "Delegieren von Verwaltungsberechtigungen für DFS-Namespaces"
description: "In diesem Artikel wird beschrieben, wie Sie Verwaltungsberechtigungen für DFS-Namespaces delegieren und welche Gruppen standardmäßig Namespaceaufgaben ausführen können"
ms.date: 6/5/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: e584b49639a83e4ab1da142a999741ae4ac7ff84
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2017
---
# <a name="delegate-management-permissions-for-dfs-namespaces"></a>Delegieren von Verwaltungsberechtigungen für DFS-Namespaces

> Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server2012 R2, Windows Server 2012, Windows Server2008 R2, Windows Server 2008

Die folgende Tabelle beschreibt die Gruppen, die grundlegende Namespaceaufgaben standardmäßig ausführen können, und die Methode für das Delegieren der Fähigkeit zum Ausführen dieser Aufgaben:

|Aufgabe | Gruppen, die diese Aufgabe standardmäßig ausführen können | Delegierungsmethoden |
|---|---|---|
|Erstellen eines domänenbasierten Namespaces|Domänen-Admins werden in der Domäne gruppiert, in der der Namespace konfiguriert ist|Klicken Sie mit der rechten Maustaste in der Konsolenstruktur unter dem Knoten **Namespaces** auf **Delegieren von Verwaltungsberechtigungen**. Oder verwenden Sie [Set-DfsnRoot GrantAdminAccounts](https://technet.microsoft.com/itpro/powershell/windows/dfsn/set-dfsnroot) und [Set-DfsnRoot RevokeAdminAccounts](https://technet.microsoft.com/itpro/powershell/windows/dfsn/set-dfsnroot). Windows PowerShell Cmdlets (wurden in Windows Server 2012 eingeführt). Außerdem müssen Sie der lokalen Gruppe Administratoren auf dem Namespaceserver den Benutzer hinzufügen.|
|Fügen Sie einen Namespaceserver zu einem domänenbasierten Namespace hinzu|Domänen-Admins werden in der Domäne gruppiert, in der der Namespace konfiguriert ist| Klicken Sie mit der rechten Maustaste in der Konsolenstruktur auf den domänenbasierten Namespaces und dann auf **Delegieren von Verwaltungsberechtigungen**. Oder verwenden Sie [Set-DfsnRoot GrantAdminAccounts](https://technet.microsoft.com/itpro/powershell/windows/dfsn/set-dfsnroot) und [Set-DfsnRoot RevokeAdminAccounts](https://technet.microsoft.com/itpro/powershell/windows/dfsn/set-dfsnroot). Windows PowerShell Cmdlets (wurden in Windows Server 2012 eingeführt). Außerdem müssen Sie der lokalen Gruppe Administratoren auf dem hinzuzufügenden Namespaceserver den Benutzer hinzufügen.|
|Verwalten eines domänenbasierten Namespaces|Lokale Administratorgruppe auf jedem Namespaceserver| Klicken Sie mit der rechten Maustaste in der Konsolenstruktur auf den domänenbasierten Namespaces und dann auf **Delegieren von Verwaltungsberechtigungen**. |
|Erstellen eines eigenständigen Namespace|Lokale Administratorgruppe auf dem Namespaceserver| Fügen Sie der lokalen Gruppe Administratoren auf dem Namespaceserver den Benutzer hinzu. |
|Verwalten eines eigenständigen Namespace*|Lokale Administratorgruppe auf dem Namespaceserver| Klicken Sie mit der rechten Maustaste in der Konsolenstruktur auf den eigenständigen Namespace und dann auf **Delegieren von Verwaltungsberechtigungen**. Oder verwenden Sie [Set-DfsnRoot GrantAdminAccounts](https://technet.microsoft.com/itpro/powershell/windows/dfsn/set-dfsnroot) und [Set-DfsnRoot RevokeAdminAccounts](https://technet.microsoft.com/itpro/powershell/windows/dfsn/set-dfsnroot). Windows PowerShell Cmdlets (wurden in Windows Server 2012 eingeführt).|
|Erstellen einer Replikationsgruppe oder Aktivieren der DFS-Replikation für einen Ordner|Domänen-Admins werden in der Domäne gruppiert, in der der Namespace konfiguriert ist| Klicken Sie mit der rechten Maustaste in der Konsolenstruktur unter dem Knoten Replikation auf **Delegieren von Verwaltungsberechtigungen**. |

<br />

\*Das Delegieren von Berechtigungen zum Verwalten eines eigenständigen Namespace erteilt dem Benutzer nicht die Möglichkeit zum Anzeigen und Verwalten der Sicherheit mithilfe der Registerkarte **Delegierung**, es sei denn, der Benutzer ist Mitglied der lokalen Administratorgruppe auf dem Namespaceserver. Dieses Problem tritt auf, da der DFS-Verwaltungs-Snap-In die freigegebenen Zugriffssteuerungslisten (Discretionary Access Control Lists, DACLs) für den eigenständigen Namespace in der Registrierung nicht abrufen kann. Zum Aktivieren des Snap-In für die Delegierungsinformationen, müssen Sie die Schritteim Microsoft<sup>®</sup> Knowledge Base-Artikel: [KB314837: Steuerung des Remote-Zugriffs auf die Registrierung](http://go.microsoft.com/fwlink?linkid=46803) ausführen