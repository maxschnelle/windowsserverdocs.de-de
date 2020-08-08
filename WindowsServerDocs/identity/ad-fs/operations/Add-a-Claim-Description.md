---
ms.assetid: 7d230527-f4fe-4572-8838-0b354ee0b06b
title: Hinzufügen einer Anspruchsbeschreibung
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 31c04f557900cee661c2283957f590caf370bbe5
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87942734"
---
# <a name="add-a-claim-description"></a>Hinzufügen einer Anspruchsbeschreibung


In einer Konto Partnerorganisation erstellen Administratoren Ansprüche, um die Mitgliedschaft eines Benutzers in einer Gruppe oder Rolle darzustellen oder um einige Daten über einen Benutzer darzustellen, z. b. die Mitarbeiter-ID eines Benutzers.

In einer Ressourcen Partnerorganisation erstellen Administratoren entsprechende Ansprüche zur Darstellung von Gruppen und Benutzern, die als Ressourcen Benutzer erkannt werden können. Da ausgehende Ansprüche in der Konto Partnerorganisation eingehenden Ansprüchen in der Ressourcen Partnerorganisation zugeordnet werden, kann der Ressourcen Partner die Anmelde Informationen akzeptieren, die der Konto Partner bereitstellt.

Mit dem folgenden Verfahren können Sie einen Anspruch hinzufügen.

Zum Ausführen dieses Verfahrens ist mindestens die Mitgliedschaft in der Gruppe **Administratoren** oder eine gleichwertige Berechtigung auf dem lokalen Computer erforderlich.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477).

## <a name="to-add-a-claim-description"></a>So fügen Sie eine Anspruchs Beschreibung hinzu

1. Klicken Sie im Server-Manager auf **Tools**, und wählen Sie **AD FS-Verwaltung** aus.

2. Erweitern Sie **Dienst** , und klicken Sie auf der rechten Seite auf **Anspruchs Beschreibung hinzufügen**
   ![Anspruchs Beschreibung hinzufügen](media/Add-a-Claim-Description/claimdesc1.png)

3. Geben Sie im Dialogfeld "Anspruchs Beschreibung hinzufügen" unter **Anzeige Name**einen eindeutigen Namen ein, der die Gruppe oder Rolle für diesen Anspruch identifiziert.

4. Fügen Sie einen **Kurznamen**hinzu.

5. Geben Sie in **Anspruchs Bezeichner**einen URI ein, der der Gruppe oder Rolle des Anspruchs zugeordnet ist, den Sie verwenden werden.

6. Geben Sie unter **Beschreibung**den Text ein, der den Zweck dieses Anspruchs am besten beschreibt.

7. Aktivieren Sie je nach den Anforderungen Ihrer Organisation eines der folgenden Kontrollkästchen, um diesen Anspruch in Verbund Metadaten zu veröffentlichen:


~~~
- To publish this claim to make partners aware that this server can accept this claim, click **Publish this claim in federation metadata as a claim type that this Federation Service can accept**.
- To publish this claim to make partners aware that this server can issue this claim, click **Publish this claim in federation metadata as a claim type that this Federation Service can send**.
~~~

8. Klicken Sie auf **OK**.

![Anspruchs Beschreibung hinzufügen](media/Add-a-Claim-Description/claimdesc2.png)


## <a name="see-also"></a>Weitere Informationen
[AD FS-Vorgänge](../ad-fs-operations.md)
