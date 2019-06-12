---
ms.assetid: 5b9fc9c1-5d12-4ad4-8ddc-3b8a6d45b217
title: Erstellen einer Vertrauensstellung der vertrauenden Seite
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: b000d4cfd4ded7ad37dbb235a9d33c83d8951707
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66444362"
---
# <a name="create-a-relying-party-trust"></a>Erstellen einer Vertrauensstellung der vertrauenden Seite


Das folgende Dokument enthält Informationen für eine Vertrauensstellung der vertrauenden Seite manuell zu erstellen und mithilfe von Verbundmetadaten.
  
## <a name="to-create-a-claims-aware-relying-party-trust-manually"></a>Zum Erstellen einer Ansprüche Beachten der vertrauenden Seite Vertrauensstellung manuell 

Neue Anspruchsanbieter-Vertrauensstellung hinzufügen, mit der AD FS-Verwaltungs-Snap\-in und manuell konfigurieren Sie die Einstellungen, führen Sie die folgende Schritte auf einem Verbundserver.  

Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe auf dem lokalen Computer sein, um dieses Verfahren ausführen zu können.  Weitere Informationen zur Verwendung der geeigneten Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477).
  
1. Klicken Sie im Server-Manager **Tools**, und wählen Sie dann **AD FS-Verwaltung**.  
  
2.  Klicken Sie unter **Aktionen**, klicken Sie auf **Partei Vertrauensstellung der vertrauenden Seite hinzufügen**.  
![vertrauende Seite](media/Create-a-Relying-Party-Trust/addtrust1.PNG)   

3.  Auf der **Willkommen** Seite **als eine Ansprüche unterstützende** , und klicken Sie auf **starten**.  
![vertrauende Seite](media/Create-a-Relying-Party-Trust/addtrust2.PNG) 
  
4.  Klicken Sie auf der Seite **Datenquelle auswählen** auf **Daten über die vertrauende Seite manuell eingeben**, und klicken Sie anschließend auf **Weiter**.  
![vertrauende Seite](media/Create-a-Relying-Party-Trust/addtrust3.PNG) 
  
5.  Auf der **Anzeigename angeben** geben einen Namen im **Anzeigenamen**unter **Anmerkungen zu dieser** Geben Sie eine Beschreibung für diese Vertrauensstellung der vertrauenden Seite, und klicken Sie dann auf **weiter** .  
![vertrauende Seite](media/Create-a-Relying-Party-Trust/addtrust4.PNG) 

6. Auf der **Zertifikat konfigurieren** Seite, wenn Sie ein optionales tokenverschlüsselungszertifikat, klicken Sie auf haben **Durchsuchen** , suchen Sie eine Zertifikatdatei, und klicken Sie dann auf **Weiter**.  
![vertrauende Seite](media/Create-a-Relying-Party-Trust/addtrust5.PNG) 

7.  Auf der **-URL konfigurieren** Seite, führen Sie eine oder beide der folgenden, klicken Sie auf **Weiter**, und klicken Sie dann mit Schritt 8:  
  
    -   Wählen Sie die **Aktivieren der Unterstützung für WS\-Verbund Passive Protocol** Kontrollkästchen. Klicken Sie unter **der vertrauenden Seite Partei WS\-URL des passiven Verbund**, geben Sie die URL für diese Vertrauensstellung der vertrauenden Seite, und klicken Sie dann auf **Weiter**.  
  
    -   Aktivieren Sie das Kontrollkästchen **Unterstützung für das SAML 2.0 WebSSO-Protokoll aktivieren**. Klicken Sie unter **Partei SAML 2.0 SSO-Dienst-URL der vertrauenden Seite**, geben Sie die Security Assertion Markup Language \(SAML\) -Dienstendpunkt-URL für diese Vertrauensstellung der vertrauenden Seite, und klicken Sie dann auf **Weiter**.  
![vertrauende Seite](media/Create-a-Relying-Party-Trust/addtrust6.PNG)   

8. Geben Sie auf der Seite **Konfigurieren von Bezeichnern** einen oder mehrere Bezeichner für diese vertrauende Seite an, klicken Sie auf **Hinzufügen**, um diese der Liste hinzufügen, und klicken Sie dann auf **Weiter**.  
![vertrauende Seite](media/Create-a-Relying-Party-Trust/addtrust8.PNG)
  
9.  Auf der **Zugriffssteuerungsrichtlinien wählen** wählen Sie eine Richtlinie, und klicken Sie auf **Weiter**.  Weitere Informationen zu Access Control-Richtlinien, finden Sie unter [Zugriffssteuerungsrichtlinien in AD FS](Access-Control-Policies-in-AD-FS.md). 
![vertrauende Seite](media/Create-a-Relying-Party-Trust/addtrust9.PNG)

