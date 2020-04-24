---
title: Erstellen einer RDS-Sammlung
description: Erfahre, wie du RDSH- und RemoteApp-Programme deiner RDS-Bereitstellung hinzufügst.
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 10/22/2019
ms.topic: article
ms.assetid: ae9767e3-864a-4eb2-96c0-626759ce6d60
author: lizap
manager: dongill
ms.openlocfilehash: 6a842c7984dc63fe40c05300f6cfbb6718846525
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2020
ms.locfileid: "80852953"
---
# <a name="create-a-remote-desktop-services-collection-for-desktops-and-apps-to-run"></a>Erstellen einer RDS-Sammlung zum Ausführen von Desktops und Apps

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016

Führe die folgenden Schritte aus, um eine RDS-Sitzungssammlung zu erstellen. Eine Sitzungssammlung enthält die Apps und Desktops, die du Benutzern zur Verfügung stellen möchtest. Nachdem du die Sammlung erstellt hast, veröffentliche sie, damit Benutzer darauf zugreifen können.

Bevor du eine Sammlung erstellst, musst du entscheiden, welche Art von Sammlung du benötigst: Pooldesktopsitzungen oder persönliche Desktopsitzungen. 

- **Verwenden von Pooldesktopsitzungen für sitzungsbasierte Virtualisierung**: Nutze die Rechenleistung von Windows Server, um eine kostengünstige Multisessionumgebung für die täglichen Workloads deiner Benutzer bereitzustellen.
- **Verwenden von persönlichen Desktopsitzungen, um eine virtuelle Desktopinfrastruktur (VDI) zu erstellen**: Nutze den Windows-Client, um die hohe Leistung, App-Kompatibilität und Vertrautheit zu bieten, die deine Benutzer von ihrer Windows-Desktopdarstellung gewohnt sind.
 
Bei einer Poolsitzung greifen mehrere Benutzer auf einen gemeinsamen Ressourcenpool zu, während bei einer persönlichen Desktopsitzung den Benutzern ein eigener Desktop aus dem Pool zugewiesen wird. Die Poolsitzung bietet niedrigere Gesamtkosten, während persönliche Sitzungen den Benutzern ermöglichen, ihre Desktopdarstellung anzupassen.

Wenn du grafikintensive gehostete Anwendung freigeben möchtest, kannst du persönliche Sitzungsdesktops mit der neuen Discrete Device Assignment-Funktion (DDA) kombinieren, um Unterstützung für solche gehosteten Anwendungen bereitzustellen. Weitere Informationen findest du unter [Welche Grafikvirtualisierungstechnologie ist für Sie geeignet?](rds-graphics-virtualization.md).


Unabhängig von der Art der Sammlung, die du wählst, füllst du diese Sammlungen mit RemoteApps – Programmen und Ressourcen, auf die Benutzer von jedem unterstützten Gerät aus zugreifen und mit denen sie arbeiten können, als ob das Programm lokal ausgeführt würde.

## <a name="create-a-pooled-desktop-session-collection"></a>Erstellen einer Pooldesktopsitzungs-Sammlung

1.  Klicke im Server-Manager auf **Remotedesktopdienste > Sammlungen > Tasks > Sitzungssammlungen erstellen**.  
2.  Gib einen Namen für die Sammlung ein, z.B. **ContosoAps**.  
3.  Wähle den RD-Sitzungshost-Server aus, den du erstellt hast (z.B. Contoso-Shr1).  
4.  Übernimm die Vorgabe **Benutzergruppen**.  
5.  Gib den Speicherort der Dateifreigabe ein, die du für die Benutzerprofil-Datenträger für diese Sammlung erstellt hast (z.B. **\Contoso-Cb1\UserDisksr**).   
6.  Klicken Sie auf **Erstellen**. Klicke nach Erstellen der Sammlung auf **Schließen**.  


## <a name="create-a-personal-desktop-session-collection"></a>Erstellen einer Sammlung einer persönlichen Desktopsitzung

Verwende das Cmdlet „New-RDSessionCollection“, um eine Sammlung persönlicher Sitzungsdesktops zu erstellen. Die folgenden drei Parameter stellen die Konfigurationsinformationen bereit, die für persönliche Sitzungsdesktops benötigt werden:

- **-PersonalUnmanaged**: Gibt den Typ der Sitzungssammlung an, mit dem du Benutzer einem persönlichen Sitzungshostserver zuweisen kannst. Wenn du diesen Parameter nicht angibst, wird die Sammlung als herkömmliche Remotedesktop-Sitzungshostsammlung erstellt, bei der Benutzer beim Anmelden dem nächsten verfügbaren Sitzungshost zugewiesen werden.
- **-GrantAdministrativePrivilege**: Wenn du **-PersonalUnmanaged** verwendest, gibt dieser Parameter an, dass der Benutzer, der dem Sitzungshost zugewiesen wurde, Administratorrechte erhalten soll. Wenn du diesen Parameter nicht verwendest, werden den Benutzern nur Standardbenutzerrechte erteilt.
- **-AutoAssignUser**: Wenn du **-PersonalUnmanaged** verwendest, gibt dieser Parameter an, dass neue Benutzer, die eine Verbindung über den Remotedesktop-Verbindungsbroker herstellen, automatisch einem noch nicht zugewiesenen Sitzungshost zugewiesen werden. Wenn in der Sammlung keine nicht zugewiesenen Sitzungshosts vorhanden sind, wird dem Benutzer eine Fehlermeldung angezeigt. Wenn du diesen Parameter nicht verwendest, musst du [Benutzer manuell einem Sitzungshost zuweisen](rds-manage-personal-collection.md#manually-assign-a-user-to-a-personal-session-host), bevor die Benutzer sich anmelden.

Du kannst PowerShell-Cmdlets verwenden, um deine Sammlungen persönlicher Desktopsitzungen zu verwalten. Weitere Informationen findest du unter [Verwalten Ihrer Sammlung mit persönlichen Desktopsitzungen](rds-manage-personal-collection.md).

## <a name="publish-remoteapp-programs"></a>Veröffentlichen von RemoteApp-Programmen
Führe die folgenden Schritte aus, um die Apps und Ressourcen in deiner Sammlung zu veröffentlichen:

1.  Wähle im Server-Manager die neue Sammlung aus (**ContosoApps**).  
2.  Klicke unter „RemoteApp-Programme“ auf **RemoteApp-Programme veröffentlichen**.  
3. Wähle die Programme aus, die du veröffentlichen möchtest, und klicke dann auf **Veröffentlichen**.  
