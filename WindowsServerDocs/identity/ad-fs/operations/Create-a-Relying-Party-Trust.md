---
ms.assetid: 5b9fc9c1-5d12-4ad4-8ddc-3b8a6d45b217
title: Erstellen einer Vertrauensstellung der vertrauenden Seite
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: a0d32edd7ebc23fa724439710c6511642d9c49a3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407644"
---
# <a name="create-a-relying-party-trust"></a>Erstellen einer Vertrauensstellung der vertrauenden Seite


Das folgende Dokument enthält Informationen zum manuellen Erstellen einer Vertrauensstellung der vertrauenden Seite und zum Verwenden von Verbund Metadaten.
  
## <a name="to-create-a-claims-aware-relying-party-trust-manually"></a>So erstellen Sie manuell eine Ansprüche unterstützende Vertrauensstellung der vertrauenden Seite 

Zum Hinzufügen einer neuen Vertrauensstellung der vertrauenden Seite mithilfe des AD FS-Verwaltungs-Snap @ no__t-0in und manuelles Konfigurieren der Einstellungen führen Sie das folgende Verfahren auf einem Verbund Server aus.  

Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe auf dem lokalen Computer sein, um dieses Verfahren ausführen zu können.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477).
  
1. Klicken Sie in Server-Manager **auf Extras**, und wählen Sie dann **AD FS Verwaltung**aus.  
  
