---
ms.assetid: e02bb152-d0db-40b0-9942-846dce75f6c7
title: AD DS-Bereitstellungsanforderungen
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 7edd7de8077a077245416f859838a6bc55415edc
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="ad-ds-deployment-requirements"></a>AD DS-Bereitstellungsanforderungen

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Die Struktur der vorhandenen Umgebung bestimmt Ihre Strategie für die Bereitstellung von Windows Server2008 Active Directory-Domänendienste (AD DS). Wenn Sie eine AD DS-Umgebung erstellen, und Sie keine Domänenstruktur haben, führen Sie den AD DS-Entwurf vor dem Erstellen der AD DS-Umgebung. Klicken Sie dann können Sie bereitstellen eine neuen Gesamtstruktur-Stammdomäne und die übrigen Ihre Domänenstruktur basierend auf Ihrem Entwurf bereitstellen.  
  
Sie könnten auch als Teil der AD DS-Bereitstellung zu aktualisieren und neu strukturieren Ihrer Umgebung. Verfügt Ihre Organisation eine vorhandene Windows2000-Domänenstruktur, können Sie z.B. Führen Sie ein direktes Upgrade einige Domänen und anderen umstrukturieren. Darüber hinaus empfiehlt es sich um die Komplexität Ihrer Umgebung verringern, indem entweder Umstrukturieren von Domänen zwischen Gesamtstrukturen oder Domänen innerhalb einer Gesamtstruktur nach der Bereitstellung von AD DS.  
  
## <a name="deploying-a-windows-server-2008-forest-root-domain"></a>Bereitstellen einer Windows Server2008-Gesamtstruktur-Stammdomäne  
Gesamtstruktur-Stammdomäne bildet die Grundlage für die AD DS-Gesamtstruktur-Infrastruktur. Zum Bereitstellen von AD DS müssen Sie zuerst eine Gesamtstruktur-Stammdomäne bereitstellen. Zu diesem Zweck müssen Sie den AD DS-Entwurf überprüfen; Konfigurieren Sie den DNS-Dienst für die Gesamtstruktur-Stammdomäne. Erstellen von Gesamtstruktur-Stammdomäne, besteht aus der Bereitstellung von Domänencontrollern im Gesamtstrukturstamm, die Standorttopologie für die Gesamtstruktur-Stammdomäne konfigurieren und Konfigurieren von Betriebsmasterrollen (auch als flexible einfache Mastervorgänge oder FSMO); und Funktionsebenen der Gesamtstruktur und Domäne heraufstufen. Die folgende Abbildungzeigt den gesamten Vorgang der Bereitstellung einer Gesamtstruktur-Stammdomäne.  
  
![AD DS-Anforderungen](media/AD-DS-Deployment-Requirements/033aad0b-25ff-4793-8825-88a6daa01a55.gif)  
  
Weitere Informationen finden Sie unter [Bereitstellen einer Gesamtstruktur-Stammdomäne von Windows Server2008](https://technet.microsoft.com/library/cc731174.aspx).  
  
## <a name="deploying-windows-server-2008-regional-domains"></a>Bereitstellen von Regionaldomänen für Windows Server2008  
Nach Abschluss die Bereitstellung der Stammdomäne der Gesamtstruktur können Sie alle neuen Windows Server2008-Regionaldomänen bereitstellen, die vom Entwurf angegeben werden. Zu diesem Zweck müssen Sie den Domänencontroller für jede Regionaldomäne bereitstellen. Die folgende Abbildungzeigt den Prozess der Bereitstellung von Regionaldomänen.  
  
![AD DS-Anforderungen](media/AD-DS-Deployment-Requirements/89a878c8-9a94-4180-ad43-ca75316a6318.gif)  
  
Weitere Informationen finden Sie unter [Bereitstellen von Windows Server2008 Regionaldomänen](https://technet.microsoft.com/library/cc755118.aspx).  
  
## <a name="upgrading-active-directory-domains-to-windows-server-2008"></a>Aktualisieren von Active Directory-Domänen auf Windows Server2008  
Aktualisieren Ihre Windows2000 oder Windows Server2003-Domänen auf Windows Server2008-Domänen ist eine effiziente und einfache Möglichkeit, zusätzliche Windows Server2008-Features und Funktionen zu nutzen. Sie können zum Verwalten der aktuellen Netzwerk- und Konfigurations beim Verbessern der Sicherheit, Skalierbarkeit und verwaltbarkeit Ihrer Netzwerkinfrastruktur Domänen aktualisieren. Aktualisieren von Windows2000 oder Windows Server2003 auf Windows Server2008 erfordert minimale Netzwerkkonfiguration. Upgrade wirkt sich auch etwas auf Benutzeraktionen. Weitere Informationen finden Sie unter [Aktualisieren von Active Directory-Domänen auf Windows Server2008 und Windows Server2008 R2 AD DS-Domänen](https://technet.microsoft.com/library/cc731188.aspx).  
  
## <a name="restructuring-ad-ds-domains"></a>Umstrukturieren von AD DS-Domänen  
Wenn Sie bei der Umstrukturierung von Domänen zwischen Gesamtstrukturen für Windows Server2008 (zwischen Gesamtstrukturen umstrukturieren), können Sie die Anzahl der Domänen in Ihrer Umgebung reduzieren und administrative Komplexität und den Aufwand zu verringern. Beim Migrieren von Objekten zwischen Gesamtstrukturen im Rahmen dieser Prozess Umstrukturierung vorhanden der Quelle Domänen- und Ziel-Domäne-Umgebung gleichzeitig. Dadurch können Sie die Quell-Umgebung während der Migration, ggf. ein Rollback auf.  
  
Wenn Sie Windows Server2008-Domänen innerhalb einer Windows Server2008 (Umstrukturierung von Domänen innerhalb einer Gesamtstruktur) umstrukturieren, können Sie Ihre Domänenstruktur konsolidieren und administrative Komplexität und den Aufwand zu verringern. Wenn Sie bei der Umstrukturierung von Domänen innerhalb einer Gesamtstruktur, sind die migrierten Konten in der Quelldomäne nicht mehr vorhanden.  
  
Weitere Informationen dazu, wie Sie die Active Directory Migration Tool (ADMT) Version 3.1 (ADMT v3. 1) zu verwenden, um die Umstrukturierung von Domänen finden Sie unter [ADMT v3. 1-Handbuch für die Migration](https://go.microsoft.com/fwlink/?LinkId=93678).  
  


