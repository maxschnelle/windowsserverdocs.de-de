---
title: Einführung in Windows Server, Version 1709
description: So erhalten und installieren Sie
ms.prod: windows-server-threshold
ms.mktglfcycl: manage
ms.sitesec: library
author: jaimeo
ms.localizationpriority: high
ms.date: 12/5/2017
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9cf87597-b15d-4f43-8aa1-91e60367f011
ms.openlocfilehash: 96f098457b9bac4541421c7889aefb030e3d8804
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59868801"
---
# <a name="introducing-windows-server-version-1709"></a>Einführung in Windows Server, Version 1709

>Gilt für: Windows Server (Semi-Annual Channel)

**Windows Server-Version 1709 ist der ersten Version in den neuen Halbjährlicher Kanal.** 

## <a name="what-the-semi-annual-channel-is--and-isnt"></a>Was ist der Semi-Annual Channel und was nicht
Als erste Version in diesem neuen Kanal ist Windows Server der Version 1709 *kein* „Update” oder „Service Pack” für Windows Server 2016. Es handelt sich um die erste halbjährliche Freigabe auf einem **neuen Kanal** für Kunden und Hoster, die mit der Geschwindigkeit der Entwicklungslebenszyklen oder den neuesten Hyper-V-Investitionen Schritt halten müssen. Jede Version in diesen Kanal wird ab der ersten Veröffentlichung 18 Monate lang unterstützt. Weitere Informationen zum Semi-Annual Channel sowie **Tipps für die Entscheidung, welchen Kanal Sie wählen sollten**, finden Sie unter [Übersicht über den Semi-Annual Channel](semi-annual-channel-overview.md).


