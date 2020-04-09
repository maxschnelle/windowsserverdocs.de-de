---
title: Erstellen des KDS-Stammschlüssels der Schlüsselverteilungsdienste
description: Windows Server-Sicherheit
ms.prod: windows-server
ms.technology: security-gmsa
ms.topic: article
ms.assetid: 42e5db8f-1516-4d42-be0a-fa932f5588e9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: d26cd32f021e8b00c6c9c6d3949a00f71096a3c9
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857013"
---
# <a name="create-the-key-distribution-services-kds-root-key"></a>Erstellen des KDS-Stammschlüssels der Schlüsselverteilungsdienste

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

In diesem Thema für IT-Experten wird beschrieben, wie ein Microsoft-Schlüssel Verteilungsdienst-Stamm Schlüssel (kdssvc. dll) auf dem Domänen Controller mithilfe von Windows PowerShell zum Generieren von Kenn Wörtern für Gruppen verwaltete Dienst Konten in Windows Server 2012 oder höher erstellt wird.

Domänen Controller erfordern einen Stamm Schlüssel, um mit dem Erstellen von GMSA-Kenn Wörtern zu beginnen. Die Domänencontroller warten bis zu zehn Stunden ab der Erstellung, um allen Domänencontrollern zu ermöglichen, ihre AD-Replikation vor der Erstellung eines gMSA zu konvergieren. Bei den zehn Stunden handelt es sich um eine Sicherheitsmaßnahme, um zu verhindern, dass das Kennwort generiert wird, bevor alle Domänencontroller in der Umgebung in der Lage sind, auf gMSA-Anforderungen zu reagieren.  Wenn Sie zu früh versuchen, ein GMSA zu verwenden, wurde der Schlüssel möglicherweise nicht auf allen Domänen Controllern repliziert. Daher kann das Abrufen des Kennworts fehlschlagen, wenn der GMSA-Host versucht, das Kennwort abzurufen. Fehler beim gMSA-Kennwortabruf können auch auftreten, wenn Domänencontroller mit begrenzten Replikationszeitplänen verwendet werden oder wenn ein Replikationsproblem auftritt.

> [!NOTE]
> Das Löschen und erneute Erstellen des Stamm Schlüssels kann zu Problemen führen, bei denen der alte Schlüssel nach dem Löschen weiterhin verwendet wird, da der Schlüssel zwischengespeichert wird. Der Schlüssel Verteilungsdienst (Key Distribution Service, KDC) sollte auf allen Domänen Controllern neu gestartet werden, wenn der Stamm Schlüssel neu erstellt wird.

Sie müssen mindestens Mitglied der Gruppe **Domänen-Admins**, **Organisations-Admins** oder einer entsprechenden Gruppe sein, damit Sie dieses Verfahren ausführen können. Detaillierte Informationen zu den geeigneten Konten und Gruppenmitgliedschaften finden Sie unter [Lokale und Domänenstandardgruppen](https://technet.microsoft.com/library/dd728026(WS.10).aspx).

> [!NOTE]
> Zum Ausführen der Windows PowerShell-Befehle ist eine 64-Bit-Architektur erforderlich, die zum Verwalten von gruppenverwalteten Dienstkonten (group Managed Service Accounts, gMSA) verwendet werden.

#### <a name="to-create-the-kds-root-key-using-the-add-kdsrootkey-cmdlet"></a>So erstellen Sie den KDS-Stamm Schlüssel mithilfe des Cmdlets "Add-kdsrootkey"

1.  Führen Sie auf dem Domänen Controller Windows Server 2012 oder höher Windows PowerShell über die Taskleiste aus.

2.  Geben Sie an der Befehlszeile für das Windows PowerShell Active Directory-Modul die folgenden Befehle ein, und drücken Sie die EINGABETASTE:

    **Add-kdsrootkey-effectiveimmediately**

    > [!TIP]
    > Der Parameter „Effective time“ kann verwendet werden, um Schlüsseln vor der Verwendung die Zeit zu geben, auf alle Domänencontroller aufgefüllt zu werden. Durch die Verwendung von "Add-kdsrootkey-effectiveimmediately" wird ein Stamm Schlüssel zum Zieldomänen Controller hinzugefügt, der sofort vom KDS-Dienst verwendet wird. Andere Domänen Controller können den Stamm Schlüssel jedoch erst verwenden, wenn die Replikation erfolgreich war.

Für Testumgebungen mit nur einem Domänencontroller können Sie einen KDS-Stammschlüssel erstellen und die Startzeit in der Vergangenheit festlegen, um zu vermeiden, dass das Intervall auf die Schlüsselgenerierung wartet, indem folgende Vorgehensweise verwendet wird. Überprüfen Sie, ob ein 4004-Ereignis im KDS-Ereignisprotokoll protokolliert wurde.

#### <a name="to-create-the-kds-root-key-in-a-test-environment-for-immediate-effectiveness"></a>So erstellen Sie den KDS-Stammschlüssel in einer Testumgebung mit unmittelbarer Wirksamkeit

1.  Führen Sie auf dem Domänen Controller Windows Server 2012 oder höher Windows PowerShell über die Taskleiste aus.

2.  Geben Sie an der Befehlszeile für das Windows PowerShell Active Directory-Modul die folgenden Befehle ein, und drücken Sie die EINGABETASTE:

    **$a = Get-Date**

    **$b = $a. AddHours (-10)**

    **Add-kdsrootkey-effectivetime-$b**

    Oder verwenden Sie einen einzelnen Befehl:

    **Add-kdsrootkey-effectivetime ((Get-Date). AddHours (-10))**

## <a name="see-also"></a>Weitere Informationen
[Erste Schritte mit gruppenverwalteten Dienstkonten](getting-started-with-group-managed-service-accounts.md)


