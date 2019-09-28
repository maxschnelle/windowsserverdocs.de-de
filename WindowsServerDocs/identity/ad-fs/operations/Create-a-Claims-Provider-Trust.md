---
ms.assetid: a4f7842c-cfca-4d78-916e-023d12a9cdf0
title: Erstellen einer Anspruchsanbieter-Vertrauensstellung
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 4539e8abd1af1eca7bacb51971e6d355bb0aab28
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407653"
---
# <a name="create-a-claims-provider-trust"></a>Erstellen einer Anspruchsanbieter-Vertrauensstellung

Zum Hinzufügen einer neuen Anspruchs Anbieter-Vertrauensstellung mithilfe des AD FS-Verwaltungs-Snap @ no__t-0in und manuelles Konfigurieren der Einstellungen führen Sie das folgende Verfahren auf einem Ressourcen Partner Verbund Server in der Ressourcen Partnerorganisation aus.  
  
Sie müssen mindestens Mitglied der Gruppe **Administratoren**oder einer entsprechenden Gruppe auf dem lokalen Computer sein, um dieses Verfahren ausführen zu können.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
## <a name="to-create-a-claims-provider-trust-manually"></a>So erstellen Sie manuell eine Anspruchsanbieter-Vertrauensstellung  
  
1.  Klicken Sie in Server-Manager **auf Extras**, und wählen Sie dann **AD FS Verwaltung**aus.  
  
2.  Klicken Sie unter **Aktionen**auf **Anspruchs Anbieter-Vertrauensstellung hinzufügen**.  
![anspruchs Anbieter-Vertrauensstellung @ no__t-1   
  
3.  Klicken Sie auf der Seite **Willkommen** auf **Start**. 
![anspruchs Anbieter-Vertrauensstellung @ no__t-1    
  
4.  Klicken Sie auf der Seite **Datenquelle auswählen** auf **Daten über die Anspruchsanbieter-Vertrauensstellung manuell eingeben**, und klicken Sie anschließend auf **Weiter**.  
![anspruchs Anbieter-Vertrauensstellung @ no__t-1     

5.  Geben Sie auf der Seite **Anzeigename angeben** einen **Anzeigenamen** und unter **Anmerkungen** eine Beschreibung für diese Anspruchsanbieter-Vertrauensstellung ein, und klicken Sie dann auf **Weiter**.  
![anspruchs Anbieter-Vertrauensstellung @ no__t-1     

6.  Geben Sie auf der Seite **URL konfigurieren** die **passive WS-Verbund-URL** an, sofern zutreffend, und klicken Sie auf **weiter**.
![anspruchs Anbieter-Vertrauensstellung @ no__t-1     

8. Geben Sie auf der Seite **Bezeichner konfigurieren** unter **Bezeichner für Anspruchsanbieter-Vertrauensstellung:** den entsprechenden Bezeichner ein, und klicken Sie dann auf **Weiter**.  
![anspruchs Anbieter-Vertrauensstellung @ no__t-1    

9. Klicken Sie auf der Seite **Zertifikate konfigurieren** auf **Hinzufügen**, um zu einer Zertifikatdatei zu navigieren und sie zur Zertifikatliste hinzuzufügen. Klicken Sie anschließend auf **Weiter**.  
![anspruchs Anbieter-Vertrauensstellung @ no__t-1    

10. Klicken Sie auf der Seite **Bereit zum Hinzufügen der Vertrauensstellung** auf **Weiter**, um die Informationen zur Anspruchsanbieter-Vertrauensstellung zu speichern.  
![anspruchs Anbieter-Vertrauensstellung @ no__t-1    

11. Klicken Sie auf der Seite **Fertig stellen** auf **Schließen**. Dadurch wird automatisch das Dialogfeld **Anspruchsregeln bearbeiten** angezeigt. Weitere Informationen dazu, wie Sie mit dem Hinzufügen von Anspruchs Regeln für diese Anspruchs Anbieter-Vertrauensstellung fortfahren, finden Sie in den folgenden zusätzlichen verweisen.  
![anspruchs Anbieter-Vertrauensstellung @ no__t-1

## <a name="to-create-a-claims-provider-trust-using-federation-metadata"></a>So erstellen Sie eine Anspruchs Anbieter-Vertrauensstellung mithilfe von Verbund Metadaten
Zum Hinzufügen einer neuen Anspruchs Anbieter-Vertrauensstellung verwenden Sie das Snap-in "AD FS-Verwaltung", indem Sie Konfigurationsdaten zum Partner aus Verbund Metadaten, die der Partner in einem lokalen Netzwerk oder im Internet veröffentlicht hat, automatisch importieren. führen Sie dazu das folgende Verfahren auf einem Verbund Server in der Ressourcen Partnerorganisation.

>[!NOTE]
>Obwohl es seit langem üblich ist, Zertifikate mit nicht qualifizierten Hostnamen wie z. b. https: \//MyServer zu verwenden, haben diese Zertifikate keinen Sicherheitswert und können einem Angreifer ermöglichen, die Identität eines Verbunddienst zu annehmen, der den Verbund veröffentlicht. benötigten. Daher sollten Sie beim Abfragen von Verbund Metadaten nur einen voll qualifizierten Domänen Namen wie `https://myserver.contoso.com` verwenden.

1.  Klicken Sie in Server-Manager **auf Extras**, und wählen Sie dann **AD FS Verwaltung**aus.  
  
2.  Klicken Sie unter **Aktionen**auf **Anspruchs Anbieter-Vertrauensstellung hinzufügen**.  
![anspruchs Anbieter-Vertrauensstellung @ no__t-1   
  
3.  Klicken Sie auf der Seite **Willkommen** auf **Start**. 
![anspruchs Anbieter-Vertrauensstellung @ no__t-1    
  
4.  Klicken Sie auf der Seite **Datenquelle auswählen** auf **Online oder in einem lokalen Netzwerk veröffentlichte Daten über den Anspruchsanbieter importieren**. Geben Sie in Verbund Metadaten-Adresse (Hostname oder URL) die Verbund **Metadaten-URL** oder den Hostnamen für den Partner ein, und klicken Sie dann auf **weiter**.
![anspruchs Anbieter-Vertrauensstellung @ no__t-1    

5.  Geben Sie auf der Seite Anzeige Name angeben einen **anzeigen Amen**ein, geben Sie unter Notes eine Beschreibung für diese Anspruchs Anbieter-Vertrauensstellung ein, und klicken Sie dann auf **weiter**.

6.  Klicken Sie auf der Seite bereit zum Hinzufügen der Vertrauensstellung auf **weiter** , um die Vertrauens Informationen Ihres Anspruchs Anbieters zu speichern.

7.  Klicken Sie auf der Seite Fertigstellen auf **Schließen**. Dadurch wird automatisch das Dialogfeld "Anspruchs Regeln bearbeiten" angezeigt. Weitere Informationen zum Hinzufügen von Anspruchs Regeln für diese Anspruchs Anbieter-Vertrauensstellung finden Sie im Abschnitt Zusätzliche Verweise weiter unten.



    
## <a name="additional-references"></a>Weitere Verweise  
[Prüfliste: Konfigurieren der Ressourcen Partner Organisation @ no__t-0  
  
[Prüfliste: Erstellen von Anspruchsregeln für eine Anspruchsanbieter-Vertrauensstellung](../../ad-fs/deployment/Checklist--Creating-Claim-Rules-for-a-Claims-Provider-Trust.md)  
  
## <a name="see-also"></a>Siehe auch  
[AD FS-Vorgänge](../../ad-fs/AD-FS-2016-Operations.md) 
  
