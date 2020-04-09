---
ms.assetid: ef83960f-d2cf-441f-b2b6-d97822ec7149
title: Erstellen einer Regel zum Transformieren eines eingehenden Anspruchs
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 43768b282005ba77d22985aa9a0d563125a97289
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80816533"
---
# <a name="create-a-rule-to-transform-an-incoming-claim"></a>Erstellen einer Regel zum Transformieren eines eingehenden Anspruchs


Mithilfe der Regel Vorlage zum **Transformieren eines eingehenden Anspruchs** in Active Directory-Verbunddienste (AD FS) \(AD FS\)können Sie einen eingehenden Anspruch auswählen, seinen Anspruchstyp ändern und seinen Anspruchs Wert ändern. Beispielsweise können Sie diese Regel Vorlage verwenden, um eine Regel zu erstellen, die einen Rollen Anspruch mit dem gleichen Anspruchs Wert eines eingehenden Gruppen Anspruchs sendet. Sie können diese Regel auch verwenden, um einen Gruppen Anspruch mit dem Anspruchs Wert "Käufer" zu senden, wenn ein eingehender Gruppen Anspruch mit dem Wert "Admins" vorhanden ist. Sie können auch nur den Benutzer Prinzipal Namen \(UPN\) Ansprüche, die mit @fabrikamenden, senden.  
  
Mithilfe des folgenden Verfahrens können Sie eine Anspruchs Regel mit dem AD FS-Verwaltungs-Snap\-in erstellen.  
  
Sie müssen mindestens Mitglied der Gruppe **Administratoren**oder einer entsprechenden Gruppe auf dem lokalen Computer sein, um dieses Verfahren ausführen zu können.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477). 

## <a name="to-create-a-rule-to-transform-an-incoming-claim-on-a-relying-party-trust-in-windows-server-2016"></a>So erstellen Sie eine Regel zum Transformieren eines eingehenden Anspruchs für eine Vertrauensstellung der vertrauenden Seite in Windows Server 2016 

1.  Klicken Sie in Server-Manager **auf Extras**, und wählen Sie dann **AD FS Verwaltung**aus.  
  
2.  Klicken Sie in der Konsolen Struktur unter **AD FS**auf Vertrauens Stellungen der vertrauenden **Seite**. 
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)  
  
3.  Klicken Sie mit der rechten\-auf die ausgewählte Vertrauensstellung, und klicken Sie dann auf **Anspruchs Ausstellungs Richtlinie bearbeiten**.
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule10.PNG)   
  
4.  Klicken Sie im Dialogfeld **Richtlinie für Anspruchs Ausstellung bearbeiten** unter Ausstellungs **Transformationsregeln** auf **Regel hinzufügen** , um den Regel-Assistenten zu starten. 
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule11.PNG)    

5.  Wählen Sie auf der Seite **Regel Vorlage auswählen** unter **Anspruchs Regel Vorlage**die **Option eingehenden Anspruch** in der Liste umwandeln aus, und klicken Sie dann auf **weiter**.  
![Regel erstellen](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform3.PNG)      

6.  Geben Sie auf der Seite **Regel konfigurieren** unter **Anspruchs Regel Name**den anzeigen Amen für diese Regel ein. Wählen Sie unter **Typ des eingehenden Anspruchs**einen Anspruchstyp in der Liste aus. Wählen Sie unter **Typ des ausgehenden Anspruchs einen Anspruchstyp**in der Liste aus, und wählen Sie dann eine der folgenden Optionen aus, die von den Anforderungen Ihrer Organisation abhängig sind:  
  
    -   **Alle Anspruchs Werte weiterleiten**  
  
    -   **Einen eingehenden Anspruchs Wert durch einen anderen ausgehenden Anspruchs Wert ersetzen**  
  
    -   **Ersetzen eingehender e\-e-Mail-suffixansprüche durch ein neues e\-Mail Suffix**  
![Regel erstellen](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform4.PNG)   

7.  Klicken Sie auf **Fertig** stellen.  
  
8.  Klicken Sie im Dialogfeld **Anspruchs Regeln bearbeiten** auf **OK** , um die Regel zu speichern.
  
