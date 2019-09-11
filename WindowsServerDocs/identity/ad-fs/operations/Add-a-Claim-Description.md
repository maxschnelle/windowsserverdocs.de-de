---
ms.assetid: 7d230527-f4fe-4572-8838-0b354ee0b06b
title: Hinzufügen einer Anspruchsbeschreibung
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 00ae720a933289e3cd4bde5fe9d20610e38ae726
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70866038"
---
# <a name="add-a-claim-description"></a>Hinzufügen einer Anspruchsbeschreibung


In einer Konto Partnerorganisation erstellen Administratoren Ansprüche, um die Mitgliedschaft eines Benutzers in einer Gruppe oder Rolle darzustellen oder um einige Daten über einen Benutzer darzustellen, z. b. die Mitarbeiter-ID eines Benutzers.

In einer Ressourcen Partnerorganisation erstellen Administratoren entsprechende Ansprüche zur Darstellung von Gruppen und Benutzern, die als Ressourcen Benutzer erkannt werden können. Da ausgehende Ansprüche in der Konto Partnerorganisation eingehenden Ansprüchen in der Ressourcen Partnerorganisation zugeordnet werden, kann der Ressourcen Partner die Anmelde Informationen akzeptieren, die der Konto Partner bereitstellt. 

Mit dem folgenden Verfahren können Sie einen Anspruch hinzufügen.

Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe auf dem lokalen Computer sein, um dieses Verfahren ausführen zu können.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477).

## <a name="to-add-a-claim-description"></a>So fügen Sie eine Anspruchs Beschreibung hinzu

1. Klicken Sie in Server-Manager **auf Extras**, und wählen Sie dann **AD FS Verwaltung**aus. 

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


## <a name="see-also"></a>Siehe auch  
[AD FS-Vorgänge](../../ad-fs/AD-FS-2016-Operations.md) 
