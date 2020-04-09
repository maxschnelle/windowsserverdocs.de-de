---
ms.assetid: aca4a4fa-b12c-4eed-a499-f9aedb7d2fd6
title: Konfigurieren des Unternehmens-DNS für den Verbunddienst und DRS
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 3e3f2b36b7949e4bbde78942006e985f41abf9df
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80814264"
---
# <a name="configure-corporate-dns-for-the-federation-service-and-drs"></a>Konfigurieren des Unternehmens-DNS für den Verbunddienst und DRS
  
## <a name="step-6-add-a-host-a-and-alias-cname-resource-record-to-corporate-dns-for-the-federation-service-and-drs"></a>Schritt 6: Hinzufügen eines Hosts \(einer\) und eines Alias \(CNAME-\) Ressourcen Datensatzes zum Unternehmens-DNS für die Verbunddienst und DRS  
Sie müssen die folgenden Ressourcen Einträge dem Unternehmens Domain Name System \(DNS-\) für den Verbund Dienst und den Geräte Registrierungsdienst hinzufügen, die Sie in den vorherigen Schritten konfiguriert haben.  
  
|Eintrag|Typ|Adresse|  
|---------|--------|-----------|  
|\_Name des Verbund\_Dienstanbieter|Host \(ein\)|IP-Adresse des AD FS Servers oder die IP-Adresse des Load Balancers, der vor der AD FS Serverfarm konfiguriert ist|  
|enterpriseregistration|Alias \(CNAME-\)|Verbund\_Server\_Name.contoso.com|  
  
Mit dem folgenden Verfahren können Sie dem Unternehmens-DNS für den Verbund Server und den Geräte Registrierungsdienst einen Host \(eine\) und einen Alias \(CNAME-\) Ressourcen Einträge hinzufügen.  
  
Sie müssen mindestens Mitglied der Gruppe **Administratoren**oder einer entsprechenden Gruppe sein, um dieses Verfahren ausführen zu können.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
#### <a name="to-add-a-host-a-and-alias-cname-resource-records-to-dns-for-your-federation-server"></a>So fügen Sie einen Host \(eine\) und einen Alias \(CNAME-\) Ressourcen Einträge zu DNS für Ihren Verbund Server hinzu  
  
1.  Klicken Sie auf Ihrem Domänen Controller in Server-Manager im **Menü Extras** auf **DNS** , um das DNS-Snap\-in zu öffnen.  
  
2.  Erweitern Sie in der Konsolen Struktur den Knoten **Domäne\_Controller\_Name** , erweitern Sie Forward-Lookupzonen, klicken Sie mit der rechten\-klicken Sie auf **Domänen\_Name**, und klicken Sie dann auf **neuer Host \(A oder AAAA\)** . **Forward Lookup Zones**  
  
3.  Geben Sie im Feld **Name** den Namen ein, der für Ihre AD FS Farm verwendet werden soll.  
  
4.  Geben Sie in das Feld **IP-Adresse** die IP-Adresse des Verbundservers ein. Klicken Sie auf **Host hinzufügen**.  
  
5.  Klicken Sie mit der rechten\-auf den Knoten **Domäne\_Name** , und klicken Sie dann auf **Neuer Alias \(CNAME\)** .  
  
6.  Geben Sie im Dialogfeld **Neuer Ressourcendatensatz** **enterpriseregistration** in das Feld **Aliasname** ein.  
  
7.  Geben Sie im Feld voll qualifizierter Domänen Name \(FQDN\) des Felds Zielhost den **Namen Verbund\_Dienst\_Farm\_Name. Domäne\_Name.com**ein, und klicken Sie dann auf **OK**.  
  
    > [!IMPORTANT]  
    > Wenn Ihr Unternehmen in einer realen Bereitstellung über mehrere Benutzer Prinzipal Namen \(UPN\) Suffixe verfügt, müssen Sie mehrere CNAME-Einträge für jedes dieser UPN-Suffixe in DNS erstellen.  
  
## <a name="see-also"></a>Weitere Informationen 

[AD FS-Bereitstellung](../../ad-fs/AD-FS-Deployment.md)  

[Windows Server 2012 R2 AD FS Bereitstellungs Handbuch](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
 
[Bereitstellen einer Verbundserverfarm](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)  
  