> [!NOTE]  
> Wenn Sie das dynamische Access Control Szenario einrichten, in dem AD FS von\-ausgestellte Ansprüche verwendet werden, erstellen Sie zunächst eine Transformations Regel für die Anspruchs Anbieter-Vertrauensstellung, und geben Sie in **eingehender Anspruchstyp**den Namen des eingehenden Anspruchs ein. Wenn Sie zuvor eine Anspruchs Beschreibung erstellt haben, wählen Sie Sie aus der Liste aus. Wählen Sie anschließend unter **Typ des ausgehenden Anspruchs**die gewünschte Anspruchs-URL aus, und erstellen Sie dann eine Transformations Regel für die Vertrauensstellung der vertrauenden Seite, um den geräteanspruch auszugeben.  
>   
> Weitere Informationen zu dynamischen Access Control Szenarien finden Sie unter [dynamische Access Control Inhalts Roadmap](../../solution-guides/dynamic-access-control--scenario-overview.md) oder [Verwenden von AD DS Ansprüchen mit AD FS](https://technet.microsoft.com/library/hh831504.aspx). 

## <a name="to-create-a-rule-to-transform-an-incoming-claim-on-a-claims-provider-trust-in-windows-server-2016"></a>So erstellen Sie eine Regel zum Transformieren eines eingehenden Anspruchs für eine Anspruchs Anbieter-Vertrauensstellung in Windows Server 2016 
  
1.  Klicken Sie in Server-Manager **auf Extras**, und wählen Sie dann **AD FS Verwaltung**aus.  
  
2.  Klicken Sie in der Konsolen Struktur unter **AD FS**auf **Anspruchs Anbieter**-Vertrauens Stellungen. 
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule1.PNG)  
  
3.  Klicken Sie mit der rechten\-auf die ausgewählte Vertrauensstellung und dann auf **Anspruchs Regeln bearbeiten**.
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule2.PNG)   
  
4.  Klicken Sie im Dialogfeld **Anspruchs Regeln bearbeiten** unter **Akzeptanz Transformationsregeln** auf **Regel hinzufügen** , um den Regel-Assistenten zu starten.
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule3.PNG)    

5.  Wählen Sie auf der Seite **Regel Vorlage auswählen** unter **Anspruchs Regel Vorlage**die **Option eingehenden Anspruch** in der Liste umwandeln aus, und klicken Sie dann auf **weiter**.  
![Regel erstellen](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform3.PNG)      

6.  Geben Sie auf der Seite **Regel konfigurieren** unter **Anspruchs Regel Name**den anzeigen Amen für diese Regel ein. Wählen Sie unter **Typ des eingehenden Anspruchs**einen Anspruchstyp in der Liste aus. Wählen Sie unter **Typ des ausgehenden Anspruchs einen Anspruchstyp**in der Liste aus, und wählen Sie dann eine der folgenden Optionen aus, die von den Anforderungen Ihrer Organisation abhängig sind:  
  
    -   **Alle Anspruchs Werte weiterleiten**  
  
    -   **Einen eingehenden Anspruchs Wert durch einen anderen ausgehenden Anspruchs Wert ersetzen**  
  
    -   **Ersetzen eingehender e\-e-Mail-suffixansprüche durch ein neues e\-Mail Suffix**  
![Regel erstellen](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform4.PNG)       

7.  Klicken Sie auf **Fertig** stellen.  
  
8.  Klicken Sie im Dialogfeld **Anspruchs Regeln bearbeiten** auf **OK** , um die Regel zu speichern.  

> [!NOTE]  
> Wenn Sie das dynamische Access Control Szenario einrichten, in dem AD FS von\-ausgestellte Ansprüche verwendet werden, erstellen Sie zunächst eine Transformations Regel für die Anspruchs Anbieter-Vertrauensstellung, und geben Sie in **eingehender Anspruchstyp**den Namen des eingehenden Anspruchs ein. Wenn Sie zuvor eine Anspruchs Beschreibung erstellt haben, wählen Sie Sie aus der Liste aus. Wählen Sie anschließend unter **Typ des ausgehenden Anspruchs**die gewünschte Anspruchs-URL aus, und erstellen Sie dann eine Transformations Regel für die Vertrauensstellung der vertrauenden Seite, um den geräteanspruch auszugeben.  
>   
> Weitere Informationen zu dynamischen Access Control Szenarien finden Sie unter [dynamische Access Control Inhalts Roadmap](../../solution-guides/dynamic-access-control--scenario-overview.md) oder [Verwenden von AD DS Ansprüchen mit AD FS](https://technet.microsoft.com/library/hh831504.aspx).   
  
## <a name="to-create-a-rule-to-transform-an-incoming-claim-in-windows-server-2012-r2"></a>So erstellen Sie eine Regel zum Transformieren eines eingehenden Anspruchs in Windows Server 2012 R2 
  
1.  Klicken Sie in Server-Manager **auf Extras, und**klicken Sie dann auf **AD FS Verwaltung**.  
  
2.  Klicken Sie in der Konsolen Struktur unter **AD FS Vertrauens Stellungen\\Vertrauens**Stellungen entweder auf **Anspruchs Anbieter** -Vertrauens Stellungen oder Vertrauens Stellungen der vertrauenden **Seite**, und klicken Sie dann auf eine bestimmte Vertrauensstellung in der Liste, in der Sie diese Regel erstellen möchten.  
  
3.  Klicken Sie mit der rechten\-auf die ausgewählte Vertrauensstellung und dann auf **Anspruchs Regeln bearbeiten**.  
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule6.PNG) 
  