10. Überprüfen Sie auf der Seite **Bereit zum Hinzufügen der Vertrauensstellung** die Einstellungen, und klicken Sie dann auf **Weiter**, um die Informationen zur Vertrauensstellung der vertrauenden Seite zu speichern.  
   ![vertrauende Seite](media/Create-a-Relying-Party-Trust/addtrust10.PNG) 
11. Klicken Sie auf der Seite **Fertig stellen** auf **Schließen**. Dadurch wird automatisch das Dialogfeld **Anspruchsregeln bearbeiten** angezeigt.  
![vertrauende Seite](media/Create-a-Relying-Party-Trust/addtrust11.PNG) 

## <a name="to-create-a-claims-aware-relying-party-trust-using-federation-metadata"></a>Zum Erstellen einer Ansprüche Beachten der vertrauenden Seite Vertrauensstellung mithilfe von Verbundmetadaten

Zum Hinzufügen einer neuen Vertrauensstellung der vertrauenden das AD FS-Verwaltungs-Snap-in, automatisches Importieren von Konfigurationsdaten zum Partner aus Verbundmetadaten, die der Partner in einem lokalen Netzwerk oder mit dem Internet veröffentlicht mit führen Sie das folgende Verfahren auf einem der Verbundserver in der Kontopartnerorganisation.

>[!NOTE]
>Wenn sie lange gängige Praxis, Zertifikate mit nicht qualifizierten Hostnamen verwenden, z. B. wurde https://myserver, diese Zertifikate haben keinen Sicherheitswert und können einem Angreifer ermöglichen, einen Verbunddienst zu imitieren, die Verbundmetadaten veröffentlicht. Aus diesem Grund beim Abfragen von Verbundmetadaten, Sie sollten nur verwenden einen vollständig qualifizierten Domänennamen wie z. B. https://myserver.contoso.com.

Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe auf dem lokalen Computer sein, um dieses Verfahren ausführen zu können.  Weitere Informationen zur Verwendung der geeigneten Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477).


1. Klicken Sie im Server-Manager **Tools**, und wählen Sie dann **AD FS-Verwaltung**.  
  
2. Klicken Sie unter **Aktionen**, klicken Sie auf **Partei Vertrauensstellung der vertrauenden Seite hinzufügen**.  
   ![vertrauende Seite](media/Create-a-Relying-Party-Trust/addtrust1.PNG)   

3. Auf der **Willkommen** Seite **als eine Ansprüche unterstützende** , und klicken Sie auf **starten**.  
   ![vertrauende Seite](media/Create-a-Relying-Party-Trust/addtrust2.PNG) 
  
4. Auf der **Auswählen einer Datenquelle** auf <strong>veröffentlichte Daten über die vertrauende Seite importieren, online oder in einem lokalen Netzwerk *. In ** Verbundmetadaten-Adresse (Hostname oder URL)</strong>, geben Sie den Verbund-Metadaten URL oder den Hostnamen der Namen für den Partner aus, und klicken Sie dann auf **Weiter**.  
   ![vertrauende Seite](media/Create-a-Relying-Party-Trust/addtrust12.PNG) 

5. Geben Sie auf der Seite Anzeigename angeben einen Namen in **Anzeigenamen**, klicken Sie unter Hinweise geben Sie eine Beschreibung für diese Vertrauensstellung der vertrauenden Seite, und klicken Sie dann auf **Weiter**.

6. Wählen Sie auf der Seite auswählen von Ausstellungsautorisierungsregeln entweder **allen Benutzern Zugriff auf diese vertrauende** oder **allen Benutzern Zugriff auf diese vertrauende Seite Verweigern**, und klicken Sie dann auf **Weiter**.

7. Klicken Sie auf der Seite bereit zum Hinzufügen der Vertrauensstellung, überprüfen Sie die Einstellungen, und klicken Sie dann auf **Weiter** Ihre vertrauende Seite speichern Informationen zu vertrauen.

8. Klicken Sie auf der Seite zum Fertigstellen auf **schließen**. Diese Aktion zeigt automatisch das Dialogfeld "Anspruchsregeln bearbeiten". Weitere Informationen zum Hinzufügen von Anspruchsregeln für diese Vertrauensstellung für die vertrauende Seite finden Sie unter „Weitere Referenzen“.




## <a name="see-also"></a>Siehe auch  
[AD FS-Vorgänge](../../ad-fs/AD-FS-2016-Operations.md) 
