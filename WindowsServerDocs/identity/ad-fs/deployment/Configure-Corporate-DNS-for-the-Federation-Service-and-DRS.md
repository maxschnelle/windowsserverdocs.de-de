---
ms.assetid: aca4a4fa-b12c-4eed-a499-f9aedb7d2fd6
title: Konfigurieren des Unternehmens-DNS für den Verbunddienst und DRS
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: cd8febf9eff300b1a83d22828874b4a577b8af36
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192316"
---
# <a name="configure-corporate-dns-for-the-federation-service-and-drs"></a>Konfigurieren des Unternehmens-DNS für den Verbunddienst und DRS
  
## <a name="step-6-add-a-host-a-and-alias-cname-resource-record-to-corporate-dns-for-the-federation-service-and-drs"></a>Schritt 6: Hinzufügen eines Hosts \(ein\) und Alias \(CNAME\) -Ressourceneintrag auf Unternehmens-DNS für den Verbunddienst und DRS  
Sie müssen die folgenden Ressourceneinträge Unternehmens Domain Name System hinzufügen \(DNS\) für Ihre Verbunddienst und Device Registration Service, die Sie in den vorherigen Schritten konfiguriert.  
  
|Eingabe|Typ|Adresse|  
|---------|--------|-----------|  
|federation\_service\_name|Host \(A\)|IP-Adresse des AD FS-Server oder die IP-Adresse des Load Balancers, die vor Ihrer AD FS-Serverfarm konfiguriert ist|  
|enterpriseregistration|Alias \(CNAME\)|federation\_server\_name.contoso.com|  
  
Sie können das folgende Verfahren zum Hinzufügen eines Hosts \(ein\) und Alias \(CNAME\) Ressourceneinträge auf Unternehmens-DNS für den Verbundserver und den Geräteregistrierungsdienst.  
  
Mitgliedschaft in **Administratoren**, oder entspricht, ist die Mindestanforderung zum Ausführen dieses Verfahrens.  Weitere Informationen zur Verwendung der geeigneten Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
#### <a name="to-add-a-host-a-and-alias-cname-resource-records-to-dns-for-your-federation-server"></a>Beim Hinzufügen eines Hosts \(ein\) und Alias \(CNAME\) -Ressourceneinträge in DNS für Ihren Verbundserver  
  
1.  Auf Sie Domänencontroller im Server-Manager auf die **Tools** Menü klicken Sie auf **DNS** , öffnen Sie die DNS-Snap\-in.  
  
2.  Erweitern Sie in der Konsolenstruktur der **Domäne\_Controller\_Namen** Knoten erweitern **Forward-Lookupzonen**mit der rechten Maustaste\-klicken Sie auf **Domäne\_Namen**, und klicken Sie dann auf **neuen Host \(A oder AAAA\)** .  
  
3.  In der **Namen** geben den Namen, die für AD FS-Farm verwendet.  
  
4.  Geben Sie in das Feld **IP-Adresse** die IP-Adresse des Verbundservers ein. Klicken Sie auf **Host hinzufügen**.  
  
5.  Rechts\-klicken Sie auf die **Domäne\_Namen** Knoten, und klicken Sie dann auf **neuer Alias \(CNAME\)** .  
  
6.  Geben Sie im Dialogfeld **Neuer Ressourcendatensatz** **enterpriseregistration** in das Feld **Aliasname** ein.  
  
7.  In den vollständig qualifizierten Domänennamen \(FQDN\) Typ von Feld Target Host **Verbund\_Service\_Farm\_Benutzername.Domänenname.com\_steht**, und klicken Sie dann Klicken Sie auf **OK**.  
  
    > [!IMPORTANT]  
    > In einer realen Bereitstellung, verfügt Ihr Unternehmen mehrere Benutzerprinzipalnamen \(UPN\) Suffixe, müssen Sie mehrere CNAME-Einträge für jede die UPN-Suffixe in DNS erstellen.  
  
## <a name="see-also"></a>Siehe auch 

[AD FS-Bereitstellung](../../ad-fs/AD-FS-Deployment.md)  

[Windows Server 2012 R2 AD FS-Bereitstellung geführt.](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
 
[Bereitstellen einer Verbundserverfarm](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)  
  

