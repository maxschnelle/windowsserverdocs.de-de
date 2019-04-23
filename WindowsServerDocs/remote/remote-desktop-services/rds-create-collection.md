---
title: Erstellen Sie eine Sammlung von Remote Desktop Services
description: Erfahren Sie, wie hinzugefügt und RDSH und RemoteApp-Programme für Ihre RDS-Bereitstellung.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 11/08/2016
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ae9767e3-864a-4eb2-96c0-626759ce6d60
author: lizap
manager: dongill
ms.openlocfilehash: 52806e28c4ef87453995728623efe2954a76dfd9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59839241"
---
# <a name="create-a-remote-desktop-services-collection-for-desktops-and-apps-to-run"></a>Erstellen einer Remote Desktop Services-Sammlung für Desktops und apps ausführen

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Verwenden Sie die folgenden Schritte aus, um eine Auflistung der Remotedesktopdienste-Sitzung zu erstellen. Eine sitzungssammlung enthält, die apps und Desktops, die Sie für Benutzer verfügbar machen möchten. Nachdem Sie die Sammlung erstellt haben, veröffentlichen Sie, damit Benutzer darauf zugreifen können.

Bevor Sie eine Sammlung erstellen, müssen Sie entscheiden, welche Art von Sammlung, die Sie benötigen: in einem Pool zusammengefasste Remotedesktopsitzungen oder persönlichen Remotedesktopsitzungen. 

- **Verwenden Sie in einem Pool zusammengefasste Remotedesktopsitzungen für sitzungsbasierte Virtualisierung**: Nutzen Sie die rechenleistung von Windows Server, bieten eine kostengünstige Multisession-Umgebung, um alltägliche Workloads für Ihrer Benutzer fördern
- **Verwenden Sie zum Erstellen einer virtuellen Desktopinfrastruktur (VDI) persönliche Remotedesktopsitzungen für**: Nutzen Sie die Windows-Client, um die hohe Leistung, Anwendungskompatibilität und vertraut sind, die Ihre Benutzer von uns erwarten von ihren Windows-desktop-Erlebnis zu bieten.
 
Mit einer Sitzung in einem Pool zusammengefasste mehrere Benutzer Zugriff auf einen freigegebenen Pool von Ressourcen, während Sie sich mit einer persönlichen desktop-Sitzung sind Benutzer zugeordnet ihre eigenen Desktop von innerhalb des Pools. Die Sitzung in einem Pool zusammengefasste bietet geringere Gesamtkosten aus, während persönliche Sitzungen Benutzer zum Anpassen ihrer desktop-Erlebnis ermöglichen.

Wenn Sie auf Freigabe, die gehostete Anwendungen, die grafikintensive sind benötigen, können Sie persönliche sitzungsdesktops mit RemoteFX vGPU für Grafiken beschleunigungen konfiguriert kombinieren. Alternativ können Sie persönliche sitzungsdesktops kombinieren, mit der neue diskrete Gerät Zuweisung (DDA)-Funktion, die auch für gehostete Anwendungen unterstützen, die beschleunigte Grafikfunktionen erfordern. Sehen Sie sich [welche Grafiken Virtualisierungstechnologie ist die richtige für Sie](rds-graphics-virtualization.md) für Weitere Informationen.


Unabhängig von der Art der Auflistung, die Sie auswählen, füllen Sie die Sammlungen mit RemoteApps - Programme und Ressourcen, die Benutzer können von einem beliebigen unterstützten Gerät Zugriff auf und Arbeiten mit, als ob die Anwendung lokal ausgeführt wurde.

## <a name="create-a-pooled-desktop-session-collection"></a>Erstellen Sie eine Remotedesktop-Sitzungshosts in einem Pool zusammengefasste Sammlung

1.  Klicken Sie im Server-Manager **Remote Desktop Services > Sammlungen > Vorgänge > Sitzungssammlungen erstellen**.  
2.  Geben Sie einen Namen für die Auflistung, z. B. **ContosoAps**.  
3.  Wählen Sie den Remotedesktop-Sitzungshost-Server (z. B. Contoso-Shr1) erstellten.  
4.  Übernehmen Sie den Standardnamen **Benutzergruppen**.  
5.  Geben Sie den Speicherort der Dateifreigabe, die Sie für die Benutzerprofil-Datenträger für diese Sammlung erstellt haben (z. B. **\Contoso-Cb1\UserDisksr**).   
6.  Klicken Sie auf **Erstellen**. Wenn die Auflistung erstellt wird, klicken Sie auf **schließen**.  


## <a name="create-a-personal-desktop-session-collection"></a>Erstellen Sie eine Sammlung von persönlichen Remotedesktop-Sitzungshosts

Verwenden Sie das Cmdlet "New-RDSessionCollection", um einen persönlichen desktop sitzungssammlung erstellen. Die folgenden drei Parameter geben die Konfigurationsinformationen für persönliche sitzungsdesktops benötigt:

- **-PersonalUnmanaged** -gibt der Typ der sitzungssammlung, der Ihnen ermöglicht eine persönliche Sitzungshostserver Benutzer zuweisen. Wenn Sie diesen Parameter nicht angeben, wird als eine herkömmliche RD-Sitzungshost-Auflistung, die Sammlung erstellt, in denen Benutzer den nächsten verfügbaren Sitzungshost zugewiesen sind, bei der Anmeldung.
- **-GrantAdministrativePrivilege** : bei Verwendung von **- PersonalUnmanaged**, gibt an, dass der Benutzer, die dem Sitzungshost zugewiesen Administratorrechte zugewiesen werden. Wenn Sie diesen Parameter nicht verwenden, erhalten Benutzer nur Berechtigungen für Standardbenutzer.
- **-AutoAssignUser** : bei Verwendung von **- PersonalUnmanaged**, gibt an, dass neue Benutzer, die eine Verbindung über den Remotedesktop-Verbindungsbroker automatisch auf einem Sitzungshost nicht zugewiesene zugewiesen werden. Wenn keine nicht zugewiesenen Sitzungshosts in der Auflistung vorhanden sind, wird der Benutzer eine Fehlermeldung angezeigt. Wenn Sie diesen Parameter nicht verwenden, müssen Sie [manuell zuweisen von Benutzern zu einem Host für Remotedesktopsitzungen](rds-manage-personal-collection.md#manually-assign-a-user-to-a-personal-session-host) , bevor sie sich anmelden.

Sie können PowerShell-Cmdlets verwenden, um Ihre persönliche Remotedesktop-Sitzungshost-Sammlungen zu verwalten. Finden Sie unter [verwalten Sie Ihre persönliche Remotedesktop-Sitzungshost-Sammlungen](rds-manage-personal-collection.md) für Weitere Informationen.

## <a name="publish-remoteapp-programs"></a>RemoteApp-Programme veröffentlichen
Verwenden Sie die folgenden Schritte aus, um die apps und Ressourcen in Ihrer Sammlung zu veröffentlichen:

1.  Wählen Sie die neue Sammlung im Server-Manager (**ContosoApps**).  
2.  Klicken Sie unter der RemoteApp-Programmen **Veröffentlichen des RemoteApp-Programme**.  
3. Wählen Sie die Programme, die Sie veröffentlichen möchten, und klicken Sie dann auf **veröffentlichen**.  
