---
ms.assetid: 9eab8c43-a0f2-4d19-a5a4-e1399f0d5f25
title: Bestimmen der Verbundanwendungsstrategie im Ressourcenpartner
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: aca47658cc5a20f63dbd59a26ebe135dd04def92
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="determine-your-federated-application-strategy-in-the-resource-partner"></a>Bestimmen der Verbundanwendungsstrategie im Ressourcenpartner

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Ein wichtiger Bestandteil des Entwurfs einer neuen Active Directory Federation Services \(AD FS\) Infrastruktur in der Ressourcenpartnerorganisation ist die Bestimmung des vollständigen Satzes von Anwendungen und Dienste, die zur Teilnahme am Verbund verwendet werden und welche Kontopartner werden die Empfänger dieser Ressourcen. Bevor Sie eine verbundanwendungs- und servicestrategie entwerfen, berücksichtigen Sie die folgenden Fragen:  
  
-   Sie aktivieren und Bereitstellen einer Anwendung ASP.NET oder einen Windows Communication Foundation \(WCF\)-Dienst für den Verbund?  
  
-   Werden für Benutzer in Ihrem Unternehmensnetzwerk Zugriff auf die verbundanwendung oder den Dienst über die integrierte Windows-Authentifizierung erforderlich?  
  
-   Wird die verbundanwendung oder den Dienst von Benutzern in Ihrem Umkreisnetzwerk werden verwendet? Wenn dies der Fall ist, wird die integrierte Windows-Authentifizierung erforderlich sein?  
  
-   Werden alle Webserver, werden verbundanwendungen gehostet Windows Server-Betriebssystem und Internetinformationsdienste \(IIS\) ausgeführt?  
  
-   Wer wird die verbundanwendung oder der Dienst Ressourcen bereit?  
  
Durch die Beantwortung dieser Fragen hilft Ihnen ein solides AD FS-Entwurfs planen. Es wird auch dazu bei, eine verbundanwendungs- und dienststrategie, die kostengünstig ist und Ressourcen effizient erstellen. Weitere Informationen zum Entwerfen der am besten geeigneten verbundanwendungs- und dienststrategie für Ihre Organisation finden Sie unter den folgenden Themen in diesem Handbuch:  
  
-   [Bereitstellen der Active Directory-Benutzern den Zugriff auf Ihre Ansprüche unterstützenden Anwendungen und Dienste](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md)  
  
-   [Bereitstellen der Active Directory-Benutzern den Zugriff auf die Anwendungen und Dienste anderer Organisationen](Provide-Your-Active-Directory-Users-Access-to-the-Applications-and-Services-of-Other-Organizations.md)  
  
-   [Bieten Sie Benutzern in einer anderen Organisationszugriff auf Ihre Ansprüche unterstützenden Anwendungen und Dienste](Provide-Users-in-Another-Organization-Access-to-Your-Claims-Aware-Applications-and-Services.md)  
  
Weitere Informationen zum Erstellen eines ASP.NET Claims\-fähigen Anwendung oder ein WCF-Dienst finden Sie unter [Windows Identity Foundation SDK](https://go.microsoft.com/fwlink/?LinkId=122266).  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)

