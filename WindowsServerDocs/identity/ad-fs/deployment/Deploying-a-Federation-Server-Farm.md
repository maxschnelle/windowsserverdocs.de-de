---
ms.assetid: bbb5b68f-00ad-4715-8176-0c2769b706c4
title: Bereitstellungshandbuch für AD FS unter Windows Server 2012 R2
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: e5507cd567114d17c6500655ee210b70bd9ea1ec
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408416"
---
# <a name="deploying-a-federation-server-farm"></a>Bereitstellen einer Verbundserverfarm


Führen Sie die Aufgaben in dieser Prüfliste in der angegebenen Reihenfolge aus, um eine Verbundserverfarm bereitzustellen. Wenn ein Link auf ein grundlegendes Thema verweist, kehren Sie nach der Durchsicht des grundlegenden Themas zu dieser Prüfliste zurück, um die übrigen Aufgaben in dieser Prüfliste auszuführen.  
  
![Bereitstellen einer Verbund Serverfarm-Prüfliste: bereitstellen](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**einer Verbund Serverfarm**  
  
||Aufgabe|Verweis|  
|-|--------|-------------|  
|![Bereitstellen einer Verbund Serverfarm](media/icon_checkboxo.gif)|Informieren Sie sich über wichtige Konzepte und Überlegungen bei der Vorbereitung der Bereitstellung Active Directory-Verbunddienste (AD FS) \(AD FS\). **Hinweis:**|![Bereitstellen einer Verbund Serverfarm](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS Entwurfs Handbuch in Windows Server 2012 R2](../../ad-fs/design/AD-FS-Design-Guide-in-Windows-Server-2012-R2.md)<br /><br />![Bereitstellen der grundlegenden](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS Konzepte](../../ad-fs/technical-reference/Understanding-Key-AD-FS-Concepts.md) der Verbund Serverfarm|  
||Wenn Sie Microsoft SQL Server als AD FS-Konfigurationsspeicher verwenden möchten, stellen Sie das Bereitstellen einer funktionsfähigen Instanz von SQL Server sicher.|[SQL Server](https://technet.microsoft.com/sqlserver) **Warnung:** Wenn Sie in Windows Server 2012 R2 eine AD FS Farm erstellen und SQL Server zum Speichern der Konfigurationsdaten verwenden möchten, können Sie SQL Server 2008 und neuere Versionen verwenden, einschließlich SQL Server 2012.|  
|![Bereitstellen einer Verbund Serverfarm](media/icon_checkboxo.gif)|Hinzufügen Ihres Computers zu einer Active Directory-Domäne.|![Bereitstellen einer Verbund Serverfarm](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Hinzufügen eines Computers zu einer Domäne](Join-a-Computer-to-a-Domain.md)|  
|![Bereitstellen einer Verbund Serverfarm](media/icon_checkboxo.gif)|Registrieren Sie einen sicheren socketlayer-\(SSL-\) Zertifikat für AD FS.|![Bereitstellen einer Verbund Serverfarm](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[ein SSL-Zertifikat für AD FS](Enroll-an-SSL-Certificate-for-AD-FS.md)|  
|![Bereitstellen einer Verbund Serverfarm](media/icon_checkboxo.gif)|Installieren des AD FS-Rollendiensts.|![Bereitstellen einer Verbund Serverfarm](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[Installieren Sie den Rollen Dienst "AD FS](Install-the-AD-FS-Role-Service.md) ".|  
|![Bereitstellen einer Verbund Serverfarm](media/icon_checkboxo.gif)|Konfigurieren eines Verbundservers.|![Bereitstellen einer Verbund Serverfarm](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[Konfigurieren eines Verbund Servers](Configure-a-Federation-Server.md)|  
|![Bereitstellen einer Verbund Serverfarm](media/icon_checkboxo.gif)|Optionaler Schritt: Konfigurieren eines Verbund Servers mit dem Geräte Registrierungsdienst \(DRS\).|![Bereitstellen einer Verbund Serverfarm](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Konfigurieren eines Verbund Servers mit dem Geräte Registrierungsdienst](Configure-a-federation-server-with-Device-Registration-Service.md)|  
|![Bereitstellen einer Verbund Serverfarm](media/icon_checkboxo.gif)|Fügen Sie dem Unternehmens Domain Name System \(DNS-\) für den Verbund Dienst und DRS einen Host \(eine\) und einen Alias \(CNAME-\) Ressourcen Daten Satz hinzu.|![Bereitstellen einer Verbund Serverfarm](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Konfigurieren des Unternehmens-DNS für die Verbunddienst und DRS](Configure-Corporate-DNS-for-the-Federation-Service-and-DRS.md)|  
|![Bereitstellen einer Verbund Serverfarm](media/icon_checkboxo.gif)|Überprüfen, ob ein Verbundserver betriebsbereit ist.|![Bereitstellen einer Verbund Serverfarm](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Überprüfen Sie, ob ein Verbund Serverbetriebs bereit ist](Verify-That-a-Federation-Server-Is-Operational.md) .|  
  

## <a name="see-also"></a>Weitere Informationen  
[AD FS-Bereitstellung](../../ad-fs/AD-FS-Deployment.md)  

[Windows Server 2012 R2 AD FS Bereitstellungs Handbuch](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
  

