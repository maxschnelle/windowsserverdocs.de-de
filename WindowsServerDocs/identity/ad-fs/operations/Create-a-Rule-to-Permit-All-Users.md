---
ms.assetid: 8c179884-f0d9-4c7a-973d-820119cf3c38
title: Erstellen einer Regel zum Zulassen aller Benutzer
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 6fa3500cc0343a7c341b2e94b011ce69f6bfbc04
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87967247"
---
# <a name="create-a-rule-to-permit-all-users"></a>Erstellen einer Regel zum Zulassen aller Benutzer

In Windows Server 2016 können Sie eine **Access Control Richtlinie** verwenden, um eine Regel zu erstellen, die allen Benutzern den Zugriff auf eine vertrauende Seite gewährt.  In Windows Server 2012 R2 können Sie mithilfe der Regel Vorlage " **alle Benutzer zulassen** " in Active Directory-Verbunddienste (AD FS) \( AD FS \) eine Autorisierungs Regel erstellen, die allen Benutzern den Zugriff auf die vertrauende Seite gewährt.

Sie können zusätzliche Autorisierungs Regeln verwenden, um den Zugriff weiter einzuschränken. Benutzern, denen der Zugriff auf die vertrauende Seite über den Verbunddienst erlaubt wird, kann der Dienst durch die vertrauende Seite dennoch verweigert werden.

Mithilfe der folgenden Verfahren können Sie eine Anspruchs Regel mit dem Snap-in "AD FS-Verwaltung" Erstellen \- .

Zum Ausführen dieses Verfahrens ist mindestens die Mitgliedschaft in der Gruppe **Administratoren** oder eine gleichwertige Berechtigung auf dem lokalen Computer erforderlich.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477).

## <a name="to-create-a-rule-to-permit-all-users-in-windows-server-2016"></a>So erstellen Sie eine Regel zum Zulassen aller Benutzer in Windows Server 2016

1.  Klicken Sie im Server-Manager auf **Tools**, und wählen Sie **AD FS-Verwaltung** aus.

2.  Klicken Sie in der Konsolen Struktur unter **AD FS**auf Vertrauens Stellungen der vertrauenden **Seite**.
![Regel erstellen](media/Create-a-Rule-to-Permit-All-Users/permitall1.PNG)

3.  Klicken Sie mit der rechten Maustaste auf die Vertrauensstellung der **vertrauenden Seite** , die Sie zulassen möchten, und wählen Sie **Access Control Richtlinie bearbeiten**aus.
![Regel erstellen](media/Create-a-Rule-to-Permit-All-Users/permitall2.PNG)

4. Wählen Sie in der Zugriffs Steuerungs Richtlinie **Alle zulassen** aus, **und klicken Sie dann auf über** nehmen und **OK**.
![Regel erstellen](media/Create-a-Rule-to-Permit-All-Users/permitall3.PNG)

## <a name="to-create-a-rule-to-permit-all-users-in-windows-server-2012-r2"></a>So erstellen Sie eine Regel zum Zulassen aller Benutzer in Windows Server 2012 R2

1.  Klicken Sie im Server-Manager auf **Tools**, und wählen Sie **AD FS-Verwaltung** aus.

2.  Klicken Sie in der Konsolen Struktur unter **AD FS Vertrauens Stellungen Vertrauens Stellungen der \\ vertrauenden \\ Seite**auf eine bestimmte Vertrauensstellung in der Liste, in der Sie diese Regel erstellen möchten.

3.  \-Klicken Sie mit der rechten Maustaste auf die ausgewählte Vertrauensstellung und dann auf **Anspruchs Regeln bearbeiten**.
![Regel erstellen](media/Create-a-Rule-to-Permit-All-Users/permitall4.PNG)

4.  Klicken Sie im Dialogfeld **Anspruchs Regeln bearbeiten** auf die Registerkarte Ausstellungs **Autorisierungs Regeln** oder auf der Registerkarte **Delegierungs Autorisierungs Regeln** \( basierend auf der gewünschten Autorisierungs Regel \) . Klicken Sie anschließend auf **Regel hinzufügen** , um den **Assistenten zum Hinzufügen von Autorisierungs Anspruchs**Regeln zu starten.
![Regel erstellen](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG)
5.  Wählen Sie auf der Seite **Regel Vorlage auswählen** unter **Anspruchs Regel Vorlage**die Option **alle Benutzer** aus der Liste zulassen aus, und klicken Sie dann auf **weiter**.
![Regel erstellen](media/Create-a-Rule-to-Permit-All-Users/permitall6.PNG)
6.  Klicken Sie auf der Seite **Regel konfigurieren** auf **Fertig**stellen.

7.  Klicken Sie im Dialogfeld **Anspruchs Regeln bearbeiten** auf **OK** , um die Regel zu speichern.

## <a name="additional-references"></a>Weitere Verweise
[Konfigurieren von Anspruchsregeln](Configure-Claim-Rules.md)

[Prüfliste: Erstellen von Anspruchsregeln für eine Vertrauensstellung der vertrauenden Seite](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/ee913578(v=ws.11))

[Wann sollte eine Autorisierungsanspruchsregel verwendet werden](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)

[Rolle von Ansprüchen](../../ad-fs/technical-reference/The-Role-of-Claims.md)

[Rolle von Anspruchsregeln](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md)
