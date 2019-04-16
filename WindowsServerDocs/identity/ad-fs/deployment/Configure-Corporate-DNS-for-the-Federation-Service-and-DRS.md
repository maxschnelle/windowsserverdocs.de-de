---
ms.assetid: aca4a4fa-b12c-4eed-a499-f9aedb7d2fd6
title: "Konfigurieren von Unternehmens-DNS für den Verbunddienst und DRS"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 9b66bed99cbc2ac2cdf116579adaea282c45fabe
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="configure-corporate-dns-for-the-federation-service-and-drs"></a>Konfigurieren von Unternehmens-DNS für den Verbunddienst und DRS

>Gilt für: Windows Server 2016, Windows Server2012 R2
  
## <a name="step-6-add-a-host-a-and-alias-cname-resource-record-to-corporate-dns-for-the-federation-service-and-drs"></a>Schritt 6: Hinzufügen eines Hosts \(A\) und Alias \(CNAME\) Ressourceneintrag Unternehmens-DNS für den Verbunddienst und DRS  
Sie müssen die folgenden Ressourceneinträge hinzufügen, corporate Domain Name System \(DNS\) für den Verbunddienst und Device Registration Service, die Sie in den vorherigen Schritten konfiguriert.  
  
|Eintrag|Typ|Adresse|  
|---------|--------|-----------|  
|federation\_service\_name|Hosten von \(A\)|IP-Adresse des AD FS-Server oder die IP-Adresse des Lastenausgleichs, die vor der AD FS-Server-Farm konfiguriert ist|  
|enterpriseregistration|Alias \(CNAME\)|federation\_server\_name.contoso.com|  
  
Das folgende Verfahren können eine \(A\) und Alias \(CNAME\) Hostressourceneinträge Unternehmens-DNS für den Verbundserver und den Geräteregistrierungsdienst hinzuzufügen.  
  
Mitgliedschaft in **Administratoren**, oder einer entsprechenden Gruppe, die Mindestanforderung zum Ausführen dieses Verfahrens.  Weitere Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
#### <a name="to-add-a-host-a-and-alias-cname-resource-records-to-dns-for-your-federation-server"></a>Ein Host \(A\) und Alias \(CNAME\)-Ressourceneinträge in DNS für Ihren Verbundserver hinzufügen  
  
1.  Auf Sie Domänencontroller in Server-Manager auf den **Tools** Menü klicken Sie auf **DNS** DNS-Snap-in zu öffnen.  
  
2.  Erweitern Sie in der Konsolenstruktur der **Domain\_controller\_name** Knoten, erweitern Sie **Forward-Lookupzonen**, klicken Sie auf **Domain\_name**, und klicken Sie dann auf **neuer Host \(A or AAAA\)**.  
  
3.  In den **Namen** geben den Namen für die AD FS-Farm.  
  
4.  In der **IP-Adresse** geben die IP-Adresse des Verbundservers. Klicken Sie auf **Host hinzufügen**.  
  
5.  Klicken Sie auf die **Domain\_name** Knoten, und klicken Sie dann auf **neuen Alias \(CNAME\)**.  
  
6.  In der **neuer Ressourcendatensatz** , geben Sie im Dialogfeld **Enterpriseregistration** in der **Aliasnamen** Feld.  
  
7.  In der vollständig qualifizierte Domäne den Namen \(FQDN\) von der Ziel-Host im Feld **federation\_service\_farm\_name.domain\_name.com**, und klicken Sie dann auf **OK**.  
  
    > [!IMPORTANT]  
    > In einer realen Bereitstellung hat das Unternehmen mehrere \(UPN\) Benutzerprinzipalnamen-Suffixe müssen Sie mehrere CNAME-Datensätze für die einzelnen die UPN-Suffixe in DNS erstellen.  
  
## <a name="see-also"></a>Siehe auch 

[AD FS-Bereitstellung](../../ad-fs/AD-FS-Deployment.md)  

[Windows Server2012 R2 ADFS-Bereitstellungshandbuch](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
 
[Bereitstellen einer Verbundserverfarm](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)  
  