4.  Wählen Sie im Dialogfeld **Anspruchs Regeln bearbeiten** eine der folgenden Registerkarten aus, die von der zu bearbeitenden Vertrauensstellung und dem Regelsatz abhängt, den Sie diese Regel erstellen möchten, und klicken Sie dann auf **Regel hinzufügen** , um den Regel-Assistenten zu starten, der diesem Regelsatz zugeordnet ist:  
  
    -   **Akzeptanz Transformationsregeln**  
  
    -   **Ausstellungs Transformationsregeln**  
  
    -   **Ausstellungs Autorisierungs Regeln**  
  
    -   **Delegierungs Autorisierungs Regeln**  
![Regel erstellen](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG)
  
5.  Wählen Sie auf der Seite **Regel Vorlage auswählen** unter **Anspruchs Regel Vorlage**die **Option eingehenden Anspruch** in der Liste umwandeln aus, und klicken Sie dann auf **weiter**.  
![Regel erstellen](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform1.PNG)   

6.  Geben Sie auf der Seite **Regel konfigurieren** unter **Anspruchs Regel Name**den anzeigen Amen für diese Regel ein. Wählen Sie unter **Typ des eingehenden Anspruchs**einen Anspruchstyp in der Liste aus. Wählen Sie unter **Typ des ausgehenden Anspruchs einen Anspruchstyp**in der Liste aus, und wählen Sie dann eine der folgenden Optionen aus, die von den Anforderungen Ihrer Organisation abhängig sind:  
  
    -   **Alle Anspruchs Werte weiterleiten**  
  
    -   **Einen eingehenden Anspruchs Wert durch einen anderen ausgehenden Anspruchs Wert ersetzen**  
  
    -   **Ersetzen eingehender e\-e-Mail-suffixansprüche durch ein neues e\-Mail Suffix**  
![Regel erstellen](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform2.PNG)  

> [!NOTE]  
> Wenn Sie das dynamische Access Control Szenario einrichten, in dem AD FS von\-ausgestellte Ansprüche verwendet werden, erstellen Sie zunächst eine Transformations Regel für die Anspruchs Anbieter-Vertrauensstellung, und geben Sie in **eingehender Anspruchstyp**den Namen des eingehenden Anspruchs ein. Wenn Sie zuvor eine Anspruchs Beschreibung erstellt haben, wählen Sie Sie aus der Liste aus. Wählen Sie anschließend unter **Typ des ausgehenden Anspruchs**die gewünschte Anspruchs-URL aus, und erstellen Sie dann eine Transformations Regel für die Vertrauensstellung der vertrauenden Seite, um den geräteanspruch auszugeben.  
>   
> Weitere Informationen zu dynamischen Access Control Szenarien finden Sie unter [dynamische Access Control Inhalts Roadmap](../../solution-guides/dynamic-access-control--scenario-overview.md) oder [Verwenden von AD DS Ansprüchen mit AD FS](https://technet.microsoft.com/library/hh831504.aspx).  
  
7. Klicken Sie auf **Fertig stellen**.  
  
8. Klicken Sie im Dialogfeld **Anspruchs Regeln bearbeiten** auf **OK** , um die Regel zu speichern.  

## <a name="additional-references"></a>Weitere Verweise 
[Konfigurieren von Anspruchsregeln](Configure-Claim-Rules.md)  
 
[Prüfliste: Erstellen von Anspruchs Regeln für eine Vertrauensstellung der vertrauenden](https://technet.microsoft.com/library/ee913578.aspx)  

[Prüfliste: Erstellen von Anspruchs Regeln für eine Anspruchs Anbieter-Vertrauensstellung](https://technet.microsoft.com/library/ee913564.aspx)  
  
[Wann sollte eine Autorisierungs Anspruchs Regel verwendet werden?](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)  

[Rolle von Ansprüchen](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[Rolle von Anspruchsregeln](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md) 