2.  Klicken Sie unter **Aktionen**auf Vertrauensstellung der **vertrauenden Seite hinzufügen**.  
![vertrauende Seite @ no__t-1   

3.  Wählen Sie auf der Seite **Willkommen** die Option **Ansprüche beachten** aus, und klicken Sie auf **starten**.  
![vertrauende Seite @ no__t-1 
  
4.  Klicken Sie auf der Seite **Datenquelle auswählen** auf **Daten über die vertrauende Seite manuell eingeben**, und klicken Sie anschließend auf **Weiter**.  
![vertrauende Seite @ no__t-1 
  
5.  Geben Sie auf der Seite **Anzeige Name angeben** einen Namen in das Feld **Anzeige Name**ein, geben Sie unter **Hinweise** eine Beschreibung für diese Vertrauensstellung der vertrauenden Seite ein, und klicken Sie dann auf **weiter**.  
![vertrauende Seite @ no__t-1 

6. Wenn Sie über ein optionales tokenverschlüsselungszertifikat verfügen, klicken Sie auf der Seite **Zertifikat konfigurieren** auf **Durchsuchen** , um eine Zertifikat Datei zu suchen, und klicken Sie dann auf **weiter**.  
![vertrauende Seite @ no__t-1 

7.  Führen Sie auf der Seite **URL konfigurieren** eine oder beide der folgenden Aktionen aus, klicken Sie auf **weiter**, und fahren Sie dann mit Schritt 8:  
  
    -   Aktivieren Sie das Kontrollkästchen **Unterstützung für das passive WS @ no__t-1federation-Protokoll aktivieren** . Geben Sie unter **vertrauende Seite WS @ no__t-1federation passive Protokoll-URL**die URL für diese Vertrauensstellung der vertrauenden Seite ein, und klicken Sie dann auf **weiter**.  
  
    -   Aktivieren Sie das Kontrollkästchen **Unterstützung für das SAML 2.0 WebSSO-Protokoll aktivieren**. Geben Sie unter **SAML 2,0 SSO-Dienst-URL**der vertrauenden Seite die Security Assertion Markup Language \(saml @ no__t-2-Dienst Endpunkt-URL für diese Vertrauensstellung der vertrauenden Seite ein, und klicken Sie dann auf **weiter**  
![vertrauende Seite @ no__t-1   

8. Geben Sie auf der Seite **Konfigurieren von Bezeichnern** einen oder mehrere Bezeichner für diese vertrauende Seite an, klicken Sie auf **Hinzufügen**, um diese der Liste hinzufügen, und klicken Sie dann auf **Weiter**.  
![vertrauende Seite @ no__t-1
  
9.  Wählen Sie unter **Access Control Richtlinie auswählen** eine Richtlinie aus, und klicken Sie auf **weiter**.  Weitere Informationen zu Access Control Richtlinien finden Sie unter [Access Control Policies in AD FS](Access-Control-Policies-in-AD-FS.md). 
![vertrauende Seite @ no__t-1

10. Überprüfen Sie auf der Seite **Bereit zum Hinzufügen der Vertrauensstellung** die Einstellungen, und klicken Sie dann auf **Weiter**, um die Informationen zur Vertrauensstellung der vertrauenden Seite zu speichern.  
   ![vertrauende Seite @ no__t-1 
11. Klicken Sie auf der Seite **Fertig stellen** auf **Schließen**. Dadurch wird automatisch das Dialogfeld **Anspruchsregeln bearbeiten** angezeigt.  
![vertrauende Seite @ no__t-1 

## <a name="to-create-a-claims-aware-relying-party-trust-using-federation-metadata"></a>So erstellen Sie eine Ansprüche unterstützende Vertrauensstellung der vertrauenden Seite mit Verbund Metadaten

Zum Hinzufügen einer neuen Vertrauensstellung der vertrauenden Seite verwenden Sie das Snap-in "AD FS-Verwaltung", indem Sie Konfigurationsdaten über den Partner automatisch aus Verbund Metadaten importieren, die der Partner in einem lokalen Netzwerk oder im Internet veröffentlicht hat. führen Sie dazu das folgende Verfahren auf einem Verbund Server in der Konto Partnerorganisation.

>[!NOTE]
>Obwohl es seit langem üblich ist, Zertifikate mit nicht qualifizierten Hostnamen wie z. b. https://myserver zu verwenden, haben diese Zertifikate keinen Sicherheitswert und können einem Angreifer ermöglichen, die Identität eines Verbunddienst anzunehmen, der Verbund Metadaten veröffentlicht. Daher sollten Sie beim Abfragen von Verbund Metadaten nur einen voll qualifizierten Domänen Namen wie https://myserver.contoso.com verwenden.

Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe auf dem lokalen Computer sein, um dieses Verfahren ausführen zu können.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477).


1. Klicken Sie in Server-Manager **auf Extras**, und wählen Sie dann **AD FS Verwaltung**aus.  
  
2. Klicken Sie unter **Aktionen**auf Vertrauensstellung der **vertrauenden Seite hinzufügen**.  
   ![vertrauende Seite @ no__t-1   

3. Wählen Sie auf der Seite **Willkommen** die Option **Ansprüche beachten** aus, und klicken Sie auf **starten**.  
   ![vertrauende Seite @ no__t-1 
  
4. Klicken Sie auf der Seite **Datenquelle auswählen** auf <strong>importieren von Daten über die vertrauende Seite, die Online oder in einem lokalen Netzwerk veröffentlicht ist *. Geben Sie in * * Verbund Metadaten-Adresse (Hostname oder URL)</strong>  die Verbund Metadaten-URL oder den Hostnamen für den Partner ein, und klicken Sie dann auf **weiter**.  
   ![vertrauende Seite @ no__t-1 

5. Geben Sie auf der Seite Anzeige Name angeben einen Namen unter **Anzeige Name**ein, geben Sie unter Hinweise eine Beschreibung für diese Vertrauensstellung der vertrauenden Seite ein, und klicken Sie dann auf **weiter**.

6. Wählen Sie auf der Seite Ausstellungs Autorisierungs Regeln auswählen entweder **allen Benutzern den Zugriff auf diese** vertrauende Seite gestatten aus, oder **verweigern Sie allen Benutzern den Zugriff auf diese**vertrauende Seite, und klicken Sie dann auf **weiter**.

7. Überprüfen Sie auf der Seite bereit zum Hinzufügen der Vertrauensstellung die Einstellungen, und klicken Sie dann auf **weiter** , um die Informationen zur Vertrauensstellung der vertrauenden Seite

8. Klicken Sie auf der Seite Fertigstellen auf **Schließen**. Diese Aktion zeigt automatisch das Dialogfeld Anspruchs Regeln bearbeiten an. Weitere Informationen zum Hinzufügen von Anspruchsregeln für diese Vertrauensstellung für die vertrauende Seite finden Sie unter „Weitere Referenzen“.




## <a name="see-also"></a>Siehe auch  
[AD FS-Vorgänge](../../ad-fs/AD-FS-2016-Operations.md) 
