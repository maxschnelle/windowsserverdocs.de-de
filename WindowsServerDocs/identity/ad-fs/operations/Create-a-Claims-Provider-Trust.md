---
ms.assetid: a4f7842c-cfca-4d78-916e-023d12a9cdf0
title: Erstellen einer Anspruchsanbieter-Vertrauensstellung
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: fbc8bb63435211a92cb7fc6aa05b1413aef939c6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59854231"
---
# <a name="create-a-claims-provider-trust"></a>Erstellen einer Anspruchsanbieter-Vertrauensstellung

>Gilt für: Windows Server 2016, Windows Server 2012 R2

Zum Hinzufügen einer neuen Anspruchsanbieter-Vertrauensstellung mithilfe der AD FS-Verwaltungs-Snap\-in und manuell konfigurieren Sie die Einstellungen, führen Sie das folgende Verfahren auf einen Ressourcenverbundserver für Partner in der Ressourcenpartnerorganisation.  
  
Mitgliedschaft in **Administratoren**, oder einer entsprechenden, auf dem lokalen Computer die Mindestanforderung zum Ausführen dieses Verfahrens.  Weitere Informationen zur Verwendung der geeigneten Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
## <a name="to-create-a-claims-provider-trust-manually"></a>So erstellen Sie manuell eine Anspruchsanbieter-Vertrauensstellung  
  
1.  Klicken Sie im Server-Manager **Tools**, und wählen Sie dann **AD FS-Verwaltung**.  
  
2.  Klicken Sie unter **Aktionen**, klicken Sie auf **Anspruchsanbieter-Vertrauensstellung hinzufügen**.  
![Anspruchsanbieter-Vertrauensstellung](media/Create-a-Claims-Provider-Trust/addclaim1.PNG)   
  
3.  Klicken Sie auf der Seite **Willkommen** auf **Start**. 
![Anspruchsanbieter-Vertrauensstellung](media/Create-a-Claims-Provider-Trust/addclaim2.PNG)    
  
4.  Klicken Sie auf der Seite **Datenquelle auswählen** auf **Daten über die Anspruchsanbieter-Vertrauensstellung manuell eingeben**, und klicken Sie anschließend auf **Weiter**.  
![Anspruchsanbieter-Vertrauensstellung](media/Create-a-Claims-Provider-Trust/addclaim3.PNG)     

5.  Geben Sie auf der Seite **Anzeigename angeben** einen Anzeigenamen**** und unter **Anmerkungen** eine Beschreibung für diese Anspruchsanbieter-Vertrauensstellung ein, und klicken Sie dann auf **Weiter**.  
![Anspruchsanbieter-Vertrauensstellung](media/Create-a-Claims-Provider-Trust/addclaim4.PNG)     

6.  Auf der **-URL konfigurieren** Seite die **URL des passiven WS-Verbund** ggf., und klicken Sie auf **Weiter**.
![Anspruchsanbieter-Vertrauensstellung](media/Create-a-Claims-Provider-Trust/addclaim5.PNG)     

8. Geben Sie auf der Seite **Bezeichner konfigurieren** unter **Bezeichner für Anspruchsanbieter-Vertrauensstellung:** den entsprechenden Bezeichner ein, und klicken Sie dann auf **Weiter**.  
![Anspruchsanbieter-Vertrauensstellung](media/Create-a-Claims-Provider-Trust/addclaim6.PNG)    

9. Klicken Sie auf der Seite **Zertifikate konfigurieren** auf **Hinzufügen**, um zu einer Zertifikatdatei zu navigieren und sie zur Zertifikatliste hinzuzufügen. Klicken Sie anschließend auf **Weiter**.  
![Anspruchsanbieter-Vertrauensstellung](media/Create-a-Claims-Provider-Trust/addclaim7.PNG)    

10. Klicken Sie auf der Seite **Bereit zum Hinzufügen der Vertrauensstellung** auf **Weiter**, um die Informationen zur Anspruchsanbieter-Vertrauensstellung zu speichern.  
![Anspruchsanbieter-Vertrauensstellung](media/Create-a-Claims-Provider-Trust/addclaim8.PNG)    

