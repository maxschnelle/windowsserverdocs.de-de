---
ms.assetid: e02bb152-d0db-40b0-9942-846dce75f6c7
title: AD DS-Bereitstellungsanforderungen
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: d21491f5ce9c15ecc514e4be24a91de28b0fd0ce
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59890971"
---
# <a name="ad-ds-deployment-requirements"></a>AD DS-Bereitstellungsanforderungen

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Die Struktur Ihrer vorhandenen Umgebung bestimmt Ihre Strategie für die Bereitstellung von Windows Server 2008 Active Directory Domain Services (AD DS). Wenn Sie eine AD DS-Umgebung erstellen, und Sie verfügen nicht über die Domänenstruktur, führen Sie Ihren AD DS-Entwurf, bevor Sie beginnen, AD DS-Umgebung erstellen. Stellen Sie dann, Sie können eine neuen Gesamtstruktur-Stammdomäne und den Rest Ihrer Domänenstruktur gemäß Ihrem Entwurf bereitstellen.  
  
Sie könnten auch als Teil der AD DS-Bereitstellung, aktualisieren und Umstrukturieren Ihrer Umgebung. Verfügt Ihre Organisation auf eine vorhandene Windows 2000-Domänenstruktur, können Sie z. B. ein direktes Upgrade von einigen Domänen durchführen und andere umstrukturieren. Sie könnten darüber hinaus verringern Sie die Komplexität Ihrer Umgebung durch Umstrukturieren von Domänen zwischen Gesamtstrukturen oder Domänen innerhalb einer Gesamtstruktur umstrukturieren, nachdem Sie AD DS bereitstellen.  
  
## <a name="deploying-a-windows-server-2008-forest-root-domain"></a>Bereitstellen einer Windows Server 2008-Gesamtstruktur-Stammdomäne  
Gesamtstruktur-Stammdomäne bildet die Grundlage für die AD DS-Gesamtstruktur-Infrastruktur. Zum Bereitstellen von AD DS müssen Sie zuerst eine Stammdomäne der Gesamtstruktur bereitstellen. Zu diesem Zweck müssen Sie Ihren AD DS-Entwurf überprüfen; Konfigurieren Sie den DNS-Dienst für die Gesamtstruktur-Stammdomäne; Erstellen von Gesamtstruktur-Stammdomäne, die von Domänencontrollern im Gesamtstrukturstamm bereitstellen, konfigurieren die Standorttopologie für die Gesamtstruktur-Stammdomäne und Konfigurieren von Betriebsmasterrollen (auch bekannt als flexible einfache Mastervorgänge oder FSMO) besteht und das Heraufsetzen der Funktionsebenen der Gesamtstruktur und Domäne. Die folgende Abbildung zeigt den gesamten Prozess der Bereitstellung von einer Gesamtstruktur-Stammdomäne an.  
  
![AD DS-Anforderungen](media/AD-DS-Deployment-Requirements/033aad0b-25ff-4793-8825-88a6daa01a55.gif)  
  
Weitere Informationen finden Sie unter [Bereitstellen einer Windows Server 2008-Gesamtstruktur-Stammdomäne](https://technet.microsoft.com/library/cc731174.aspx).  
  
## <a name="deploying-windows-server-2008-regional-domains"></a>Bereitstellen von Regionaldomänen für Windows Server 2008  
Nach Abschluss die Bereitstellung der Stammdomäne der Gesamtstruktur können Sie neuen Regionaldomänen für Windows Server 2008 bereitstellen, die vom Entwurf angegeben werden. Zu diesem Zweck müssen Sie die Domänencontroller für jede Regionaldomäne bereitstellen. Die folgende Abbildung zeigt den Prozess Bereitstellen von Regionaldomänen.  
  
![AD DS-Anforderungen](media/AD-DS-Deployment-Requirements/89a878c8-9a94-4180-ad43-ca75316a6318.gif)  
  
Weitere Informationen finden Sie unter [Bereitstellen von Windows Server 2008 Regionaldomänen](https://technet.microsoft.com/library/cc755118.aspx).  
  
## <a name="upgrading-active-directory-domains-to-windows-server-2008"></a>Aktualisieren von Active Directory-Domänen auf Windows Server 2008  
Aktualisieren Ihrer Windows 2000 oder Windows Server 2003-Domänen auf Windows Server 2008-Domänen ist ein wirksamer und einfacher Weg, um zusätzliche Windows Server 2008- Funktionen nutzen. Sie können zum Verwalten Ihrer aktuellen Netzwerk und die Domäne der Konfigurations bei gleichzeitiger Verbesserung der Sicherheit, Skalierbarkeit und verwaltbarkeit Ihrer Netzwerkinfrastruktur Domänen aktualisieren. Aktualisieren von Windows 2000 oder Windows Server 2003 auf Windows Server 2008 ist die minimale Netzwerkkonfiguration erforderlich. Upgrade hat, wird auch nur eine geringe Auswirkung auf Vorgänge. Weitere Informationen finden Sie unter [Aktualisieren von Active Directory-Domänen auf Windows Server 2008 und Windows Server 2008 R2 AD DS-Domänen](https://technet.microsoft.com/library/cc731188.aspx).  
  
## <a name="restructuring-ad-ds-domains"></a>Umstrukturieren von AD DS-Domänen  
Wenn Sie bei der Umstrukturierung von Domänen zwischen Gesamtstrukturen für Windows Server 2008 (zwischen Gesamtstrukturen umstrukturieren), können die Anzahl der Domänen in Ihrer Umgebung verringern und daher reduzieren die Komplexität der Verwaltung und den Aufwand. Beim Migrieren von Objekten zwischen Gesamtstrukturen im Rahmen dieser Umstrukturierung Prozess werden sowohl die Domänen- und Ziel Domäne quellumgebungen gleichzeitig vorhanden. Dadurch können Sie auf der Quell-und zielumgebung während der Migration bei Bedarf zurückzusetzen.  
  
Wenn Sie Windows Server 2008-Domänen innerhalb einer Windows Server 2008 (Umstrukturierung von Domänen) umstrukturieren, können Sie Ihre Domänenstruktur konsolidieren und daher reduzieren die Komplexität der Verwaltung und den Aufwand. Wenn Sie Domänen innerhalb einer Gesamtstruktur umstrukturieren, ist die migrierten Konten nicht mehr vorhanden, in der Quelldomäne.  
  
Weitere Informationen dazu, wie Sie die Active Directory Migration Tool (ADMT) der Version 3.1 (ADMT v3. 1) zu verwenden, um die Umstrukturierung von Domänen finden Sie unter [ADMT v3. 1-Handbuch für die Migration](https://go.microsoft.com/fwlink/?LinkId=93678).  
  


