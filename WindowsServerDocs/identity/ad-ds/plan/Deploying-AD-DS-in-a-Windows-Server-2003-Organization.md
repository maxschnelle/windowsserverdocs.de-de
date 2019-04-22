---
ms.assetid: e6b72a80-e8b7-4305-be0c-0a290f468d36
title: Bereitstellen von AD DS in einer Windows Server 2003-Organisation
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 033973ad7a726054f6c47c7154fa54a3767beab4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59816361"
---
# <a name="deploying-ad-ds-in-a-windows-server-2003-organization"></a>Bereitstellen von AD DS in einer Windows Server 2003-Organisation

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Wenn Ihre Organisation derzeit Windows Server 2003 Active Directory ausgeführt wird, können Sie Windows Server 2008 Active Directory Domain Services (AD DS) bereitstellen, indem Sie entweder eine in-Place-Aktualisierung einiger oder aller Ihrer Domänencontroller-Betriebssysteme ausführen  WindowsServer 2008 oder durch die Einführung von Domänencontrollern unter WindowsServer 2008 in Ihrer Umgebung.  
  
Bevor Sie einen Domänencontroller unter Windows Server 2008 zu einer existierenden Windows Server 2003 Active Directory-Domäne hinzufügen können, müssen Sie ausführen **Adprep**, ein Befehlszeilentool. Adprep das AD DS-Schema erweitert, Aktualisieren von standardsicherheitsbeschreibungen ausgewählter Objekte und das Hinzufügen neuer Verzeichnisobjekte von einigen Anwendungen. Adprep-Befehls ist auf dem Installationsdatenträger von Windows Server 2008 (\sources\adprep\adprep.exe) verfügbar. Weitere Informationen finden Sie unter Adprep ([https://go.microsoft.com/fwlink/?LinkId=99215](https://go.microsoft.com/fwlink/?LinkId=99215)).  
  
Die folgende Abbildung zeigt die Schritte zum Bereitstellen von Windows Server 2008 AD DS in einer Netzwerkumgebung, auf denen derzeit Windows Server 2003 Active Directory ausgeführt wird.  
  
![Bereitstellen Sie in einem Windows 2003-Organisation](media/Deploying-AD-DS-in-a-Windows-Server-2003-Organization/900c4eee-1119-4a9a-9310-755597428b71.gif)  
  
> [!NOTE]  
> Wenn Sie die Funktionsebene der Domäne oder Gesamtstruktur auf Windows Server 2008 festgelegt möchten, müssen alle Domänencontroller in Ihrer Umgebung mit das Betriebssystem Windows Server 2008 ausführen.  
  
Konsolidierung von Ressourcen und Kontodomänen, die als Teil der Windows Server 2008 AD DS-Bereitstellung zwischen Gesamtstrukturen oder innerhalb der Gesamtstruktur Domänen Umstrukturieren von möglicherweise direkt aus einer Windows Server 2003-Umgebung aktualisiert werden. AD DS-Domänen zwischen Gesamtstrukturen umstrukturieren, können Sie reduzieren, die Komplexität für die Darstellung Ihrer Organisation in AD DS, und hilft, die damit verbundenen administrative Kosten zu reduzieren. AD DS-Domänen innerhalb einer Gesamtstruktur umstrukturieren, hilft Ihnen, verringern den Verwaltungsaufwand für Ihre Organisation, indem Sie Replikations-Datenverkehr verringert werden, verringert die Menge von Benutzer- und gruppenverwaltung, die erforderlich ist und vereinfacht die Verwaltung der Gruppe "" Die Richtlinie. Weitere Informationen finden Sie im ADMT v3. 1-Handbuch für die Migration ([https://go.microsoft.com/fwlink/?LinkId=93678](https://go.microsoft.com/fwlink/?LinkId=93678)).  
  
Eine detaillierte Liste der Aufgaben, die Sie verwenden können, um zu planen und Bereitstellen von AD DS in einer Organisation, auf denen Windows Server 2003 Active Directory ausgeführt wird, finden Sie unter [Prüfliste: Bereitstellen von AD DS in einer Windows Server 2003-Organisation](https://technet.microsoft.com/library/cc771407.aspx).  
  


