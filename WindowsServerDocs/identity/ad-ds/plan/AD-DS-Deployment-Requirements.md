---
ms.assetid: e02bb152-d0db-40b0-9942-846dce75f6c7
title: AD DS-Bereitstellungsanforderungen
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: a23ba4ac8bbdb076381c8419e3a0821bee364acf
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71409031"
---
# <a name="ad-ds-deployment-requirements"></a>AD DS-Bereitstellungsanforderungen

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Die Struktur Ihrer vorhandenen Umgebung bestimmt Ihre Strategie für die Bereitstellung von Windows Server 2008 Active Directory Domain Services (AD DS). Wenn Sie eine AD DS Umgebung erstellen und keine Domänen Struktur vorhanden ist, vervollständigen Sie den Entwurf Ihrer AD DS, bevor Sie mit dem Erstellen der AD DS Umgebung beginnen. Anschließend können Sie eine neue Gesamtstruktur-Stamm Domäne bereitstellen und den Rest der Domänen Struktur entsprechend Ihrem Entwurf bereitstellen.  
  
Außerdem können Sie im Rahmen ihrer AD DS Bereitstellung entscheiden, Ihre Umgebung zu aktualisieren und neu zu strukturieren. Wenn Ihre Organisation z. b. über eine vorhandene Windows 2000-Domänen Struktur verfügt, können Sie ein direktes Upgrade einiger Domänen durchführen und andere umstrukturieren. Außerdem können Sie die Komplexität Ihrer Umgebung verringern, indem Sie entweder Domänen zwischen Gesamtstrukturen umstrukturieren oder Domänen innerhalb einer Gesamtstruktur umstrukturieren, nachdem Sie AD DS bereitgestellt haben.  
  
## <a name="deploying-a-windows-server-2008-forest-root-domain"></a>Bereitstellen einer Windows Server 2008-Gesamtstruktur-Stamm Domäne  
Die Stamm Domäne der Gesamtstruktur stellt die Grundlage für Ihre AD DS Gesamtstruktur Infrastruktur dar. Zum Bereitstellen von AD DS müssen Sie zuerst eine Gesamtstruktur-Stamm Domäne bereitstellen. Zu diesem Zweck müssen Sie den AD DS Entwurf überprüfen. Konfigurieren Sie den DNS-Dienst für die Stamm Domäne der Gesamtstruktur. Erstellen Sie die Stamm Domäne der Gesamtstruktur, die sich aus der Bereitstellung von Gesamtstruktur-Stamm Domänen Controllern, der Konfiguration der Standort Topologie für die Stamm Domäne der Gesamtstruktur und der Konfiguration von Betriebs Master Rollen (auch als Flexible Single Master Operations oder FSMO bezeichnet) und die Gesamtstruktur-und Domänen Funktionsebene. Die folgende Abbildung zeigt den Gesamtprozess der Bereitstellung einer Gesamtstruktur-Stamm Domäne.  
  
![AD DS-Anforderungen](media/AD-DS-Deployment-Requirements/033aad0b-25ff-4793-8825-88a6daa01a55.gif)  
  
Weitere Informationen finden Sie unter Bereitstellen [einer Windows Server 2008](https://technet.microsoft.com/library/cc731174.aspx)-Gesamtstruktur-Stamm Domäne.  
  
## <a name="deploying-windows-server-2008-regional-domains"></a>Bereitstellen von regionalen Windows Server 2008-Domänen  
Nachdem Sie die Bereitstellung der Gesamtstruktur-Stamm Domäne abgeschlossen haben, können Sie alle neuen regionalen Windows Server 2008-Domänen bereitstellen, die durch den Entwurf angegeben werden. Zu diesem Zweck müssen Sie Domänen Controller für jede regionale Domäne bereitstellen. Die folgende Abbildung zeigt den Prozess der Bereitstellung von regionalen Domänen.  
  
![AD DS-Anforderungen](media/AD-DS-Deployment-Requirements/89a878c8-9a94-4180-ad43-ca75316a6318.gif)  
  
Weitere Informationen finden Sie unter Bereitstellen von [Regional Domänen in Windows Server 2008](https://technet.microsoft.com/library/cc755118.aspx).  
  
## <a name="upgrading-active-directory-domains-to-windows-server-2008"></a>Aktualisieren von Active Directory Domänen auf Windows Server 2008  
Ein Upgrade Ihrer Windows 2000-oder Windows Server 2003-Domänen auf Windows Server 2008-Domänen ist eine effiziente und unkomplizierte Möglichkeit, zusätzliche Features und Funktionen von Windows Server 2008 zu nutzen. Sie können Domänen aktualisieren, um die aktuelle Netzwerk-und Domänen Konfiguration beizubehalten und gleichzeitig die Sicherheit, Skalierbarkeit und Verwaltbarkeit Ihrer Netzwerkinfrastruktur zu verbessern. Für ein Upgrade von Windows 2000 oder Windows Server 2003 auf Windows Server 2008 ist eine minimale Netzwerkkonfiguration erforderlich. Das Upgrade wirkt sich auch nur geringfügig auf Benutzer Vorgänge aus. Weitere Informationen finden Sie unter [Aktualisieren von Active Directory Domänen auf Windows Server 2008 und Windows Server 2008 R2 AD DS Domänen](https://technet.microsoft.com/library/cc731188.aspx).  
  
## <a name="restructuring-ad-ds-domains"></a>Umstrukturierung von AD DS Domänen  
Wenn Sie Domänen zwischen Windows Server 2008-Gesamtstrukturen (Gesamtstruktur übergreifende Umstrukturierung) umstrukturieren, können Sie die Anzahl der Domänen in Ihrer Umgebung verringern und so die administrative Komplexität und den Verwaltungsaufwand reduzieren. Wenn Sie Objekte zwischen Gesamtstrukturen im Rahmen dieses Restrukturierungsprozesses migrieren, sind sowohl die Quell-als auch die Zieldomänen Umgebung gleichzeitig vorhanden. Dies ermöglicht es Ihnen, ggf. während der Migration ein Rollback zur Quell Umgebung auszuführen.  
  
Wenn Sie Windows Server 2008-Domänen innerhalb einer Windows Server 2008-Gesamtstruktur umstrukturieren (Gesamtstruktur Umstrukturierung), können Sie Ihre Domänen Struktur konsolidieren und somit die administrative Komplexität und den Verwaltungsaufwand reduzieren. Wenn Sie Domänen innerhalb einer Gesamtstruktur umstrukturieren, sind die migrierten Konten in der Quell Domäne nicht mehr vorhanden.  
  
Weitere Informationen zur Verwendung des Active Directory Migration Tool (ADMT) Version 3,1 (ADMT v 3.1) zum Umstrukturieren von Domänen finden Sie im [ADMT v 3.1-Migrations Handbuch](https://go.microsoft.com/fwlink/?LinkId=93678).  
  


