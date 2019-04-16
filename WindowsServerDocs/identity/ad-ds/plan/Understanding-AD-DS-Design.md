---
ms.assetid: d590c90e-9adf-4305-b226-eb2a5743337b
title: Grundlegendes zu AD DS-Design
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 09afe3d19add87327d05bfafba6e0492a278b968
ms.sourcegitcommit: 1c3e6375b2e8eb01cfd299d0e9478fee46905c99
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/27/2018
---
# <a name="understanding-ad-ds-design"></a>Grundlegendes zu AD DS-Design

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Organisationen können in Windows Server Active Directory-Domänendienste (AD DS) verwenden, zur Vereinfachung der Verwaltung von Benutzern und Ressourcen während des Erstellens skalierbare, sichere und verwaltbare Infrastruktur. AD DS können Sie um Ihre Netzwerkinfrastruktur, einschließlich der Filiale, die Microsoft Exchange Server und die Umgebung mit mehreren Gesamtstrukturen zu verwalten.  
  
Ein Projekt der AD DS-Bereitstellung besteht aus drei Phasen: eine Entwurfsphase, einer Bereitstellungsphase und einer Phase Vorgänge. Während der Entwurfsphase erstellt das Entwurfsteam ein Entwurfs für die logischen AD DS-Struktur, die am besten den Anforderungen für jede Abteilung in der Organisation entspricht, der den Verzeichnisdienst verwendet wird. Nachdem das Design genehmigt wurde, wird das Bereitstellungsteam testet den Entwurf in einer Testumgebung und klicken Sie dann in der Produktionsumgebung implementiert das Design. Da Tests von dem Bereitstellungsteam durchgeführt, und es potenziell wirkt sich auf der Entwurfsphase, ist ein Zwischenschritt, der Entwurf und der Bereitstellung überschneidet. Wenn die Bereitstellung abgeschlossen ist, ist das Betriebsteam zuständig für die Verwaltung des Verzeichnisdiensts.  
  
Obwohl die Windows Server-AD DS Entwurfs- und Strategien, die in diesem Handbuch beschriebenen auf umfangreiche Lab und Pilot-Programm testen und erfolgreiche Implementierung in Kundenumgebungen basieren, müssen Sie möglicherweise den AD DS-Entwurf anzupassen und Bereitstellung auf bestimmte, komplexe Umgebungen besser geeignet.  
  
-   Weitere Informationen zum Bereitstellen von AD DS in einer filialenumgebung finden Sie unter der Read-Only Domänencontroller (RODC) Branch Office Planning Guide ([https://go.microsoft.com/fwlink/?LinkId=100207](https://go.microsoft.com/fwlink/?LinkId=100207)).  
  
-   Weitere Informationen zum Bereitstellen von AD DS in einer Exchange-Umgebung finden Sie unter Exchange 2007 – Planen von Active Directory ([https://go.microsoft.com/fwlink/?LinkId=88904](https://go.microsoft.com/fwlink/?LinkId=88904)).  
  
-   Weitere Informationen zum Bereitstellen von AD DS in einer Umgebung mit mehreren Gesamtstrukturen finden Sie unter Aspekte mehrerer Gesamtstrukturen in Windows2000 und Windows Server2003 ([https://go.microsoft.com/fwlink/?LinkId=88905](https://go.microsoft.com/fwlink/?LinkId=88905)).  
  


