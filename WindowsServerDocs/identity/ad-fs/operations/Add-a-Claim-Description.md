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
ms.openlocfilehash: 454d261aa520778a6129ac9809f53894937b036a
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66190139"
---
# <a name="add-a-claim-description"></a>Hinzufügen einer Anspruchsbeschreibung


Administratoren erstellen in einer Kontopartnerorganisation möglicherweise die Ansprüche, die zum Darstellen der Mitgliedschaft in einer Gruppe oder Rolle eines Benutzers oder zur Darstellung von Daten über einen Benutzer, z. B. eines Benutzers Mitarbeiter-ID an.

Administratoren erstellen in einer Ressourcenpartnerorganisation übernehmen die entsprechenden Ansprüche zum Darstellen von Gruppen und Benutzer, die als Ressource Benutzer erkannt werden können. Da die ausgehenden Ansprüche in der Konto-Partner Organisation Zuordnung für eingehende Ansprüche, die in der Ressourcenpartnerorganisation, den Ressourcenpartner kann die Anmeldeinformationen akzeptiert werden, die der Kontopartner bereitstellt. 

Sie können das folgende Verfahren verwenden, einen Anspruch hinzufügen.

Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe auf dem lokalen Computer sein, um dieses Verfahren ausführen zu können.  Weitere Informationen zur Verwendung der geeigneten Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477).

## <a name="to-add-a-claim-description"></a>Hinzufügen eine anspruchsbeschreibung

1. Klicken Sie im Server-Manager **Tools**, und wählen Sie dann **AD FS-Verwaltung**. 

2.  Erweitern Sie **Service** und auf der rechten Maustaste auf **Anspruchsbeschreibung hinzufügen**.
![Fügen Sie die anspruchsbeschreibung](media\Add-a-Claim-Description\claimdesc1.png)

3.  Auf dem Hinzufügen einer Anspruchsbeschreibung Dialogfeld **Anzeigenamen**, geben Sie einen eindeutigen Namen, der die Gruppe oder Rolle für dieser Anspruch identifiziert.

4.  Hinzufügen einer **kurze Namen**.

5.  In **Anspruch Bezeichner**, geben Sie einen URI, der mit der Gruppe oder Rolle des Anspruchs, die Sie verwenden möchten, zugeordnet ist.

6.  Klicken Sie unter **Beschreibung**, geben Sie Text ein, die den Zweck dieses Anspruchs am besten beschreibt.

7.  Je nach den Anforderungen Ihrer Organisation wählen Sie eines der folgenden Kontrollkästchen nach Bedarf, um diesen Anspruch in Verbundmetadaten veröffentlicht:


    - Um diesen Anspruch zu Partnern Beachten Sie, dass dieser Server dieser Anspruch akzeptieren kann zu veröffentlichen, klicken Sie auf **diesen Anspruch in Verbundmetadaten als Anspruchstyp, der diesem Verbunddienst akzeptiert veröffentlichen**.
    - Um diesen Anspruch zu Partnern Beachten Sie, dass dieser Server dieser Anspruch ausstellen kann zu veröffentlichen, klicken Sie auf **diesen Anspruch in Verbundmetadaten als Anspruchstyp, der diesem Verbunddienst gesendet werden können veröffentlichen**.

8.  Klicken Sie auf **OK**.

![Fügen Sie die anspruchsbeschreibung](media\Add-a-Claim-Description\claimdesc2.png)

  
## <a name="see-also"></a>Siehe auch  
[AD FS-Vorgänge](../../ad-fs/AD-FS-2016-Operations.md) 
