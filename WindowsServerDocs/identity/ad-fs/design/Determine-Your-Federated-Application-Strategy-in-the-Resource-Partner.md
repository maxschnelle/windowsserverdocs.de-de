---
ms.assetid: 9eab8c43-a0f2-4d19-a5a4-e1399f0d5f25
title: Bestimmen der Verbundanwendungsstrategie im Ressourcenpartner
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 0cc7a9202813cd3f8d45a72305d13ad197f5b04d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359162"
---
# <a name="determine-your-federated-application-strategy-in-the-resource-partner"></a>Bestimmen der Verbundanwendungsstrategie im Ressourcenpartner

Ein wichtiger Bestandteil des Entwurfs einer neuen Active Directory-Verbunddienste (AD FS) \(AD FS\) Infrastruktur in der Ressourcen Partnerorganisation ist das Ermitteln des vollständigen Satzes von Anwendungen und Diensten, die zur Teilnahme am Verbund verwendet werden, und von den Konto Partnern, die die Empfänger dieser Ressourcen sein werden. Bevor Sie eine Verbundanwendungs- und Servicestrategie entwerfen, berücksichtigen Sie die folgenden Fragen:  
  
-   Aktivieren und Bereitstellen Sie eine ASP.NET-Anwendung oder eine Windows Communication Foundation \(WCF\) Dienst für den Verbund?  
  
-   Benötigen Benutzer in Ihrem Unternehmensnetzwerk Zugriff auf die Verbundanwendung oder den Dienst über die integrierte Windows-Authentifizierung?  
  
-   Soll die Verbundanwendung oder der Dienst von Benutzern in Ihrem Umkreisnetzwerk verwendet werden? Wird in diesem Fall die integrierte Windows-Authentifizierung erforderlich sein?  
  
-   Sind alle Webserver, auf denen Verbund Anwendungen gehostet werden, auf denen ein Windows Server-Betriebssystem ausgeführt wird, und Internetinformationsdienste \(IIS-\)?  
  
-   Für wen stellt die Verbundanwendung oder der Dienst Ressourcen bereit?  
  
Durch das Beantworten dieser Fragen können Sie einen soliden AD FS Entwurf planen. Sie trägt auch dazu bei, eine Verbundanwendungs- und Dienststrategie zu erstellen, die kostengünstig ist und ressourceneffizient ist. Weitere Informationen zum Entwerfen der am besten geeigneten Verbundanwendungs- und Dienststrategie für Ihre Organisation finden Sie unter den folgenden Themen in diesem Handbuch:  
  
-   [Bereitstellen von Zugriff auf Ihre Ansprüche unterstützenden Anwendungen und Dienste für Active Directory-Benutzer](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md)  
  
-   [Bereitstellen von Zugriff auf die Anwendungen und Dienste anderer Organisationen für Ihre Active Directory-Benutzer](Provide-Your-Active-Directory-Users-Access-to-the-Applications-and-Services-of-Other-Organizations.md)  
  
-   [Bereitstellen von Zugriff auf Ihre Ansprüche unterstützenden Anwendungen und Dienste für die Benutzer anderer Organisationen](Provide-Users-in-Another-Organization-Access-to-Your-Claims-Aware-Applications-and-Services.md)  
  
Weitere Informationen zum Erstellen eines Anspruchs\-Aware ASP.NET-Anwendung oder eines WCF-Dienstanbieter finden Sie unter [Windows Identity Foundation SDK](https://go.microsoft.com/fwlink/?LinkId=122266).  
  
## <a name="see-also"></a>Weitere Informationen
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)

