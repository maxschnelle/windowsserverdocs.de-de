---
ms.assetid: de7e1e4a-f96d-4b59-ac9b-f65f5d37a96f
title: Bereitstellen des Zugriffs auf Ihre Ansprüche unterstützenden Anwendungen und Dienste für die Benutzer anderer Organisationen
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: b4ec08182e2523b0fcb16088ec9c1d094a5923fe
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59836531"
---
# <a name="provide-users-in-another-organization-access-to-your-claims-aware-applications-and-services"></a>Bereitstellen des Zugriffs auf Ihre Ansprüche unterstützenden Anwendungen und Dienste für die Benutzer anderer Organisationen

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Wenn Sie ein Administrator in der Ressourcenpartnerorganisation in Active Directory Federation Services sind \(AD FS\) und Sie eine Bereitstellung darin besteht, verbundzugriff für Benutzer in einer anderen Organisation bereitstellen \(der Konto der Partnerorganisation\) in einen\-fähigen Anwendungen oder eine Web\--basierten Diensts, der in Ihrer Organisation befindet \(der Ressourcenpartnerorganisation\):  
  
-   Verbundbenutzer in Ihrer Organisation und in Organisationen, die einen Verbund konfiguriert haben in Ihrer Organisation vertrauen \(Kontopartner-Organisationen\) können zugreifen AD FS gesicherten Anwendungen oder Dienste, die von gehostet wird, Ihre die Organisation. Weitere Informationen finden Sie unter [Federated Web SSO Design](Federated-Web-SSO-Design.md).  
  
    Beispielsweise könnte Fabrikam anfragen, dass Mitarbeiter im Unternehmensnetzwerk Verbundzugriff auf Webdienste erhalten, die von Contoso gehostet werden.  
  
-   Verbundbenutzer, die keine direkte Zuordnung zu einer vertrauenswürdigen Organisation haben \(z. B. einzelne Kunden\), die einem Attributspeicher angemeldet sind, die in Ihrem Umkreisnetzwerk gehostet wird, können mehrere AD FS zugreifen\- gesicherte Anwendungen, die auch in Ihrem Umkreisnetzwerk, gehostet werden durch die Anmeldung einmalig von Clientcomputern, die im Internet befinden. Wenn Sie also Kundenkonten zum Aktivieren des Zugriffs auf Anwendungen oder Dienste in Ihrem Umkreisnetzwerk hosten, können Kunden, die Sie in einem Attributspeicher hosten, auf ein oder mehrere Anwendungen oder Dienste im Umkreisnetzwerk zugreifen, indem Sie sich einfach einmalig anmelden. Weitere Informationen finden Sie unter [Web SSO Design](Web-SSO-Design.md).  
  
    Fabrikam kann z. B. seinen Kunden damit einzelne\-anmelden\-auf \(SSO\) Zugriff auf mehrere Anwendungen oder Dienste, die im Umkreisnetzwerk gehostet werden.  
  
Die folgenden Komponenten sind für dieses Bereitstellungsziel erforderlich:  
  
-   **Active Directory-Domänendienste \(AD DS\):** Die ressourcenpartnerverbundserver muss Active Directory-Domäne angehören.  
  
-   **Umkreis-DNS:** Domain Name System \(DNS\) sollte einen einfachen Host enthalten \(ein\) Ressource aufzeichnen, sodass Clientcomputer den ressourcenpartnerverbundserver und den Webserver finden können. Der DNS-Server kann andere DNS-Einträge hosten, die auch im Umkreisnetzwerk erforderlich sind. Weitere Informationen finden Sie unter [Name Resolution Requirements for Federation Servers](Name-Resolution-Requirements-for-Federation-Servers.md).  
  
-   **Ressourcenpartnerverbundserver:** Die ressourcenpartnerverbundserver überprüft, ob die AD FS-Tokens, die der Kontopartner sendet. Ermittlung von Kontopartnern erfolgt über diese Verbundserver. Weitere Informationen finden Sie unter [Review the Role of the Federation Server in the Resource Partner](Review-the-Role-of-the-Federation-Server-in-the-Resource-Partner.md).  
  
-   **Webserver:** Der Webserver kann eine Webanwendung oder einen Webdienst hosten. Der Webserver bestätigt, dass er gültige AD FS-Token von Verbundbenutzer erhält, bevor er Zugriff auf die geschützte Webanwendung oder den Webdienst gestattet.  
  
    Mithilfe von Windows Identity Foundation \(WIF\), Sie können Ihre Webanwendung entwickeln oder-Dienste so, dass die It akzeptiert Verbund-anmeldeanforderungen von Benutzern, die mit jeder standardanmeldemethode, z. B. Benutzername und Kennwort vorgenommen werden.  
  
Nach dem Durchlesen der Informationen in den verknüpften Themen können Sie beginnen können, Umsetzung dieses Bereitstellungsziels anhand der Schritte in [Prüfliste: Implementieren eines Federated-Web-SSO-Entwurfs](../../ad-fs/deployment/Checklist--Implementing-a-Federated-Web-SSO-Design.md) und [Prüfliste: Implementieren eines Web-SSO-Entwurfs](../../ad-fs/deployment/Checklist--Implementing-a-Web-SSO-Design.md).  
  
Die folgende Abbildung zeigt jede der erforderlichen Komponenten für dieses Bereitstellungsziel für AD FS.  
  
![der Zugriff auf Ihre Ansprüche](media/75358b16-2a6f-4e16-9cc4-b0e614480305.gif)  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in WindowsServer 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
