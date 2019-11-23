---
ms.assetid: 7530cafe-98d7-46c9-95d9-e49d39caa021
title: Bereitstellen von AD DS in einer Windows 2000-Organisation
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: cad5deb32a31f15277c3e0e985d5b7d9b07856aa
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408919"
---
# <a name="deploying-ad-ds-in-a-windows-2000-organization"></a>Bereitstellen von AD DS in einer Windows 2000-Organisation

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Wenn in Ihrer Organisation derzeit Windows 2000 Active Directory ausgeführt wird, können Sie Windows Server 2008 Active Directory Domain Services (AD DS) bereitstellen, indem Sie entweder ein direktes Upgrade einiger oder aller der Betriebssysteme ihrer Domänen Controller auf Windows ausführen. Server 2008 oder durch Einführen von Domänen Controllern unter Windows Server 2008 in Ihrer Umgebung.  
  
Bevor Sie einen Domänen Controller, auf dem Windows Server 2008 ausgeführt wird, zu einer vorhandenen Windows 2000 Active Directory-Domäne hinzufügen können, müssen Sie **adprep**ausführen, ein Befehlszeilen Tool. Adprep erweitert das AD DS Schema, aktualisiert die Standard Sicherheits Beschreibungen ausgewählter Objekte und fügt die von einigen Anwendungen benötigten neuen Verzeichnisobjekte hinzu. Adprep ist auf dem Installations Datenträger für Windows Server 2008 verfügbar (\sources\adprep\adprep.exe). Weitere Informationen finden Sie unter adprep ([https://go.microsoft.com/fwlink/?LinkId=99215](https://go.microsoft.com/fwlink/?LinkId=99215)).  
  
> [!NOTE]  
> Wenn Sie ein direktes Upgrade eines vorhandenen Windows 2000 AD DS-Domänen Controllers auf Windows Server 2008 durchführen möchten, müssen Sie zuerst den Server auf Windows Server 2003 aktualisieren und dann ein Upgrade auf Windows Server 2008 durchführen.  
  
In der folgenden Abbildung werden die Schritte zum Bereitstellen des Windows Server 2008-AD DS in einer Netzwerkumgebung gezeigt, in der derzeit Windows 2000 Active Directory ausgeführt wird.  
  
![Bereitstellen in einer Windows 2000-Organisation](media/Deploying-AD-DS-in-a-Windows-2000-Organization/ee51218a-a858-49d9-8b99-9986679191c1.gif)  
  
> [!NOTE]  
> Wenn Sie die Domänen-oder Gesamtstruktur Funktionsebene auf Windows Server 2008 festlegen möchten, müssen alle Domänen Controller in Ihrer Umgebung das Betriebssystem Windows Server 2008 ausführen.  
  
Die Konsolidierung von Ressourcen-und Konto Domänen, die direkt aus einer Windows 2000-Umgebung im Rahmen ihrer Windows Server 2008 AD DS-Bereitstellung aktualisiert werden, erfordert möglicherweise eine Gesamtstruktur übergreifende oder Gesamtstruktur übergreifende Domänen Umstrukturierung Durch die Umstrukturierung AD DS Domänen zwischen Gesamtstrukturen können Sie die Komplexität Ihrer Organisation und die damit verbundenen administrativen Kosten reduzieren. Durch die Umstrukturierung AD DS Domänen in einer Gesamtstruktur können Sie den Verwaltungsaufwand für Ihre Organisation verringern, indem Sie den Replikations Datenverkehr verringern, die erforderliche Menge an Benutzer-und Gruppenverwaltung reduzieren und die Verwaltung von Gruppenrichtlinie. Weitere Informationen finden Sie im ADMT v 3.1-Migrations Handbuch ([https://go.microsoft.com/fwlink/?LinkId=93678](https://go.microsoft.com/fwlink/?LinkId=93678)).  
  
Eine Liste der detaillierten Aufgaben, die Sie zum Planen und Bereitstellen von AD DS in einer Organisation verwenden können, die derzeit Windows 2000 Active Directory ausgeführt wird, finden Sie unter Prüfliste: Bereitstellen von [AD DS in einer Windows 2000-Organisation](https://technet.microsoft.com/library/cc732737.aspx).  
  