**Das aktuelle Produkt im Long-Term Servicing Channel (LTSC) ist Windows Server 2016.** Der LTSC empfiehlt sich, wenn Sie langfristige Stabilität und Vorhersagbarkeit im Server-Betriebssystem zur Unterstützung von herkömmlichen Arbeitslasten und Anwendungen benötigen. Wenn Sie weiterhin den LTSC verwenden möchten, sollten Sie Windows Server 2016 installieren (oder weiterhin nutzen), da dieses Produkt im Server Core-Modus oder im Server with Desktop Experience-Modus installiert werden kann. Weitere Details finden Sie unter [Erste Schritte mit Windows Server 2016](https://docs.microsoft.com/windows-server/get-started/server-basics).


## <a name="whats-different-about-1709"></a>Unterschiede bei 1709.

Windows Server der Version 1709 wird im Server Core-Modus ausgeführt. Das bedeutet, dass es keine grafische Benutzeroberfläche gibt, sodass Sie das Produkt remote verwalten müssen. Es bietet jedoch große Vorteile, z. B. kleinere Hardwareanforderungen, weit weniger Angriffsfläche und weniger notwendige Updates. Wenn Sie noch keine Erfahrung mit Server Core haben, hilft Ihnen [Verwalten eines Servers im Server-Core-Modus](../administration/server-core/server-core-manage.md), um sich in der Umgebung zurecht zu finden. [Verwalten von Windows Server 2016](../administration/manage-windows-server.md) zeigt die verschiedenen Optionen für die Remoteverwaltung von Servern.

[Neuigkeiten in Windows Server, Version 1709](whats-new-in-windows-server-1709.md) führt Sie in die neuen Features und Funktionen von Windows Server, Version 1709 ein.

### <a name="why-does-windows-server-version-1709-offer-only-the-server-core-installation-option"></a>Warum bietet die Version 1709 von Windows Server nur die Server Core-Installationsoption?
Eine der wichtigsten Schritte bei der Planung jeder Version von Windows Server ist das Kundenfeedback – wie verwenden Sie Windows Server? Welche neuen Features haben die größte Auswirkung auf die Windows Server-Bereitstellungen und ebenfalls auf Ihren täglichen Einsatz? Ihr Feedback zeigt uns, dass die Bereitstellung neuer Innovationen so schnell und effizient wie möglich ein Hauptanliegen ist. Kunden, die gleichzeitig die Innovationen schnell einführen haben uns mitgeteilt, dass sie in erster Linie Befehlszeilen mit PowerShell-Skripting für die Verwaltung der Rechenzentren verwenden und daher nicht unbedingt eine Desktop-GUI für Windows Server im Modus „Desktopdarstellung“ installieren müssen. Durch den Fokus auf die Server Core-Installationsoption können wir diese Innovationen durch weitere Ressourcen gleichzeitig für herkömmliche Windows Server-Plattform-Funktionen und Anwendungskompatibilität entwickeln. Wenn Sie Feedback zu diesem oder anderen Problemen im Zusammenhang mit Windows Server und unseren zukünftigen Versionen haben, können Sie Vorschläge machen und Kommentare über den [Feedback-Hub](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app) abgeben.


### <a name="what-about-nano-server"></a>Was ist mit Nano Server?
Nano Server ist als Containerbetriebssystem verfügbar. Weitere Details finden Sie unter [Changes to Nano Server in Windows Server Semi-Annual Channel](nano-in-semi-annual-channel.md).

## <a name="additional-information-about-this-release"></a>Zusätzliche Informationen zu dieser Version
Um einen umfassenden Überblick über die wichtigsten Fakten der Windows-Server Version 1709 zu erhalten, sollten Sie auch diese Themen vor der Installation durchlesen:

- Welche Hardware ist für die Ausführung erforderlich? Weitere Informationen finden Sie unter [Systemanforderungen](system-requirements.md). Die Systemanforderungen für diese Version sind identisch mit denen für Windows Server 2016.
- Welche neuen Features und Funktionen wurden hinzugefügt? Informationen hierzu finden Sie unter [Neues in IPAM unter Windows Server Version 1709](whats-new-in-windows-server-1709.md).
- Was wurde entfernt? Weitere Informationen finden Sie unter [In Windows Server (Version 1709) entfernte oder veraltete Features](Removed-Features-1709.md)
- Was speziellen Probleme dieser Version müssen umgangen werden? Siehe [Anmerkungen zu dieser Version – Wichtige Probleme in Windows Server, Version 1709](server-1709-relnotes.md)


## <a name="where-to-obtain-windows-server-version-1709"></a>Beziehen von Windows Server, Version 1709

Diese Versionen müssen als Neuinstallation installiert werden.

- VLSC: Kunden mit Volumenlizenzierung lizenzierten [Software Assurance](https://www.microsoft.com/en-us/licensing/licensing-programs/software-assurance-default.aspx) können diese Version abrufen, indem Sie auf die [Volume Licensing Service Center](https://www.microsoft.com/Licensing/servicecenter/default.aspx) und auf **Anmeldung**. Klicken Sie dann auf **Downloads und SchlüsselKeys** und suchen Sie nach dieser Version. 

- Windows Server der Version 1709 ist auch in [Microsoft Azure](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.WindowsServer?tab=Overview) verfügbar.

- Teilnehmer **Visual Studio-Abonnements:** Wenn Sie bereits Visual Studio-Abonnements teilnehmen, erhalten Sie Windows Server, Version 1709, indem Sie auf die [Downloadseite für Visual Studio-Abonnent](https://my.visualstudio.com/downloads?pid=2347) und Abschließen von gibt es den Download zur Verfügung. Wenn Sie nicht bereits ein Abonnent sind, wechseln Sie zu [Visual Studio Subscriptions](https://www.visualstudio.com/subscriptions/), um sich anzumelden, und besuchen Sie anschließend die [Seite zum Herunterladen von Visual Studio-Abonnenten](https://my.visualstudio.com/downloads?pid=2347) wie oben beschrieben. Versionen, die über Visual Studio Subscriptions bereitgestellt werden, dienen nur zur Entwicklung und zum Testen.




## <a name="activating-windows-server-version-1709"></a>Aktivieren von Windows Server, Version 1709

- Wenn Sie diese Version aus dem Volume Licensing Service Center abgerufen haben, können Sie sie mithilfe des Windows Server 2016-Aktivierungsschlüssels aktivieren.
- Wenn Sie Microsoft Azure verwenden, sollte diese Version automatisch aktiviert werden.
- Wenn Sie diese Version über Visual Studio Subscriptions erhalten haben, sollte sie automatisch aktiviert sein.