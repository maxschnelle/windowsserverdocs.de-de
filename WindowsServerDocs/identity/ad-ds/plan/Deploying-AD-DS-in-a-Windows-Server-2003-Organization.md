---
ms.assetid: e6b72a80-e8b7-4305-be0c-0a290f468d36
title: Bereitstellen von AD DS in einer Windows Server 2003-Organisation
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: df1267ded5ece95dd5a3ab17e4ec6ad5d87a2f12
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="deploying-ad-ds-in-a-windows-server-2003-organization"></a>Bereitstellen von AD DS in einer Windows Server 2003-Organisation

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Wenn Ihre Organisation derzeit Windows Server2003 Active Directory ausgeführt wird, können Sie Windows Server2008 Active Directory-Domänendienste (AD DS) bereitstellen, indem Sie entweder ein direktes Upgrade der einige oder alle Ihre Domänencontroller-Betriebssysteme auf Windows Server2008 ausführen oder einführen von Domänencontrollern unter Windows Server2008 in Ihrer Umgebung.  
  
Bevor Sie einen Domänencontroller unter Windows Server2008 mit einer vorhandenen Windows Server2003 Active Directory-Domäne hinzufügen können, müssen Sie ausführen **Adprep**, ein Befehlszeilentool. Adprep das AD DS-Schema erweitert, aktualisiert Standardsicherheitsbeschreibungen ausgewählter Objekte und Hinzufügen neuer Verzeichnisobjekte einige Anwendungen. Adprep finden Sie auf der Windows Server2008-Installations-CD (\sources\adprep\adprep.exe). Weitere Informationen finden Sie unter Adprep ([https://go.microsoft.com/fwlink/?LinkId=99215](https://go.microsoft.com/fwlink/?LinkId=99215)).  
  
Die folgende Abbildungzeigt die Schrittezum Bereitstellen von Windows Server2008 AD DS in einer Umgebung, auf denen derzeit Windows Server2003 Active Directory ausgeführt wird.  
  
![In einem Windows2003-Organisation bereitstellen](media/Deploying-AD-DS-in-a-Windows-Server-2003-Organization/900c4eee-1119-4a9a-9310-755597428b71.gif)  
  
> [!NOTE]  
> Wenn Sie die Funktionsebene der Domäne oder Gesamtstruktur auf Windows Server2008 festlegen möchten, müssen alle Domänencontroller in der Umgebung des Betriebssystems Windows Server2008 ausführen.  
  
Bei der Konsolidierung Ressourcendomänen und Domänen, die direkt in einer Windows Server2003-Umgebung als Teil der Windows Server2008 AD DS-Bereitstellung zwischen Gesamtstrukturen oder innerhalb einer Gesamtstruktur Neustrukturieren erfordern möglicherweise aktualisiert werden. Umstrukturieren von AD DS-Domänen zwischen Gesamtstrukturen hilft Ihnen, reduzieren Sie die Komplexität der Darstellung Ihrer Organisation in AD DS, und erleichtert die zugehörigen Verwaltungskosten zu reduzieren. Umstrukturieren von AD DS-Domänen innerhalb einer Gesamtstruktur, hilft Ihnen, verringern den Verwaltungsaufwand für Ihre Organisation durch Verringern des Replikationsdatenverkehrs, reduzieren die Menge an Benutzer und Gruppe Verwaltung, die erforderlich ist und Vereinfachung der Verwaltung von Gruppenrichtlinien. Weitere Informationen finden Sie im ADMT v3. 1-Handbuch für die Migration ([https://go.microsoft.com/fwlink/?LinkId=93678](https://go.microsoft.com/fwlink/?LinkId=93678)).  
  
Eine detaillierte Liste der Aufgaben, die Sie verwenden können, zum Planen und Bereitstellen von AD DS in einer Organisation, auf denen Windows Server2003 Active Directory ausgeführt wird, finden Sie unter [Prüfliste: Bereitstellen von AD DS in einer Windows Server2003-Organisation](https://technet.microsoft.com/library/cc771407.aspx).  
  


