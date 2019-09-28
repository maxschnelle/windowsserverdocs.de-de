---
ms.assetid: 8c179884-f0d9-4c7a-973d-820119cf3c38
title: Erstellen einer Regel zum Zulassen aller Benutzer
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 1356218c5f9f47073f007286e8acfdf4c3608b73
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407622"
---
# <a name="create-a-rule-to-permit-all-users"></a>Erstellen einer Regel zum Zulassen aller Benutzer

In Windows Server 2016 können Sie eine **Access Control Richtlinie** verwenden, um eine Regel zu erstellen, die allen Benutzern den Zugriff auf eine vertrauende Seite gewährt.  In Windows Server 2012 R2 können Sie mithilfe der Regel Vorlage " **alle Benutzer zulassen** " in Active Directory-Verbunddienste (AD FS) \(AD FS @ no__t-2 eine Autorisierungs Regel erstellen, die allen Benutzern den Zugriff auf die vertrauende Seite gewährt. 

Sie können zusätzliche Autorisierungs Regeln verwenden, um den Zugriff weiter einzuschränken. Benutzern, denen der Zugriff auf die vertrauende Seite über den Verbunddienst erlaubt wird, kann der Dienst durch die vertrauende Seite dennoch verweigert werden.  
  
Mithilfe der folgenden Verfahren können Sie eine Anspruchs Regel mit dem AD FS Management-Snap @ no__t-0in erstellen.  
  
Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe auf dem lokalen Computer sein, um dieses Verfahren ausführen zu können.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477). 

## <a name="to-create-a-rule-to-permit-all-users-in-windows-server-2016"></a>So erstellen Sie eine Regel zum Zulassen aller Benutzer in Windows Server 2016

1.  Klicken Sie in Server-Manager **auf Extras**, und wählen Sie dann **AD FS Verwaltung**aus.  
  
2.  Klicken Sie in der Konsolen Struktur unter **AD FS**auf Vertrauens Stellungen der vertrauenden **Seite**. 
![Regel erstellen](media/Create-a-Rule-to-Permit-All-Users/permitall1.PNG)

3.  Klicken Sie mit der rechten Maustaste auf die Vertrauensstellung der **vertrauenden Seite** , die Sie zulassen möchten, und wählen Sie **Access Control Richtlinie bearbeiten**aus.  
![Regel erstellen](media/Create-a-Rule-to-Permit-All-Users/permitall2.PNG)

4. Wählen Sie in der Zugriffs Steuerungs Richtlinie **Alle zulassen** aus, **und klicken Sie dann auf über** nehmen und **OK**.
![Regel erstellen](media/Create-a-Rule-to-Permit-All-Users/permitall3.PNG)
  
## <a name="to-create-a-rule-to-permit-all-users-in-windows-server-2012-r2"></a>So erstellen Sie eine Regel zum Zulassen aller Benutzer in Windows Server 2012 R2 
  
1.  Klicken Sie in Server-Manager **auf Extras**, und wählen Sie dann **AD FS Verwaltung**aus.  
  
2.  Klicken Sie in der Konsolen Struktur **unter\\AD FS Vertrauens\\Stellungen Vertrauens Stellungen der vertrauenden Seite**auf eine bestimmte Vertrauensstellung in der Liste, in der Sie diese Regel erstellen möchten.  

3.  Klicken\-Sie mit der rechten Maustaste auf die ausgewählte Vertrauensstellung und dann auf **Anspruchs Regeln bearbeiten**.  
![Regel erstellen](media/Create-a-Rule-to-Permit-All-Users/permitall4.PNG)  

4.  Klicken Sie im Dialogfeld **Anspruchs Regeln bearbeiten** auf die Registerkarte Ausstellungs **Autorisierungs Regeln** oder auf der Register \(Karte **Delegierungs Autorisierungs Regeln** basierend auf der\)gewünschten Autorisierungs Regel, und klicken Sie dann auf **Regel hinzufügen.** um den **Assistenten zum Hinzufügen von Autorisierungs Anspruchs Regeln**zu starten.  
![Regel erstellen](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG)  
5.  Wählen Sie auf der Seite **Regel Vorlage auswählen** unter **Anspruchs Regel Vorlage**die Option **alle Benutzer** aus der Liste zulassen aus, und klicken Sie dann auf **weiter**.  
![Regel erstellen](media/Create-a-Rule-to-Permit-All-Users/permitall6.PNG)    
6.  Klicken Sie auf der Seite **Regel konfigurieren** auf **Fertig**stellen.  
  
7.  Klicken Sie im Dialogfeld **Anspruchs Regeln bearbeiten** auf **OK** , um die Regel zu speichern.  

## <a name="additional-references"></a>Weitere Verweise 
[Konfigurieren von Anspruchsregeln](Configure-Claim-Rules.md)  
 
[Prüfliste: Erstellen von Anspruchsregeln für eine Vertrauensstellung der vertrauenden Seite](https://technet.microsoft.com/library/ee913578.aspx)  
  
[Wann sollte eine Autorisierungs Anspruchs Regel verwendet werden?](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)  

[Rolle von Ansprüchen](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[Rolle von Anspruchsregeln](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md)  
