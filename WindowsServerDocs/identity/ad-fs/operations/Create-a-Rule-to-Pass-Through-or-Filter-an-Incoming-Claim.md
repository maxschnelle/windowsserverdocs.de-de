---
ms.assetid: 6127963f-71b2-4d8f-8b53-7c525bf06521
title: Erstellen einer Regel zum durchlaufen oder Filtern eines eingehenden Anspruchs
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: a72be27746e64fb38c04d30a4dcef9b009257e0a
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87967307"
---
# <a name="create-a-rule-to-pass-through-or-filter-an-incoming-claim"></a>Erstellen einer Regel zum durchlaufen oder Filtern eines eingehenden Anspruchs

Mithilfe der Regel Vorlage zum durchlaufen oder Filtern einer eingehenden Anspruchs Regel in Active Directory-Verbunddienste (AD FS) \( AD FS \) können Sie alle eingehenden Ansprüche mit einem ausgewählten Anspruchstyp weiterleiten. Außerdem können Sie die Werte der eingehenden Ansprüche mit einem bestimmten Anspruchstyp filtern. Sie können beispielswiese diese Regelvorlage verwenden, um eine Regel zu erstellen, die alle eingehenden Gruppenansprüche sendet. Sie können diese Regel auch verwenden, um nur Benutzer Prinzipal Namen- \( UPN-Ansprüche zu senden \) , die mit enden @fabrikam .

Mithilfe des folgenden Verfahrens können Sie eine Anspruchs Regel mit dem Snap-in "AD FS-Verwaltung" Erstellen \- .

Zum Ausführen dieses Verfahrens ist mindestens die Mitgliedschaft in der Gruppe **Administratoren** oder eine gleichwertige Berechtigung auf dem lokalen Computer erforderlich.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477).

## <a name="to-create-a-rule-to-pass-through-or-filter-an-incoming-claim-on-a-relying-party-trust-in-windows-server-2016"></a>So erstellen Sie eine Regel zum Weiterleiten oder Filtern eines eingehenden Anspruchs für eine Vertrauensstellung der vertrauenden Seite in Windows Server 2016

1.  Klicken Sie im Server-Manager auf **Tools**, und wählen Sie **AD FS-Verwaltung** aus.

2.  Klicken Sie in der Konsolen Struktur unter **AD FS**auf Vertrauens Stellungen der vertrauenden **Seite**.
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)

3.  \-Klicken Sie mit der rechten Maustaste auf die ausgewählte Vertrauensstellung, und klicken Sie dann auf **Richtlinie**zum
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule10.PNG)

4.  Klicken Sie im Dialogfeld **Richtlinie für Anspruchs Ausstellung bearbeiten** unter Ausstellungs **Transformationsregeln** auf **Regel hinzufügen** , um den Regel-Assistenten zu starten.
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule11.PNG)

5.  Wählen Sie auf der Seite **Regel Vorlage auswählen** unter **Anspruchs Regel Vorlage**die **Option Pass-Through oder einen eingehenden Anspruch Filtern** aus der Liste aus, und klicken Sie dann auf **weiter**.
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule4.PNG)

6.  Geben Sie auf der Seite **Regel konfigurieren** unter **Anspruchs Regel Name** den anzeigen Amen für diese Regel ein, wählen Sie unter **eingehender Anspruchstyp** einen Anspruchstyp in der Liste aus, und wählen Sie dann je nach den Anforderungen Ihrer Organisation eine der folgenden Optionen aus:

    -   **Alle Anspruchswerte weiterleiten**

    -   **Nur einen bestimmten Anspruchswert weiterleiten**

    -   **Nur Anspruchs Werte weiterleiten, die einem bestimmten e-Mail-suffixwert entsprechen**

    -   **Nur Anspruchs Werte weiterleiten, die mit einem bestimmten Wert beginnen** 
 ![ Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule5.PNG)

7.  Klicken Sie auf die Schaltfläche **Fertig stellen**.

8.  Klicken Sie im Dialogfeld **Anspruchs Regeln bearbeiten** auf **OK** , um die Regel zu speichern.

## <a name="to-create-a-rule-to-pass-through-or-filter-an-incoming-claim-on-a-claims-provider-trust-in-windows-server-2016"></a>So erstellen Sie eine Regel zum Weiterleiten oder Filtern eines eingehenden Anspruchs für eine Anspruchs Anbieter-Vertrauensstellung in Windows Server 2016

1.  Klicken Sie im Server-Manager auf **Tools**, und wählen Sie **AD FS-Verwaltung** aus.

2.  Klicken Sie in der Konsolen Struktur unter **AD FS**auf **Anspruchs Anbieter**-Vertrauens Stellungen.
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule1.PNG)

3.  \-Klicken Sie mit der rechten Maustaste auf die ausgewählte Vertrauensstellung und dann auf **Anspruchs Regeln bearbeiten**.
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule2.PNG)

