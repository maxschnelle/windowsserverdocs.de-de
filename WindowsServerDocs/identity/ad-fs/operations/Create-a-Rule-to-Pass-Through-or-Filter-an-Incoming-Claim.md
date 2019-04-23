---
ms.assetid: 6127963f-71b2-4d8f-8b53-7c525bf06521
title: Erstellen Sie eine Regel zum Pass-Through oder Filtern eines eingehenden Anspruchs
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 50f50cd4e096b107a2b58ac05328ff8ed413f2dc
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59860271"
---
# <a name="create-a-rule-to-pass-through-or-filter-an-incoming-claim"></a>Erstellen Sie eine Regel zum Pass-Through oder Filtern eines eingehenden Anspruchs

>Gilt für: Windows Server 2016, Windows Server 2012 R2

Verwenden Sie die Pass-Through oder Filtern von einer Vorlage des eingehenden Anspruchs-Regel in Active Directory Federation Services \(AD FS\), können Sie alle eingehenden Ansprüche mit einem ausgewählten Anspruchstyp durchlaufen. Sie können auch die Werte der eingehenden Ansprüche mit einem ausgewählten Anspruchstyp filtern. Beispielsweise können Sie diese Regelvorlage zum Erstellen einer Regel, die alle eingehenden Gruppenansprüche sendet. Sie können auch diese Regel nur Benutzerprinzipalname senden \(UPN\) Ansprüche, die mit @fabrikam.  
  
Sie können das folgende Verfahren zum Erstellen einer Anspruchsregel mit der AD FS-Verwaltungs-Snap\-in.  
  
Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe auf dem lokalen Computer sein, um dieses Verfahren ausführen zu können.  Weitere Informationen zur Verwendung der geeigneten Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   

## <a name="to-create-a-rule-to-pass-through-or-filter-an-incoming-claim-on-a-relying-party-trust-in-windows-server-2016"></a>Erstellen Sie eine Regel, um die pass-through oder Filtern eines eingehenden Anspruchs auf a Relying Party Trust in Windows Server 2016 

1.  Klicken Sie im Server-Manager **Tools**, und wählen Sie dann **AD FS-Verwaltung**.  
  
2.  In der Konsolenstruktur unter **AD FS**, klicken Sie auf **Vertrauensstellungen für vertrauende Seiten**. 
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)  
  
3.  Rechts\-klicken Sie auf der ausgewählten Vertrauensstellung, und klicken Sie dann auf **Anspruchsausstellungsrichtlinie bearbeiten**.
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule10.PNG)   
  
4.  In der **Anspruchsausstellungsrichtlinie bearbeiten** Dialogfeld **Ausstellungstransformationsregeln** klicken Sie auf **Regel hinzufügen** um die Regel-Assistenten zu starten. 
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule11.PNG)    

5.  Auf der **Regelvorlage auswählen** Seite **anspruchsregelvorlage**Option **Pass-Through oder Filtern eines eingehenden Anspruchs** aus der Liste aus, und klicken Sie dann auf **weiter** .  
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule4.PNG)    

6.  Auf der **Regel konfigurieren** Seite **anspruchsregelname** Geben Sie den Anzeigenamen für diese Regel in **eingehender Anspruchstyp** wählen Sie einen Anspruchstyp aus der Liste aus, und wählen Sie dann eine der folgende Möglichkeiten, je nach den Anforderungen Ihrer Organisation:  
  
    -   **Alle Anspruchswerte weiterleiten**  
  
    -   **Pass-through-nur einen bestimmten Anspruchswert**  
  
    -   **Pass-through-nur Anspruchswerte, die einem bestimmten e-Mail-Suffixwert entsprechen**  
  
    -   **Pass-through-nur Anspruchswerte durchalufen, die mit einem bestimmten Wert beginnen.**  
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule5.PNG)    

7.  Klicken Sie auf die **Fertig stellen** Schaltfläche.  
  
8.  In der **Edit Claim Rules** Dialogfeld klicken Sie auf **OK** um die Regel zu speichern.
  
## <a name="to-create-a-rule-to-pass-through-or-filter-an-incoming-claim-on-a-claims-provider-trust-in-windows-server-2016"></a>Erstellen Sie eine Regel, um die pass-through oder Filtern eines eingehenden Anspruchs auf eine Anspruchsanbieter-Vertrauensstellung in Windows Server 2016 
  
1.  Klicken Sie im Server-Manager **Tools**, und wählen Sie dann **AD FS-Verwaltung**.  
  
2.  In der Konsolenstruktur unter **AD FS**, klicken Sie auf **Anspruchsanbieter-Vertrauensstellungen**. 
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule1.PNG)  
  
3.  Rechts\-klicken Sie auf der ausgewählten Vertrauensstellung, und klicken Sie dann auf **Edit Claim Rules**.
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule2.PNG)   
  
