---
title: "Erstellen Sie die Verteilung KDS-Stammschlüssels"
description: Windows Server-Sicherheit
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-gmsa
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 42e5db8f-1516-4d42-be0a-fa932f5588e9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 30075e56f3ca8e90a0655508efeacfcf2aaa0337
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="create-the-key-distribution-services-kds-root-key"></a>Erstellen Sie die Verteilung KDS-Stammschlüssels

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema für IT-Experten wird beschrieben, wie erstellen Sie einen Microsoft-Schlüsselverteilungsdienst (kdssvc.dll) Stammschlüssel auf dem Domänencontroller, die Verwendung von Windows PowerShell zum Generieren von Managed Service Account gruppieren. Kennwörter in Windows Server2012.

 Windows Server2012-Domänencontroller (DC) erfordern einen Stammschlüssel, damit das Generieren von gMSA-Kennwörtern gestartet. Die Domänencontroller wartet bis zu zehn Stunden ab der Erstellung, um alle Domänencontroller auf ihre AD-Replikation vor der Erstellung eines gmsa zu konvergieren zu ermöglichen. Die zehn Stunden handelt es sich um eine Sicherheitsmaßnahme, um zu verhindern, dass Kennwort Generation von generiert wird, bevor alle Domänencontroller in der Umgebung gMSA-Anforderungen beantwortet werden.  Wenn Sie versuchen, ein gMSA zu verwenden, zu früh der Schlüssel möglicherweise wurde nicht repliziert, alle Windows Server2012-Domänencontrollern und Kennwortabruf kann daher fehlschlagen, wenn der gMSA-Host versucht, das Kennwort abzurufen. Fehler bei der gMSA Kennwort abrufen können auch auftreten, wenn Domänencontroller mit begrenzten Replikationszeitplänen oder wenn ein Replikationsproblem vorliegt.

Mitgliedschaft in der **Domänen-Admins** oder **Organisations-Admins** Gruppen oder einer entsprechenden Gruppe ist mindestens erforderlich, um dieses Verfahren ausführen. Ausführliche Informationen zur Verwendung der geeigneten Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänenstandardgruppen](https://technet.microsoft.com/library/dd728026(WS.10).aspx).

> [!NOTE]
> Eine 64-Bit-Architektur ist erforderlich, um Windows PowerShell-Befehle ausführen, die zum Verwalten von Gruppenverwalteten Dienstkonten verwendet werden.

#### <a name="to-create-the-kds-root-key-using-the-new-kdsrootkey-cmdlet"></a>Erstellen Sie den KDS-Stammschlüssel mithilfe des Cmdlets New-KdsRootKey

1.  Führen Sie auf dem Windows Server2012-Domänencontroller die Windows PowerShell über die Taskleiste.

2.  Geben Sie die folgenden Befehle an der Eingabeaufforderung für das Windows PowerShell Active Directory-Modul und drücken Sie dann die EINGABETASTE:

    **Add-KdsRootKey – EffectiveImmediately**

    > [!TIP]
    > Der Effective Time-Parameter kann verwendet werden, um die Zeit für Schlüssel an alle Domänencontroller vor der Verwendung weitergegeben werden. Mithilfe von Add-KdsRootKey – EffectiveImmediately wird einen Stammschlüssel für den Zieldomänencontroller hinzufügen, durch den KDS-Dienst sofort verwendet werden. Jedoch andere Windows Server2012-Domänencontrollern nicht den Stammschlüssel verwenden, bis die Replikation erfolgreich ist.

Für Testumgebungen mit nur einem Domänencontroller können Sie einen KDS-Stammschlüssel erstellen und festlegen die Startzeit in der Vergangenheit auf die schlüsselgenerierung wartet Intervall zu vermeiden, indem Sie mithilfe des folgenden Verfahrens. Überprüfen Sie, ob ein 4004-Ereignis im Kds-Ereignisprotokoll protokolliert wurde.

#### <a name="to-create-the-kds-root-key-in-a-test-environment-for-immediate-effectiveness"></a>Erstellen Sie den KDS-Stammschlüssel in einer Testumgebung unmittelbarer Wirksamkeit

1.  Führen Sie auf dem Windows Server2012-Domänencontroller die Windows PowerShell über die Taskleiste.

2.  Geben Sie die folgenden Befehle an der Eingabeaufforderung für das Windows PowerShell Active Directory-Modul und drücken Sie dann die EINGABETASTE:

    **$ein = Get-Date**

    **$b=$a.AddHours(-10)**

    **Add-KdsRootKey – EffectiveTime $b**

    Oder verwenden Sie einen einzelnen Befehl

    **((Get-date).addhours(-10)) Add-KdsRootKey – EffectiveTime**

## <a name="see-also"></a>Siehe auch
[Erste Schrittemit Gruppe von verwalteten Dienstkonten](getting-started-with-group-managed-service-accounts.md)