4.  Klicken Sie im Dialogfeld **Anspruchs Regeln bearbeiten** unter **Akzeptanz Transformationsregeln** auf **Regel hinzufügen** , um den Regel-Assistenten zu starten.
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule3.PNG)

5.  Wählen Sie auf der Seite **Regel Vorlage auswählen** unter **Anspruchs Regel Vorlage**die **Option Pass-Through oder einen eingehenden Anspruch Filtern** aus der Liste aus, und klicken Sie dann auf **weiter**.
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule4.PNG)

6.  Geben Sie auf der Seite **Regel konfigurieren** unter **Anspruchs Regel Name** den anzeigen Amen für diese Regel ein, wählen Sie unter **eingehender Anspruchstyp** einen Anspruchstyp in der Liste aus, und wählen Sie dann je nach den Anforderungen Ihrer Organisation eine der folgenden Optionen aus:

    -   **Alle Anspruchswerte weiterleiten**

    -   **Nur einen bestimmten Anspruchswert weiterleiten**

    -   **Nur Anspruchs Werte weiterleiten, die einem bestimmten e-Mail-suffixwert entsprechen**

    -   **Nur Anspruchs Werte weiterleiten, die mit einem bestimmten Wert beginnen** 
 ![ Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule5.PNG)

7.  Klicken Sie auf die Schaltfläche **Fertig stellen**.

8.  Klicken Sie im Dialogfeld **Anspruchs Regeln bearbeiten** auf **OK** , um die Regel zu speichern.

## <a name="to-create-a-rule-to-pass-through-or-filter-an-incoming-claim-in-windows-server-2012-r2"></a>So erstellen Sie eine Regel zum Weiterleiten oder Filtern eines eingehenden Anspruchs in Windows Server 2012 R2

1.  Klicken Sie im Server-Manager auf **Tools**, und wählen Sie **AD FS-Verwaltung** aus.

2.  Klicken Sie in der Konsolen Struktur unter **AD FSAD FS \\ Vertrauens**Stellungen entweder auf **Anspruchs Anbieter** -Vertrauens Stellungen oder Vertrauens Stellungen der vertrauenden **Seite**, und klicken Sie dann auf eine bestimmte Vertrauensstellung in der Liste, in der Sie diese Regel erstellen möchten.

3.  \-Klicken Sie mit der rechten Maustaste auf die ausgewählte Vertrauensstellung und dann auf **Anspruchs Regeln bearbeiten**.
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule6.PNG)

4.  Wählen Sie im Dialogfeld **Anspruchs Regeln bearbeiten** je nach der zu bearbeitenden Vertrauensstellung und dem Regelsatz, in dem Sie diese Regel erstellen möchten, eine der folgenden Registerkarten aus, und klicken Sie dann auf **Regel hinzufügen** , um den Regel-Assistenten zu starten, der diesem Regelsatz zugeordnet ist:

    -   **Akzeptanz Transformationsregeln**

    -   **Ausstellungs Transformationsregeln**

    -   **Ausstellungs Autorisierungs Regeln**

    -   **Delegierungs Autorisierungs Regeln** 
 ![ Regel erstellen](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG)

5.  Wählen Sie auf der Seite **Regel Vorlage auswählen** unter **Anspruchs Regel Vorlage**die **Option Pass-Through oder einen eingehenden Anspruch Filtern** aus der Liste aus, und klicken Sie dann auf **weiter**.
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule7.PNG)

6.  Geben Sie auf der Seite **Regel konfigurieren** unter **Anspruchs Regel Name** den anzeigen Amen für diese Regel ein, wählen Sie unter **eingehender Anspruchstyp** einen Anspruchstyp in der Liste aus, und wählen Sie dann je nach den Anforderungen Ihrer Organisation eine der folgenden Optionen aus:

    -   **Alle Anspruchswerte weiterleiten**

    -   **Nur einen bestimmten Anspruchswert weiterleiten**

    -   **Nur Anspruchs Werte weiterleiten, die einem bestimmten e-Mail-suffixwert entsprechen**

    -   **Nur Anspruchs Werte weiterleiten, die mit einem bestimmten Wert beginnen** 
 ![ Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule8.PNG)

7.  Klicken Sie auf die Schaltfläche **Fertig stellen**.

8.  Klicken Sie im Dialogfeld **Anspruchs Regeln bearbeiten** auf **OK** , um die Regel zu speichern.




## <a name="additional-references"></a>Weitere Verweise
[Konfigurieren von Anspruchsregeln](Configure-Claim-Rules.md)

[Verwenden einer Anspruchsregel vom Typ "Weiterleiten" oder "Filtern"](../../ad-fs/technical-reference/When-to-Use-a-Pass-Through-or-Filter-Claim-Rule.md)

[Rolle von Ansprüchen](../../ad-fs/technical-reference/The-Role-of-Claims.md)

[Rolle von Anspruchsregeln](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md)

