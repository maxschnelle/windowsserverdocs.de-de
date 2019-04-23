---
ms.assetid: 7530cafe-98d7-46c9-95d9-e49d39caa021
title: Bereitstellen von AD DS in einer Windows 2000-Organisation
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 5015c0ca2c01fca966927af4207a7e3501d9cd39
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59854281"
---
# <a name="deploying-ad-ds-in-a-windows-2000-organization"></a>Bereitstellen von AD DS in einer Windows 2000-Organisation

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Wenn Ihre Organisation derzeit Windows 2000 Active Directory ausgeführt wird, können Sie Windows Server 2008 Active Directory Domain Services (AD DS) bereitstellen, indem Sie entweder eine in-Place-Aktualisierung einiger oder aller Ihrer Domänencontroller-Betriebssysteme Windows ausführen Server 2008 oder durch die Einführung von Domänencontrollern unter WindowsServer 2008 in Ihrer Umgebung.  
  
Bevor Sie einen Domänencontroller unter Windows Server 2008 mit einer vorhandenen Windows 2000 Active Directory-Domäne hinzufügen können, müssen Sie ausführen **Adprep**, ein Befehlszeilentool. Adprep das AD DS-Schema erweitert, Aktualisieren von standardsicherheitsbeschreibungen ausgewählter Objekte und das Hinzufügen neuer Verzeichnisobjekte von einigen Anwendungen. Adprep-Befehls ist auf dem Installationsdatenträger von Windows Server 2008 (\sources\adprep\adprep.exe) verfügbar. Weitere Informationen finden Sie unter Adprep ([https://go.microsoft.com/fwlink/?LinkId=99215](https://go.microsoft.com/fwlink/?LinkId=99215)).  
  
> [!NOTE]  
> Wenn Sie ein direktes Upgrade von einem vorhandenen Windows 2000 AD DS-Domänencontroller auf Windows Server 2008 ausführen möchten, müssen Sie zunächst ein upgrade den Server auf Windows Server 2003 und klicken Sie dann ein upgrade auf Windows Server 2008.  
  
Die folgende Abbildung zeigt die Schritte zum Bereitstellen von Windows Server 2008 AD DS in einer Netzwerkumgebung, auf denen derzeit Windows 2000 Active Directory ausgeführt wird.  
  
![Bereitstellen in einer Windows 2000-Organisation](media/Deploying-AD-DS-in-a-Windows-2000-Organization/ee51218a-a858-49d9-8b99-9986679191c1.gif)  
  
> [!NOTE]  
> Wenn Sie die Funktionsebene der Domäne oder Gesamtstruktur auf Windows Server 2008 festgelegt möchten, müssen alle Domänencontroller in Ihrer Umgebung mit das Betriebssystem Windows Server 2008 ausführen.  
  
Konsolidierung von Ressourcenmanagement und Kundenmanagement Domänen, die direkt aus einer Windows 2000-Umgebung als Teil Ihrer Windows Server 2008 AD DS aktualisiert werden erfordern Bereitstellung zwischen Gesamtstrukturen oder innerhalb einer Gesamtstruktur, Domänen umstrukturieren. AD DS-Domänen zwischen Gesamtstrukturen umstrukturieren, hilft Ihnen, die Komplexität Ihrer Organisation und die damit verbundenen administrative Kosten zu reduzieren. AD DS-Domänen innerhalb einer Gesamtstruktur umstrukturieren, können Sie verringert den Verwaltungsaufwand für Ihre Organisation von Replikations-Datenverkehr verringert werden, verringert die Menge von Benutzer- und gruppenverwaltung, die erforderlich ist und vereinfacht die Verwaltung von Die Gruppenrichtlinie. Weitere Informationen finden Sie im ADMT v3. 1-Handbuch für die Migration ([https://go.microsoft.com/fwlink/?LinkId=93678](https://go.microsoft.com/fwlink/?LinkId=93678)).  
  
Eine detaillierte Liste der Aufgaben, die Sie verwenden können, um zu planen und Bereitstellen von AD DS in einer Organisation, denen derzeit Windows 2000 Active Directory ausgeführt wird, finden Sie unter [Prüfliste: Bereitstellen von AD DS in einer Windows 2000-Organisation](https://technet.microsoft.com/library/cc732737.aspx).  
  


