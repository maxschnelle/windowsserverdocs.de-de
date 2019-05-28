---
ms.assetid: bbb5b68f-00ad-4715-8176-0c2769b706c4
title: Bereitstellungshandbuch für AD FS unter Windows Server 2012 R2
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: c0f8dca425f644952c36a289ec72651f6383e846
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192187"
---
# <a name="deploying-a-federation-server-farm"></a>Bereitstellen einer Verbundserverfarm


Führen Sie die Aufgaben in dieser Prüfliste in der angegebenen Reihenfolge aus, um eine Verbundserverfarm bereitzustellen. Wenn ein Link auf ein grundlegendes Thema verweist, kehren Sie nach der Durchsicht des grundlegenden Themas zu dieser Prüfliste zurück, um die übrigen Aufgaben in dieser Prüfliste auszuführen.  
  
![Bereitstellen von Verbund-Serverfarm](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**Prüfliste: Bereitstellen einer Verbundserverfarm**  
  
||Aufgabe|Referenz|  
|-|--------|-------------|  
|![Verbund-Serverfarm bereitstellen](media/icon_checkboxo.gif)|Überprüfen Sie wichtige Konzepte und Überlegungen, wie die Vorbereitung der Bereitstellung von Active Directory Federation Services \(AD FS\). **Hinweis**:|![Bereitstellen von Verbund-Serverfarm](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS-Entwurfshandbuch in Windows Server 2012 R2](../../ad-fs/design/AD-FS-Design-Guide-in-Windows-Server-2012-R2.md)<br /><br />![Bereitstellen von Verbund-Serverfarm](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Understanding Key AD FS Concepts](../../ad-fs/technical-reference/Understanding-Key-AD-FS-Concepts.md)|  
||Wenn Sie Microsoft SQL Server als AD FS-Konfigurationsspeicher verwenden möchten, stellen Sie das Bereitstellen einer funktionsfähigen Instanz von SQL Server sicher.|[SQLServer](https://technet.microsoft.com/sqlserver) **Warnung:** Wenn Sie in Windows Server 2012 R2 eine AD FS-Farm erstellen und Ihre Konfigurationsdaten mithilfe von SQL Server speichern möchten, können Sie SQL Server 2008 und höhere Versionen, einschließlich SQL Server 2012, verwenden.|  
|![Verbund-Serverfarm bereitstellen](media/icon_checkboxo.gif)|Hinzufügen Ihres Computers zu einer Active Directory-Domäne.|![Bereitstellen von Verbund-Serverfarm](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Hinzufügen eines Computers zu einer Domäne](Join-a-Computer-to-a-Domain.md)|  
|![Verbund-Serverfarm bereitstellen](media/icon_checkboxo.gif)|Registrieren Sie eine Secure Sockets Layer \(SSL\) Zertifikats für AD FS.|![Bereitstellen von Verbund-Serverfarm](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[Registrieren eines SSL-Zertifikats für AD FS](Enroll-an-SSL-Certificate-for-AD-FS.md)|  
|![Verbund-Serverfarm bereitstellen](media/icon_checkboxo.gif)|Installieren des AD FS-Rollendiensts.|![Bereitstellen von Verbund-Serverfarm](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[Installieren der AD FS-Rollendiensts](Install-the-AD-FS-Role-Service.md)|  
|![Verbund-Serverfarm bereitstellen](media/icon_checkboxo.gif)|Konfigurieren eines Verbundservers.|![Bereitstellen von Verbund-Serverfarm](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[Konfigurieren eines Verbundservers](Configure-a-Federation-Server.md)|  
|![Verbund-Serverfarm bereitstellen](media/icon_checkboxo.gif)|Optionaler Schritt: Konfigurieren eines Verbundservers mit Device Registration Service \(DRS\).|![Bereitstellen von Verbund-Serverfarm](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Konfigurieren eines Verbundservers mit Device Registration Service](Configure-a-federation-server-with-Device-Registration-Service.md)|  
|![Verbund-Serverfarm bereitstellen](media/icon_checkboxo.gif)|Hinzufügen eines Hosts \(ein\) und Alias \(CNAME\) Unternehmens Domain Name System-Ressourceneintrag \(DNS\) für den Verbunddienst und DRS.|![Bereitstellen von Verbund-Serverfarm](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Konfigurieren von Unternehmens-DNS für den Verbunddienst und DRS](Configure-Corporate-DNS-for-the-Federation-Service-and-DRS.md)|  
|![Verbund-Serverfarm bereitstellen](media/icon_checkboxo.gif)|Überprüfen, ob ein Verbundserver betriebsbereit ist.|![Bereitstellen von Verbund-Serverfarm](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[überprüfen Sie, ob ein Verbund Server Betriebsbereitschaft](Verify-That-a-Federation-Server-Is-Operational.md)|  
  

## <a name="see-also"></a>Siehe auch  
[AD FS-Bereitstellung](../../ad-fs/AD-FS-Deployment.md)  

[Windows Server 2012 R2 AD FS-Bereitstellung geführt.](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
  

