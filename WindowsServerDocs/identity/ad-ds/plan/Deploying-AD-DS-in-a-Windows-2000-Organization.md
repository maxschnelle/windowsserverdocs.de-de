---
ms.assetid: 7530cafe-98d7-46c9-95d9-e49d39caa021
title: Bereitstellen von AD DS in einer Windows 2000-Organisation
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 1c46ff6aee03eee4169dbfe0cdff99febad312d2
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="deploying-ad-ds-in-a-windows-2000-organization"></a>Bereitstellen von AD DS in einer Windows 2000-Organisation

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Wenn Ihre Organisation derzeit Windows2000 Active Directory ausgeführt wird, können Sie die Windows Server2008 Active Directory-Domänendienste (AD DS) bereitstellen, indem Sie entweder ein direktes Upgrade der einige oder alle Ihre Domänencontroller-Betriebssysteme auf Windows Server2008 ausführen oder einführen von Domänencontrollern unter Windows Server2008 in Ihrer Umgebung.  
  
Bevor Sie einen Domänencontroller unter Windows Server2008 mit einer vorhandenen Windows2000 Active Directory-Domäne hinzufügen können, müssen Sie ausführen **Adprep**, ein Befehlszeilentool. Adprep das AD DS-Schema erweitert, aktualisiert Standardsicherheitsbeschreibungen ausgewählter Objekte und Hinzufügen neuer Verzeichnisobjekte einige Anwendungen. Adprep finden Sie auf der Windows Server2008-Installations-CD (\sources\adprep\adprep.exe). Weitere Informationen finden Sie unter Adprep ([https://go.microsoft.com/fwlink/?LinkId=99215](https://go.microsoft.com/fwlink/?LinkId=99215)).  
  
> [!NOTE]  
> Wenn Sie ein direktes Upgrade von einem vorhandenen Windows2000 AD DS-Domänencontroller auf Windows Server2008 ausführen möchten, müssen Sie zuerst den Server auf Windows Server2003 aktualisieren und dann ein Upgrade auf Windows Server2008.  
  
Die folgende Abbildungzeigt die Schrittezum Bereitstellen von Windows Server2008 AD DS in einer Umgebung, auf denen derzeit Windows2000 Active Directory ausgeführt wird.  
  
![Bereitstellung in einer Windows2000-Organisation](media/Deploying-AD-DS-in-a-Windows-2000-Organization/ee51218a-a858-49d9-8b99-9986679191c1.gif)  
  
> [!NOTE]  
> Wenn Sie die Funktionsebene der Domäne oder Gesamtstruktur auf Windows Server2008 festlegen möchten, müssen alle Domänencontroller in der Umgebung des Betriebssystems Windows Server2008 ausführen.  
  
Konsolidierung von Ressourcen und Konto Domänen, die aus einer Windows2000-Umgebung, als Teil der Windows Server2008 AD DS aktualisiert wurden erfordern Bereitstellung zwischen Gesamtstrukturen oder innerhalb einer Gesamtstruktur Neustrukturieren. Umstrukturieren von AD DS-Domänen zwischen Gesamtstrukturen hilft Ihnen bei die Komplexität Ihrer Organisation und die zugehörigen Verwaltungskosten zu reduzieren. Umstrukturieren von AD DS-Domänen innerhalb einer Gesamtstruktur, können Sie verringert den Verwaltungsaufwand für Ihre Organisation Verringern des Replikationsdatenverkehrs, reduzieren die Menge an Benutzer und Gruppe Verwaltung, die erforderlich ist und Vereinfachung der Verwaltung von Gruppenrichtlinien. Weitere Informationen finden Sie im ADMT v3. 1-Handbuch für die Migration ([https://go.microsoft.com/fwlink/?LinkId=93678](https://go.microsoft.com/fwlink/?LinkId=93678)).  
  
Eine detaillierte Liste der Aufgaben, die Sie verwenden können, zum Planen und Bereitstellen von AD DS in einer Organisation, auf denen derzeit Windows2000 Active Directory ausgeführt wird, finden Sie unter [Prüfliste: Bereitstellen von AD DS in einer Windows2000-Organisation](https://technet.microsoft.com/library/cc732737.aspx).  
  


