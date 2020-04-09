---
ms.assetid: a4f7842c-cfca-4d78-916e-023d12a9cdf0
title: Erstellen einer Anspruchsanbieter-Vertrauensstellung
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: bd5c13dbdf4258b6a87dcf599299dd7969da5acd
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80817063"
---
# <a name="create-a-claims-provider-trust"></a>Erstellen einer Anspruchsanbieter-Vertrauensstellung

Zum Hinzufügen einer neuen Anspruchs Anbieter-Vertrauensstellung mithilfe des Snap\-"AD FS-Verwaltung" in und manuelles Konfigurieren der Einstellungen führen Sie das folgende Verfahren auf einem Ressourcen Partner Verbund Server in der Ressourcen Partnerorganisation aus.  
  
Sie müssen mindestens Mitglied der Gruppe **Administratoren**oder einer entsprechenden Gruppe auf dem lokalen Computer sein, um dieses Verfahren ausführen zu können.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
## <a name="to-create-a-claims-provider-trust-manually"></a>So erstellen Sie manuell eine Anspruchsanbieter-Vertrauensstellung  
  
1.  Klicken Sie in Server-Manager **auf Extras**, und wählen Sie dann **AD FS Verwaltung**aus.  
  
2.  Klicken Sie unter **Aktionen**auf **Anspruchs Anbieter-Vertrauensstellung hinzufügen**.  
![Anspruchs Anbieter-Vertrauensstellung](media/Create-a-Claims-Provider-Trust/addclaim1.PNG)   
  
3.  Klicken Sie auf der Seite **Willkommen** auf **Start**. 
![Anspruchs Anbieter-Vertrauensstellung](media/Create-a-Claims-Provider-Trust/addclaim2.PNG)    
  
4.  Klicken Sie auf der Seite **Datenquelle auswählen** auf **Daten über die Anspruchsanbieter-Vertrauensstellung manuell eingeben**, und klicken Sie anschließend auf **Weiter**.  
![Anspruchs Anbieter-Vertrauensstellung](media/Create-a-Claims-Provider-Trust/addclaim3.PNG)     

5.  Geben Sie auf der Seite **Anzeigename angeben** einen Anzeigenamen und unter **Anmerkungen** eine Beschreibung für diese Anspruchsanbieter-Vertrauensstellung ein, und klicken Sie dann auf **Weiter**.  
![Anspruchs Anbieter-Vertrauensstellung](media/Create-a-Claims-Provider-Trust/addclaim4.PNG)     

6.  Geben Sie auf der Seite **URL konfigurieren** die **passive WS-Verbund-URL** an, sofern zutreffend, und klicken Sie auf **weiter**.
![Anspruchs Anbieter-Vertrauensstellung](media/Create-a-Claims-Provider-Trust/addclaim5.PNG)     

8. Geben Sie auf der Seite **Bezeichner konfigurieren** unter **Bezeichner für Anspruchsanbieter-Vertrauensstellung:** den entsprechenden Bezeichner ein, und klicken Sie dann auf **Weiter**.  
![Anspruchs Anbieter-Vertrauensstellung](media/Create-a-Claims-Provider-Trust/addclaim6.PNG)    

9. Klicken Sie auf der Seite **Zertifikate konfigurieren** auf **Hinzufügen**, um zu einer Zertifikatdatei zu navigieren und sie zur Zertifikatliste hinzuzufügen. Klicken Sie anschließend auf **Weiter**.  
![Anspruchs Anbieter-Vertrauensstellung](media/Create-a-Claims-Provider-Trust/addclaim7.PNG)    

10. Klicken Sie auf der Seite **Bereit zum Hinzufügen der Vertrauensstellung** auf **Weiter**, um die Informationen zur Anspruchsanbieter-Vertrauensstellung zu speichern.  
![Anspruchs Anbieter-Vertrauensstellung](media/Create-a-Claims-Provider-Trust/addclaim8.PNG)    

