---
ms.assetid: 7d230527-f4fe-4572-8838-0b354ee0b06b
title: "Hinzufügen einer Anspruchsbeschreibung"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 0e388ef656d3b690da62b077cb9f9e678a771e64
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="add-a-claim-description"></a>Hinzufügen einer Anspruchsbeschreibung

>Gilt für: Windows Server 2016, Windows Server2012 R2

In einer Kontopartnerorganisation erstellen Administratoren Ansprüche zum Darstellen der Mitgliedschaft in einer Gruppe oder die Rolle eines Benutzers oder zum Darstellen von Daten über einen Benutzer, z.B. eines Benutzers Mitarbeiter ID-Nummer.

In einer Ressourcenpartnerorganisation erstellen Administratoren entsprechende Ansprüche zum Darstellen von Gruppen und Benutzer, die als Ressource Benutzer erkannt werden können. Da ausgehende im Konto Partner Organisation zuordnen eingehenden Ansprüche in der Ressourcenpartnerorganisation Ressourcenpartner Ansprüche nimmt die Anmeldeinformationen an, die der Kontopartner bereitstellt. 

Das folgende Verfahren können einen Anspruch hinzu.

Mitgliedschaft in **Administratoren**, oder eine entsprechende Berechtigung auf dem lokalen Computer mindestens erforderlich, um dieses Verfahren ausführen.  Weitere Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477).

## <a name="to-add-a-claim-description"></a>Hinzufügen eine anspruchsbeschreibung

1. Klicken Sie im Server-Manager auf **Tools**, und wählen Sie dann **AD FS-Verwaltungs**. 

2.  Erweitern Sie **Service** und auf der rechten Maustaste auf **Anspruchsbeschreibung hinzufügen**.
![Hinzufügen von anspruchsbeschreibung](media\Add-a-Claim-Description\claimdesc1.png)

3.  Hinzufügen einer Anspruchsbeschreibung Dialogfeld **Anzeigenamen**, geben Sie einen eindeutigen Namen, der die Gruppe oder die Rolle für diesen Anspruch identifiziert.

4.  Hinzufügen einer **kurzen Namen**.

5.  In **Anspruch Bezeichner**, geben Sie einen URI, der die Gruppe oder die Rolle des Anspruchs, die Sie verwenden zugeordnet ist.

6.  Klicken Sie unter **Beschreibung**, geben Sie Text, der den Zweck dieses Anspruchs am besten beschreibt.

7.  Je nach den Anforderungen Ihrer Organisation wählen Sie eine der folgenden Kontrollkästchen nach Bedarf, um diesen Anspruch in Verbundmetadaten veröffentlicht:


    - Um diesen Anspruch Partner fähig werden, dass dieser Server diesen Anspruch akzeptieren kann zu veröffentlichen, klicken Sie auf **diesen Anspruch in Verbundmetadaten als Anspruchstyp, die diesem Verbunddienst akzeptiert veröffentlichen**.
    - Um diesen Anspruch Partner fähig werden, dass dieser Server diesen Anspruch ausstellen kann zu veröffentlichen, klicken Sie auf **diesen Anspruch in Verbundmetadaten als Anspruchstyp, die diesem Verbunddienst senden können veröffentlichen**.

8.  Klicken Sie auf **OK**.

![Hinzufügen von anspruchsbeschreibung](media\Add-a-Claim-Description\claimdesc2.png)

  
## <a name="see-also"></a>Siehe auch  
[AD FS-Vorgänge](../../ad-fs/AD-FS-2016-Operations.md) 
