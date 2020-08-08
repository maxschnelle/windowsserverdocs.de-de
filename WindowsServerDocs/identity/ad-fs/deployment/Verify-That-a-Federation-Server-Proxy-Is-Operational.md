---
ms.assetid: d555041a-709e-42c7-920a-8dfd2c7e0488
title: Überprüfen der Betriebsbereitschaft eines Verbundserverproxys
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.author: billmath
ms.openlocfilehash: 4550934c56b4406ea7aff9b90509a205014dd95d
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87940959"
---
# <a name="verify-that-a-federation-server-proxy-is-operational"></a>Überprüfen der Betriebsbereitschaft eines Verbundserverproxys


Mithilfe des folgenden Verfahrens können Sie überprüfen, ob der Verbund Server Proxy mit dem Verbunddienst in Active Directory-Verbunddienste (AD FS) AD FS kommunizieren kann \( \) . Sie führen dieses Verfahren aus, nachdem Sie den Assistenten zum Konfigurieren von **AD FS Verbund Server Proxy** ausgeführt haben, um den Computer für die Ausführung in der Verbund Server Proxy-Rolle zu konfigurieren. Weitere Informationen zum Ausführen dieses Assistenten finden Sie unter [Konfigurieren eines Computers für die Verbund Server Proxy-Rolle](Configure-a-Computer-for-the-Federation-Server-Proxy-Role.md).

> [!IMPORTANT]
> Das Ergebnis dieses Tests besteht im erfolgreichen Generieren eines bestimmten Ereignisses in der Ereignisanzeige auf dem Verbundserverproxy-Computer.

Zum Ausführen dieses Verfahrens ist mindestens die Mitgliedschaft in der Gruppe **Administratoren** oder eine gleichwertige Berechtigung auf dem lokalen Computer erforderlich.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477).

### <a name="to-verify-that-a-federation-server-proxy-is-operational"></a>So überprüfen Sie die Funktionstüchtigkeit eines Verbund Server Proxys

1.  Melden Sie sich beim Verbund Server Proxy als Administrator an.

2.  Geben Sie auf dem **Start** Bildschirm**Ereignisanzeige**ein, und drücken Sie dann die EINGABETASTE.

3.  Doppel \- Klicken Sie im Detailbereich auf **Anwendungs-und Dienst Protokolle**, Doppel \- Klicken Sie auf **AD FS**Ereignis, und klicken Sie dann auf **Admin**.

4.  Suchen Sie in der Spalte **Ereignis-ID** nach der Ereignis-ID 198.

    Wenn der Verbund Server Proxy ordnungsgemäß konfiguriert ist, wird im Anwendungsprotokoll Ereignisanzeige ein neues Ereignis mit der Ereignis-ID 198 angezeigt. Dieses Ereignis überprüft, ob der Verbund Server Proxy-Dienst erfolgreich gestartet wurde und nun online ist.

## <a name="additional-references"></a>Weitere Verweise
[Prüfliste: Einrichten eines Verbundserverproxys](Checklist--Setting-Up-a-Federation-Server-Proxy.md)