4.  In der **Edit Claim Rules** Dialogfeld **Akzeptanztransformationsregeln** klicken Sie auf **Regel hinzufügen** um die Regel-Assistenten zu starten.
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule3.PNG)    

5.  Auf der **Regelvorlage auswählen** Seite **anspruchsregelvorlage**Option **Pass-Through oder Filtern eines eingehenden Anspruchs** aus der Liste aus, und klicken Sie dann auf **weiter** .  
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule4.PNG)    

6.  Auf der **Regel konfigurieren** Seite **anspruchsregelname** Geben Sie den Anzeigenamen für diese Regel in **eingehender Anspruchstyp** wählen Sie einen Anspruchstyp aus der Liste aus, und wählen Sie dann eine der folgende Möglichkeiten, je nach den Anforderungen Ihrer Organisation:  
  
    -   **Alle Anspruchswerte weiterleiten**  
  
    -   **Pass-through-nur einen bestimmten Anspruchswert**  
  
    -   **Pass-through-nur Anspruchswerte, die einem bestimmten e-Mail-Suffixwert entsprechen**  
  
    -   **Pass-through-nur Anspruchswerte durchalufen, die mit einem bestimmten Wert beginnen.**  
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule5.PNG)    

7.  Klicken Sie auf die **Fertig stellen** Schaltfläche.  
  
8.  In der **Edit Claim Rules** Dialogfeld klicken Sie auf **OK** um die Regel zu speichern.  

## <a name="to-create-a-rule-to-pass-through-or-filter-an-incoming-claim-in-windows-server-2012-r2"></a>Erstellen Sie eine Regel, um die pass-through oder Filtern eines eingehenden Anspruchs in Windows Server 2012 R2

1.  Klicken Sie im Server-Manager **Tools**, und wählen Sie dann **AD FS-Verwaltung**.  
  
2.  In der Konsolenstruktur unter **FSAD für AD FS\\Vertrauensstellungen**, klicken Sie auf **Anspruchsanbieter-Vertrauensstellungen** oder **Vertrauensstellungen für vertrauende Seiten**, und klicken Sie dann auf eine bestimmte Vertrauensstellung in der Liste, die zum Erstellen dieser Regel werden sollen.  
  
3.  Rechts\-klicken Sie auf der ausgewählten Vertrauensstellung, und klicken Sie dann auf **Edit Claim Rules**.
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule6.PNG)   
  
4.  In der **Edit Claim Rules** im Dialogfeld Wählen Sie eine der folgenden Registerkarten, abhängig von der Vertrauensstellung, die Sie bearbeiten und welche Regel legen Sie, diese Regel in erstellen möchten, und klicken Sie dann auf **Regel hinzufügen** zum Starten des Regel-Assistenten Das ist mit diesem Regelsatz verknüpft:  
  
    -   **Akzeptanztransformationsregeln**  
  
    -   **Ausstellungstransformationsregeln**  
  
    -   **Ausstellungsautorisierungsregeln**  
  
    -   **Autorisierungsregeln**  
![Regel erstellen](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG)    

5.  Auf der **Regelvorlage auswählen** Seite **anspruchsregelvorlage**Option **Pass-Through oder Filtern eines eingehenden Anspruchs** aus der Liste aus, und klicken Sie dann auf **weiter** .  
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule7.PNG)    

6.  Auf der **Regel konfigurieren** Seite **anspruchsregelname** Geben Sie den Anzeigenamen für diese Regel in **eingehender Anspruchstyp** wählen Sie einen Anspruchstyp aus der Liste aus, und wählen Sie dann eine der folgende Möglichkeiten, je nach den Anforderungen Ihrer Organisation:  
  
    -   **Alle Anspruchswerte weiterleiten**  
  
    -   **Pass-through-nur einen bestimmten Anspruchswert**  
  
    -   **Pass-through-nur Anspruchswerte, die einem bestimmten e-Mail-Suffixwert entsprechen**  
  
    -   **Pass-through-nur Anspruchswerte durchalufen, die mit einem bestimmten Wert beginnen.**  
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule8.PNG)    

7.  Klicken Sie auf die **Fertig stellen** Schaltfläche.  
  
8.  In der **Edit Claim Rules** Dialogfeld klicken Sie auf **OK** um die Regel zu speichern.  



  
## <a name="additional-references"></a>Weitere Verweise  
[Konfigurieren von Anspruchsregeln](Configure-Claim-Rules.md)  
  
[Verwendung von Pass-Through or Filter Claim Rule](../../ad-fs/technical-reference/When-to-Use-a-Pass-Through-or-Filter-Claim-Rule.md)  
  
[Die Rolle von Ansprüchen](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[Die Rolle von Anspruchsregeln](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md)  
  
