---
ms.assetid: bbb5b68f-00ad-4715-8176-0c2769b706c4
title: Windows Server2012 R2 ADFS-Bereitstellungshandbuch
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 05f1ea6830237813e6fd2bd6a172f467e8d81065
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="deploying-a-federation-server-farm"></a>Bereitstellen einer Verbundserverfarm

>Gilt für: Windows Server 2016, Windows Server2012 R2

Führen Sie die Aufgaben in dieser Prüfliste in der Reihenfolge, um eine Verbundserverfarm bereitzustellen. Wenn ein Link auf ein grundlegendes Thema verweist, kehren zu dieser Prüfliste zurück, nach dem Thema überprüfen, sodass Sie mit den übrigen Aufgaben in dieser Prüfliste fortfahren können.  
  
![Bereitstellen von Verbund-Serverfarm](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**Prüfliste: Bereitstellen einer Verbundserverfarm**  
  
||Aufgabe|Referenz zu|  
|-|--------|-------------|  
|![Bereitstellen von Verbund-Serverfarm](media/icon_checkboxo.gif)|Überprüfen Sie wichtige Konzepte und Aspekte bei der Vorbereitung der Active Directory-Verbunddienste \(AD FS\) bereitstellen. **Hinweis:**|![Bereitstellen von Verbund-Serverfarm](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS-Entwurfshandbuch in Windows Server2012 R2](../../ad-fs/design/AD-FS-Design-Guide-in-Windows-Server-2012-R2.md)<br /><br />![Bereitstellen von Verbund-Serverfarm](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Understanding Key AD FS Concepts](../../ad-fs/technical-reference/Understanding-Key-AD-FS-Concepts.md)|  
||Wenn Sie Microsoft SQL Server für Ihre AD FS-Konfigurationsspeicher verwenden möchten, stellen Sie zum Bereitstellen einer funktionsfähigen Instanz von SQL Server sicher.|[SQL Server](https://technet.microsoft.com/sqlserver)**Warnung:** In Windows Server2012 R2, wenn Sie möchten eine AD FS-Farm erstellen und mithilfe von SQL Server zum Speichern der Konfigurationsdaten können SQL Server2008 und höhere Versionen, einschließlich SQL Server2012.|  
|![Bereitstellen von Verbund-Serverfarm](media/icon_checkboxo.gif)|Fügen Sie den Computer einer Active Directory-Domäne.|![Bereitstellen von Verbund-Serverfarm](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Hinzufügen eines Computers zu einer Domäne](Join-a-Computer-to-a-Domain.md)|  
|![Bereitstellen von Verbund-Serverfarm](media/icon_checkboxo.gif)|Registrieren Sie ein Zertifikat für Secure Socket Layer \(SSL\) für AD FS.|![Bereitstellen von Verbund-Serverfarm](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[Registrieren eines SSL-Zertifikats für AD FS](Enroll-an-SSL-Certificate-for-AD-FS.md)|  
|![Bereitstellen von Verbund-Serverfarm](media/icon_checkboxo.gif)|Installieren des AD FS-Rollendiensts.|![Bereitstellen von Verbund-Serverfarm](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[Installieren des AD FS-Rollendiensts](Install-the-AD-FS-Role-Service.md)|  
|![Bereitstellen von Verbund-Serverfarm](media/icon_checkboxo.gif)|Konfigurieren eines Verbundservers.|![Bereitstellen von Verbund-Serverfarm](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[Configure a Federation Server](Configure-a-Federation-Server.md)|  
|![Bereitstellen von Verbund-Serverfarm](media/icon_checkboxo.gif)|Optionaler Schritt: Konfigurieren eines Verbundservers mit Device Registration Service \(DRS\).|![Bereitstellen von Verbund-Serverfarm](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Konfigurieren eines Verbundservers mit Device Registration Service](Configure-a-federation-server-with-Device-Registration-Service.md)|  
|![Bereitstellen von Verbund-Serverfarm](media/icon_checkboxo.gif)|Fügen Sie einen \(A\) und Alias \(CNAME\) Hostressourceneintrag Unternehmens Domain Name System \(DNS\) für den Verbunddienst und DRS.|![Bereitstellen von Verbund-Serverfarm](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Konfigurieren von Unternehmens-DNS für den Verbunddienst und DRS](Configure-Corporate-DNS-for-the-Federation-Service-and-DRS.md)|  
|![Bereitstellen von Verbund-Serverfarm](media/icon_checkboxo.gif)|Stellen Sie sicher, dass ein Verbundserver betriebsbereit ist.|![Bereitstellen von Verbund-Serverfarm](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[überprüfen Sie, ob eine Federation Server ist betriebsbereit](Verify-That-a-Federation-Server-Is-Operational.md)|  
  

## <a name="see-also"></a>Siehe auch  
[AD FS-Bereitstellung](../../ad-fs/AD-FS-Deployment.md)  

[Windows Server2012 R2 ADFS-Bereitstellungshandbuch](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
  