11. Klicken Sie auf der Seite **Fertig stellen** auf **Schließen**. Dadurch wird automatisch das Dialogfeld **Anspruchsregeln bearbeiten** angezeigt. Weitere Informationen dazu, wie Sie mit dem Hinzufügen von Anspruchs Regeln für diese Anspruchs Anbieter-Vertrauensstellung fortfahren, finden Sie in den folgenden zusätzlichen verweisen.  
![Anspruchs Anbieter-Vertrauensstellung](media/Create-a-Claims-Provider-Trust/addclaim9.PNG)

## <a name="to-create-a-claims-provider-trust-using-federation-metadata"></a>So erstellen Sie eine Anspruchs Anbieter-Vertrauensstellung mithilfe von Verbund Metadaten
Zum Hinzufügen einer neuen Anspruchs Anbieter-Vertrauensstellung verwenden Sie das Snap-in "AD FS-Verwaltung", indem Sie Konfigurationsdaten zum Partner aus Verbund Metadaten, die der Partner in einem lokalen Netzwerk oder im Internet veröffentlicht hat, automatisch importieren. führen Sie dazu das folgende Verfahren auf einem Verbund Server in der Ressourcen Partnerorganisation.

>[!NOTE]
>Obwohl es seit langem üblich ist, Zertifikate mit nicht qualifizierten Hostnamen, wie z. b. https:\//MyServer, zu verwenden, haben diese Zertifikate keinen Sicherheitswert und können einem Angreifer ermöglichen, die Identität eines Verbunddienst anzunehmen, der Verbund Metadaten veröffentlicht. Daher sollten Sie beim Abfragen von Verbund Metadaten nur einen voll qualifizierten Domänen Namen verwenden, z. b. `https://myserver.contoso.com`.

1.  Klicken Sie in Server-Manager **auf Extras**, und wählen Sie dann **AD FS Verwaltung**aus.  
  
2.  Klicken Sie unter **Aktionen**auf **Anspruchs Anbieter-Vertrauensstellung hinzufügen**.  
![Anspruchs Anbieter-Vertrauensstellung](media/Create-a-Claims-Provider-Trust/addclaim1.PNG)   
  
3.  Klicken Sie auf der Seite **Willkommen** auf **Start**. 
![Anspruchs Anbieter-Vertrauensstellung](media/Create-a-Claims-Provider-Trust/addclaim2.PNG)    
  
4.  Klicken Sie auf der Seite **Datenquelle auswählen** auf **Online oder in einem lokalen Netzwerk veröffentlichte Daten über den Anspruchsanbieter importieren**. Geben Sie in Verbund Metadaten-Adresse (Hostname oder URL) die Verbund **Metadaten-URL** oder den Hostnamen für den Partner ein, und klicken Sie dann auf **weiter**.
![Anspruchs Anbieter-Vertrauensstellung](media/Create-a-Claims-Provider-Trust/addclaim10.PNG)    

5.  Geben Sie auf der Seite Anzeige Name angeben einen **anzeigen Amen**ein, geben Sie unter Notes eine Beschreibung für diese Anspruchs Anbieter-Vertrauensstellung ein, und klicken Sie dann auf **weiter**.

6.  Klicken Sie auf der Seite bereit zum Hinzufügen der Vertrauensstellung auf **weiter** , um die Vertrauens Informationen Ihres Anspruchs Anbieters zu speichern.

7.  Klicken Sie auf der Seite Fertigstellen auf **Schließen**. Dadurch wird automatisch das Dialogfeld "Anspruchs Regeln bearbeiten" angezeigt. Weitere Informationen zum Hinzufügen von Anspruchs Regeln für diese Anspruchs Anbieter-Vertrauensstellung finden Sie im Abschnitt Zusätzliche Verweise weiter unten.



    
## <a name="additional-references"></a>Weitere Verweise  
[Prüfliste: Konfigurieren der Ressourcen Partner Organisation](../../ad-fs/deployment/Checklist--Configuring-the-Resource-Partner-Organization.md)  
  
[Prüfliste: Erstellen von Anspruchs Regeln für eine Anspruchs Anbieter-Vertrauensstellung](../../ad-fs/deployment/Checklist--Creating-Claim-Rules-for-a-Claims-Provider-Trust.md)  
  
## <a name="see-also"></a>Weitere Informationen  
[AD FS-Vorgänge](../../ad-fs/AD-FS-2016-Operations.md) 
  
