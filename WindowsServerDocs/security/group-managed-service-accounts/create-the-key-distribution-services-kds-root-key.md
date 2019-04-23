---
title: Erstellen des KDS-Stammschlüssels der Schlüsselverteilungsdienste
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
ms.openlocfilehash: 3d5f7b46b28e6a2fbfafb664b69aebc8d34886fe
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59867211"
---
# <a name="create-the-key-distribution-services-kds-root-key"></a>Erstellen des KDS-Stammschlüssels der Schlüsselverteilungsdienste

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

In diesem Thema für IT-Experten wird beschrieben, wie einen Stammschlüssel für den Microsoft-Schlüsselverteilungsdienst ("kdssvc.dll") auf dem Domänencontroller, die mithilfe von Windows PowerShell zum Generieren von Kennwörtern verwaltetes Dienstkonto in Windows Server 2012 zu erstellen.

 Windows Server 2012-Domänencontroller (DC) erfordern einen Stammschlüssel, Generieren von gMSA-Kennwörtern zu beginnen. Die Domänencontroller warten bis zu zehn Stunden ab der Erstellung, um allen Domänencontrollern zu ermöglichen, ihre AD-Replikation vor der Erstellung eines gMSA zu konvergieren. Bei den zehn Stunden handelt es sich um eine Sicherheitsmaßnahme, um zu verhindern, dass das Kennwort generiert wird, bevor alle Domänencontroller in der Umgebung in der Lage sind, auf gMSA-Anforderungen zu reagieren.  Wenn Sie versuchen, ein gruppenverwaltetes Dienstkonto zu verwenden, zu früh der Schlüssel kann nicht repliziert wurden, alle Windows Server 2012-Domänencontrollern und Kennwortabruf kann aus diesem Grund fehlschlagen, wenn der gMSA-Host versucht, das Kennwort abzurufen. Fehler beim gMSA-Kennwortabruf können auch auftreten, wenn Domänencontroller mit begrenzten Replikationszeitplänen verwendet werden oder wenn ein Replikationsproblem auftritt.

Sie müssen mindestens Mitglied der Gruppe **Domänen-Admins**, **Organisations-Admins** oder einer entsprechenden Gruppe sein, damit Sie dieses Verfahren ausführen können. Detaillierte Informationen zu den geeigneten Konten und Gruppenmitgliedschaften finden Sie unter [Lokale und Domänenstandardgruppen](https://technet.microsoft.com/library/dd728026(WS.10).aspx).

> [!NOTE]
> Zum Ausführen der Windows PowerShell-Befehle ist eine 64-Bit-Architektur erforderlich, die zum Verwalten von gruppenverwalteten Dienstkonten (group Managed Service Accounts, gMSA) verwendet werden.

#### <a name="to-create-the-kds-root-key-using-the-add-kdsrootkey-cmdlet"></a>Erstellen Sie den KDS-Stammschlüssel mithilfe des Cmdlets Add-KdsRootKey

1.  Führen Sie auf dem Windows Server 2012-Domänencontroller die Windows PowerShell über die Taskleiste.

2.  Geben Sie an der Befehlszeile für das Windows PowerShell Active Directory-Modul die folgenden Befehle ein, und drücken Sie die EINGABETASTE:

    **Add-KdsRootKey -EffectiveImmediately**

    > [!TIP]
    > Der Parameter „Effective time“ kann verwendet werden, um Schlüsseln vor der Verwendung die Zeit zu geben, auf alle Domänencontroller aufgefüllt zu werden. Mithilfe der Add-KdsRootKey wird – EffectiveImmediately einen Stammschlüssel zum Zieldomänencontroller hinzufügen das durch den KDS-Dienst sofort verwendet werden soll. Allerdings werden andere Windows Server 2012-Domänencontroller nicht Schlüssel des Stammzertifikats verwenden, erst nach erfolgreicher Replikation.

Für Testumgebungen mit nur einem Domänencontroller können Sie einen KDS-Stammschlüssel erstellen und die Startzeit in der Vergangenheit festlegen, um zu vermeiden, dass das Intervall auf die Schlüsselgenerierung wartet, indem folgende Vorgehensweise verwendet wird. Überprüfen Sie, ob ein 4004-Ereignis im KDS-Ereignisprotokoll protokolliert wurde.

#### <a name="to-create-the-kds-root-key-in-a-test-environment-for-immediate-effectiveness"></a>So erstellen Sie den KDS-Stammschlüssel in einer Testumgebung mit unmittelbarer Wirksamkeit

1.  Führen Sie auf dem Windows Server 2012-Domänencontroller die Windows PowerShell über die Taskleiste.

2.  Geben Sie an der Befehlszeile für das Windows PowerShell Active Directory-Modul die folgenden Befehle ein, und drücken Sie die EINGABETASTE:

    **$a=Get-Date**

    **$b=$a.AddHours(-10)**

    **Add-KdsRootKey -EffectiveTime $b**

    Oder verwenden Sie einen einzelnen Befehl:

    **Add-KdsRootKey -EffectiveTime ((get-date).addhours(-10))**

## <a name="see-also"></a>Siehe auch
[Erste Schritte mit der Gruppe von verwalteten Dienstkonten](getting-started-with-group-managed-service-accounts.md)