11. Klicken Sie auf der Seite **Fertig stellen** auf **Schließen**. Dadurch wird automatisch das Dialogfeld **Anspruchsregeln bearbeiten** angezeigt. Weitere Informationen zum Hinzufügen Anspruchsregeln für diese Anspruchsanbieter-Vertrauensstellung, finden Sie die folgenden zusätzliche Verweise.  
![Anspruchsanbieter-Vertrauensstellung](media/Create-a-Claims-Provider-Trust/addclaim9.PNG)

## <a name="to-create-a-claims-provider-trust-using-federation-metadata"></a>Zum Erstellen einer Anspruchsanbieter-Vertrauensstellung mithilfe von Verbundmetadaten
Zum Hinzufügen einer neuen Anspruchsanbieter-Vertrauensstellung, verwenden das AD FS-Verwaltungs-Snap-in, automatisches Importieren von Konfigurationsdaten zum Partner aus Verbundmetadaten, die der Partner in einem lokalen Netzwerk oder im Internet veröffentlicht hat führen Sie das folgende Verfahren auf einem der Verbundserver in der Ressourcenpartnerorganisation.

>[!NOTE]
>Wenn sie lange gängige Praxis, Zertifikate mit nicht qualifizierten Hostnamen verwenden, z. B. wurde https://myserver, diese Zertifikate haben keinen Sicherheitswert und können einem Angreifer ermöglichen, einen Verbunddienst zu imitieren, die Verbundmetadaten veröffentlicht. Aus diesem Grund beim Abfragen von Verbundmetadaten, Sie sollten nur verwenden einen vollständig qualifizierten Domänennamen wie z. B. https://myserver.contoso.com.

1.  Klicken Sie im Server-Manager **Tools**, und wählen Sie dann **AD FS-Verwaltung**.  
  
2.  Klicken Sie unter **Aktionen**, klicken Sie auf **Anspruchsanbieter-Vertrauensstellung hinzufügen**.  
![Anspruchsanbieter-Vertrauensstellung](media/Create-a-Claims-Provider-Trust/addclaim1.PNG)   
  
3.  Klicken Sie auf der Seite **Willkommen** auf **Start**. 
![Anspruchsanbieter-Vertrauensstellung](media/Create-a-Claims-Provider-Trust/addclaim2.PNG)    
  
4.  Klicken Sie auf der Seite **Datenquelle auswählen** auf **Online oder in einem lokalen Netzwerk veröffentlichte Daten über den Anspruchsanbieter importieren**. Geben Sie im Verbund Metadatenaustausch-Adresse (Hostname oder URL), die **Verbundmetadaten-URL der** oder den Hostnamen für den Partner, und klicken Sie dann auf **Weiter**.
![Anspruchsanbieter-Vertrauensstellung](media/Create-a-Claims-Provider-Trust/addclaim10.PNG)    

5.  Klicken Sie auf den Anzeigenamen angeben Seite Art einer **Anzeigenamen**, geben Sie unter Anmerkungen eine Beschreibung für diese Anspruchsanbieter-Vertrauensstellung ein, und klicken Sie dann auf **Weiter**.

6.  Klicken Sie auf der Seite bereit zum Hinzufügen der Vertrauensstellung auf **Weiter** von Ansprüchen vertrauen Anbieterinformationen gespeichert.

7.  Klicken Sie auf der Seite zum Fertigstellen auf **schließen**. Dadurch wird automatisch das Dialogfeld "Anspruchsregeln bearbeiten" angezeigt. Weitere Informationen zum Hinzufügen Anspruchsregeln für diese Anspruchsanbieter-Vertrauensstellung, finden Sie im Abschnitt Weitere Verweise.



    
## <a name="additional-references"></a>Weitere Verweise  
[Prüfliste: Konfigurieren der Ressourcenpartnerorganisation](../../ad-fs/deployment/Checklist--Configuring-the-Resource-Partner-Organization.md)  
  
[Prüfliste: Erstellen von Anspruchsregeln für eine Anspruchsanbieter-Vertrauensstellung](../../ad-fs/deployment/Checklist--Creating-Claim-Rules-for-a-Claims-Provider-Trust.md)  
  
## <a name="see-also"></a>Siehe auch  
[AD FS-Vorgänge](../../ad-fs/AD-FS-2016-Operations.md) 
  
