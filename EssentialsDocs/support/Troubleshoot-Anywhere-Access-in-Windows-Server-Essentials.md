---
title: Problembehandlung von "Zugriff überall" in Windows Server Essentials
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.topic: article
ms.assetid: 68f2b05c-09eb-4cba-8db4-a91353b513c6
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 241e2225c9e1dfdea3189e938a04c4af4c033c3f
ms.sourcegitcommit: 04637054de2bfbac66b9c78bad7bf3e7bae5ffb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87838319"
---
# <a name="troubleshoot-anywhere-access-in-windows-server-essentials"></a>Problembehandlung von "Zugriff überall" in Windows Server Essentials

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Dieses Thema enthält allgemeine Anweisungen für die Verwendung des Assistenten zum Reparieren von "Zugriff überall" in Windows Server Essentials, um Probleme zu beheben, die verhindern, dass Netzwerk Benutzer auf Server Ressourcen zugreifen. "Zugriff überall"-Funktionen: Remote Webzugriff, virtuelles privates Netzwerk (VPN) und DirectAccess: ermöglichen Netzwerk Benutzern den Zugriff auf Server Ressourcen von einem beliebigen Standort mit einer Internet Verbindung jederzeit von einem beliebigen Gerät aus.

Der Assistent zum Reparieren von "Zugriff überall" versucht, Probleme mit Router, Domänenname oder Firewall zu identifizieren und zu beheben, die Benutzer im Netzwerk daran hindern, per Remotezugriff auf Serverressourcen zuzugreifen.

> [!NOTE]
> Die aktuellsten Informationen zur Problembehandlung aus der Windows Server Essentials-Community finden Sie im [Windows Server Essentials-Forum](/answers/topics/windows-server-essentials.html). Das Windows Server Essentials-Forum eignet sich optimal, um nach Hilfe zu suchen oder um Fragen zu stellen.

## <a name="to-repair-anywhere-access"></a>So reparieren Sie "Zugriff überall"

1. Melden Sie sich an den Server an und öffnen Sie das Dashboard.

2. Klicken Sie auf **Einstellungen** und dann auf die Registerkarte **Zugriff überall**.

3. Klicken Sie auf **Reparatur**. Die Assistent zur Reparatur von "Zugriff überall" wird gestartet.

4. Klicken Sie auf **Weiter**. Der Assistent analysiert "Zugriff überall", identifiziert das Problem und versucht anschließend, das Problem zu beheben.

5. Wenn nach Beenden des Assistenten eine Warnung angezeigt wird, können Sie auf **Wiederholung** klicken, um zu versuchen, das Problem erneut zu reparieren. Wenn Sie weiterhin eine Warnung erhalten, überprüfen Sie die Warnung auf weitere Informationen zu dem Problem und auf Schritte zur Problembehandlung.

## <a name="to-get-more-information-about-an-alert"></a>So rufen Sie weitere Informationen zu einer Warnung ab

1. Klicken Sie in der oberen rechten Ecke des Dashboards auf ein Fehler- oder Warnungssymbol, um die Meldungsanzeige zu öffnen.

2. Klicken Sie in der Meldungsanzeige auf den Fehler oder die Warnung, um zusätzliche Informationen anzuzeigen.

## <a name="additional-troubleshooting-for-anywhere-access"></a>Zusätzliche Fehlerbehebung für "Zugriff überall"
 Wenn der Assistent zum Reparieren von "Zugriff überall" keine Reparatur ausführen kann, überprüfen Sie die folgenden Ressourcen für die Problembehandlung bei Problemen im Zusammenhang mit Remote Web Access, VPN und DirectAccess:

- [Behandeln von Problemen mit der Remotewebzugriff-Verbindung](Troubleshoot-Remote-Web-Access-connectivity-in-Windows-Server-Essentials.md)

- [Behandeln von Problemen mit der Firewall](Troubleshoot-your-firewall-in-Windows-Server-Essentials.md)

- Im [Windows Server Essentials-Forum](/answers/topics/windows-server-essentials.html) finden Sie die neuesten Probleme, die von der Windows Server Essentials-Community gemeldet wurden.