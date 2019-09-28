---
ms.assetid: aca4a4fa-b12c-4eed-a499-f9aedb7d2fd6
title: Konfigurieren des Unternehmens-DNS für den Verbunddienst und DRS
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 9f0b04f9dc050117fdefc630759c86d2b1bb1ecc
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408442"
---
# <a name="configure-corporate-dns-for-the-federation-service-and-drs"></a>Konfigurieren des Unternehmens-DNS für den Verbunddienst und DRS
  
## <a name="step-6-add-a-host-a-and-alias-cname-resource-record-to-corporate-dns-for-the-federation-service-and-drs"></a>Schritt 6: Fügen Sie dem Unternehmens-DNS für die Verbunddienst und DRS den Ressourcen Daten Satz "Host \(A @ no__t-1" und "Alias \(cname @ no__t-3" hinzu.  
Sie müssen die folgenden Ressourcen Einträge für den Unternehmens Domain Name System \(dns @ no__t-1 für den Verbund Dienst und den Geräte Registrierungsdienst hinzufügen, den Sie in den vorherigen Schritten konfiguriert haben.  
  
|Eingabe|Typ|Adresse|  
|---------|--------|-----------|  
|Verbund @ no__t-0dienst @ no__t-1name|Host \(A @ no__t-1|IP-Adresse des AD FS Servers oder die IP-Adresse des Load Balancers, der vor der AD FS Serverfarm konfiguriert ist|  
|enterpriseregistration|Alias \(cname @ no__t-1|Verbund @ no__t-0Server\_name.contoso.com|  
  
Mit dem folgenden Verfahren können Sie dem Unternehmens-DNS für den Verbund Server und den Geräte Registrierungsdienst einen Host \(A @ no__t-1-und Alias \(cname @ no__t-3-Ressourcen Einträge hinzufügen.  
  
Sie müssen mindestens Mitglied der Gruppe **Administratoren**oder einer entsprechenden Gruppe sein, um dieses Verfahren ausführen zu können.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
#### <a name="to-add-a-host-a-and-alias-cname-resource-records-to-dns-for-your-federation-server"></a>So fügen Sie einen Host \(A @ no__t-1 und Alias \(cname @ no__t-3-Ressourcen Einträge zu DNS für Ihren Verbund Server hinzu  
  
1.  Klicken Sie auf Ihrem Domänen Controller in Server-Manager im **Menü Extras** auf **DNS** , um das DNS-Snap-in @ no__t-2in zu öffnen.  
  
2.  Erweitern Sie in der Konsolen Struktur den Knoten **Domäne @ no__t-1controller @ no__t-2name** , erweitern Sie Forward-Lookupzonen, klicken Sie mit der rechten @ no__t-4click **Domäne @ no__t-6name**, und klicken Sie dann auf **neuer Host \(A oder AAAA @ no__t-9**.  
  
3.  Geben Sie im Feld **Name** den Namen ein, der für Ihre AD FS Farm verwendet werden soll.  
  
4.  Geben Sie in das Feld **IP-Adresse** die IP-Adresse des Verbundservers ein. Klicken Sie auf **Host hinzufügen**.  
  
5.  Rechts @ no__t-0klicken Sie auf den Knoten **Domäne @ no__t-2name** , und klicken Sie dann auf **Neuer Alias \(cname @ no__t-5**.  
  
6.  Geben Sie im Dialogfeld **Neuer Ressourcendatensatz** **enterpriseregistration** in das Feld **Aliasname** ein.  
  
7.  Geben Sie im Feld voll qualifizierter Domänen Name \(fqdn @ no__t-1 des Felds Zielhost den Namen **Federation @ no__t-3service @ no__t-4farm @ no__t-5name. Domain @ no__t-6name. com**ein, und klicken Sie dann auf **OK**.  
  
    > [!IMPORTANT]  
    > Wenn Ihr Unternehmen in einer realen Bereitstellung über mehrere Benutzer Prinzipal Namen \(upn @ no__t-1-Suffixe verfügt, müssen Sie mehrere CNAME-Einträge für jedes dieser UPN-Suffixe in DNS erstellen.  
  
## <a name="see-also"></a>Siehe auch 

[AD FS-Bereitstellung](../../ad-fs/AD-FS-Deployment.md)  

[Windows Server 2012 R2 AD FS Bereitstellungs Handbuch](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
 
[Bereitstellen einer Verbundserverfarm](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)  
  

