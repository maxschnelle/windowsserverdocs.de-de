---
ms.assetid: 231158d8-5e81-4630-b8d5-93fee16e0cd3
title: Bestimmen der Funktionsebenenaktualisierung
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 02620fdce6132fa3868207ffe2afbf6c95e6a37b
ms.sourcegitcommit: 11421f4005f9f3a3f6c0db95b1836d0f765a9fa3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2020
ms.locfileid: "81624198"
---
# <a name="identifying-your-functional-level-upgrade"></a>Bestimmen der Funktionsebenenaktualisierung

> Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Bevor Sie Domänen-und Gesamtstruktur Funktionsebenen erhöhen können, müssen Sie die aktuelle Umgebung auswerten und die Funktionsebene ermitteln, die die Anforderungen Ihrer Organisation am besten erfüllt. Bewerten Sie Ihre aktuelle Umgebung, indem Sie die Domänen in der Gesamtstruktur, die Domänen Controller in den einzelnen Domänen, das Betriebssystem und die Service Packs, die auf den einzelnen Domänen Controllern ausgeführt werden, und das Datum, an dem Sie das Upgrade der Domänen Controller planen Wenn Sie einen Domänen Controller außer Betrieb nehmen möchten, stellen Sie sicher, dass Sie die vollständige Auswirkung auf Ihre Umgebung kennen.

Die folgenden Umstände können verhindern, dass Sie eine frühere Version des Windows Server-Betriebssystems auf die Funktionsebene Windows Server 2008 oder Windows Server 2008 R2 aktualisieren:

- Unzureichende Hardware

- Ein Domänen Controller, auf dem ein Antivirenprogramm ausgeführt wird, das mit Windows Server 2008 oder Windows Server 2008 R2 nicht kompatibel ist

- Verwendung eines Versions spezifischen Programms, das nicht unter Windows Server 2008 oder Windows Server 2008 R2 ausgeführt wird

- Das Upgrade eines Programms mit den neuesten Service Pack

Diese Informationen können Ihnen dabei helfen, die erforderlichen Schritte zu identifizieren, um sicherzustellen, dass Sie über eine voll funktionsfähige Windows Server 2008-oder Windows Server 2008 R2-Umgebung verfügen.

Nachdem Sie die aktuelle Umgebung ausgewertet haben, müssen Sie die Funktionsebene aktualisieren, die für Ihre Organisation gilt. Diese Optionen sind verfügbar:

- Windows 2000-Umgebung im einheitlichen Modus zu Windows Server 2008 oder Windows Server 2008 R2

- Windows Server 2003-Gesamtstruktur zu Windows Server 2008 oder Windows Server 2008 R2

- Neue Windows Server 2008-Gesamtstruktur

- Neue Windows Server 2008 R2-Gesamtstruktur

## <a name="upgrading-functional-levels-in-a-native-windows-2000-active-directory-forest"></a>Aktualisieren von Funktionsebenen in einer systemeigenen Windows 2000 Active Directory-Gesamtstruktur
In einer systemeigenen Windows 2000-Umgebung, die nur aus Windows 2000-basierten Domänen Controllern besteht, werden die Funktionsebenen standardmäßig auf die folgenden Ebenen festgelegt und bleiben so lange erhalten, bis Sie Sie manuell erhöhen:

- Funktionsebene der systemeigenen Windows 2000-Domäne

- Windows 2000-Gesamtstruktur Funktionsebene

Wenn Sie alle Features auf Gesamtstruktur-und Domänen Ebene in Windows Server 2008 oder Windows Server 2008 R2 verwenden möchten, müssen Sie für diese Windows 2000-Umgebung ein Upgrade auf Windows Server 2008 oder Windows Server 2008 R2 durchführen. Dieses Upgrade kann auf eine der folgenden Arten ausgeführt werden:

- Führen Sie neu installierte Windows Server 2008-oder Windows Server 2008 R2-basierte Domänen Controller in die Gesamtstruktur ein, und ziehen Sie dann alle Domänen Controller unter Windows 2000 außer Betrieb.

- Führen Sie ein direktes Upgrade aller vorhandenen Domänen Controller unter Windows 2000 in der Gesamtstruktur auf Domänen Controller unter Windows Server 2003 aus. Führen Sie dann ein direktes Upgrade dieser Domänen Controller auf Windows Server 2008 oder Windows Server 2008 R2 aus. Weitere Informationen finden Sie unter [Aktualisieren von Active Directory Domänen auf Windows Server 2008 und Windows Server 2008 R2 AD DS Domänen](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731188(v=ws.10)).

    > [!IMPORTANT]
    >  Windows Server 2008 R2 ist ein x64-basiertes Betriebssystem. Wenn auf Ihrem Server eine x64-basierte Version von Windows Server 2003 ausgeführt wird, können Sie ein direktes Upgrade des Betriebssystems dieses Computers auf Windows Server 2008 R2 durchführen. Wenn auf Ihrem Server eine x86-basierte Version von Windows Server 2003 ausgeführt wird, können Sie diesen Computer nicht auf Windows Server 2008 R2 aktualisieren.

Um die Features auf Domänen Ebene in Windows Server 2008 oder Windows Server 2008 R2 zu verwenden, ohne die gesamte Windows 2000-Gesamtstruktur auf Windows Server 2008 oder Windows Server 2008 R2 zu aktualisieren, müssen Sie nur die Domänen Funktionsebene auf Windows Server 2008 oder Windows Server 2008 R2 erhöhen.

> [!NOTE]
> Bevor Sie die Domänen Funktionsebene erhöhen, müssen Sie für alle Windows 2000-basierten Domänen Controller in dieser Domäne ein Upgrade auf Windows Server 2008 oder Windows Server 2008 R2 durchführen.

Nachdem Sie alle Windows 2000-basierten Domänen Controller in der Gesamtstruktur durch Domänen Controller ersetzt haben, auf denen Windows Server 2008 oder Windows Server 2008 R2 ausgeführt wird, können Sie die Gesamtstruktur Funktionsebene auf Windows Server 2008 oder Windows Server 2008 R2 erhöhen. Dadurch wird die Funktionsebene aller Domänen in der Gesamtstruktur, die auf Windows 2000 native oder höher festgelegt sind, automatisch auf Windows Server 2008 oder Windows Server 2008 R2 angehoben.

Weitere Informationen zum Erhöhen der Gesamtstruktur-und Domänen Funktionsebenen sowie zu Verfahren zum Ausführen dieser Aufgaben finden Sie unter Bereitstellen [einer Windows Server 2008](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc731174(v=ws.10))-Gesamtstruktur-Stamm Domäne.

## <a name="upgrading-functional-levels-in-a-windows-server-2003-active-directory-forest"></a>Aktualisieren von Funktionsebenen in einer Windows Server 2003 Active Directory-Gesamtstruktur
In einer Windows Server 2003-Umgebung, die nur aus Windows Server 2003-basierten Domänen Controllern besteht, werden die Funktionsebenen standardmäßig auf die folgenden Ebenen festgelegt und bleiben so lange erhalten, bis Sie Sie manuell erhöhen:

- Funktionsebene der systemeigenen Windows 2000-Domäne

- Windows 2000-Gesamtstruktur Funktionsebene

Wenn Sie alle Features auf Gesamtstruktur-und Domänen Ebene in Windows Server 2008 oder Windows Server 2008 R2 verwenden möchten, müssen Sie für diese Windows Server 2003-Umgebung ein Upgrade auf Windows Server 2008 oder Windows Server 2008 R2 durchführen. Dieses Upgrade kann auf eine der folgenden Arten ausgeführt werden:

- Führen Sie einen neu installierten Windows Server 2008-oder Windows Server 2008 R2-basierten Domänen Controller in die Gesamtstruktur ein, und ziehen Sie dann alle Domänen Controller unter Windows Server 2003 außer Betrieb, oder führen Sie ein Upgrade auf Windows Server 2008 oder Windows Server 2008 R2 aus.

- Führen Sie ein direktes Upgrade aller vorhandenen Domänen Controller unter Windows Server 2003 auf Domänen Controllern aus, auf denen Windows Server 2008 oder Windows Server 2008 R2 ausgeführt wird. Weitere Informationen finden Sie unter [Aktualisieren von Active Directory Domänen auf Windows Server 2008 und Windows Server 2008 R2 AD DS Domänen](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731188(v=ws.10)).

> [!IMPORTANT]
> Windows Server 2008 R2 ist ein x64-basiertes Betriebssystem. Wenn auf Ihrem Server eine x64-basierte Version von Windows Server 2003 ausgeführt wird, können Sie ein direktes Upgrade des Betriebssystems dieses Computers auf Windows Server 2008 R2 durchführen. Wenn auf Ihrem Server eine x86-basierte Version von Windows Server 2003 ausgeführt wird, können Sie diesen Computer nicht aktualisieren, um Windows Server 2008 R2 auszuführen.

Wenn Sie alle Windows Server 2008-oder Windows Server 2008 R2-Features auf Domänen Ebene verwenden möchten, ohne die gesamte Windows Server 2003-Gesamtstruktur auf Windows Server 2008 oder Windows Server 2008 R2 zu aktualisieren, müssen Sie nur die Domänen Funktionsebene für Windows Server 2008 oder Windows Server 2008 R2 erhöhen.

> [!NOTE]
> Bevor Sie die Domänen Funktionsebene erhöhen, müssen Sie für alle Windows Server 2003-basierten Domänen Controller in dieser Domäne ein Upgrade auf Windows Server 2008 oder Windows Server 2008 R2 durchführen.

Nachdem Sie alle Windows Server 2003-basierten Domänen Controller in der Gesamtstruktur auf Windows Server 2008 oder Windows Server 2008 R2 aktualisiert haben, können Sie die Gesamtstruktur Funktionsebene auf Windows Server 2008 oder Windows Server 2008 R2 erhöhen. Dadurch wird die Funktionsebene aller Domänen in der Gesamtstruktur, die auf Windows Server 2003 auf Windows Server 2008 oder Windows Server 2008 R2 festgelegt sind, automatisch erhöht.

Weitere Informationen zum Erhöhen der Gesamtstruktur-und Domänen Funktionsebenen sowie zu Verfahren zum Ausführen dieser Aufgaben finden Sie unter Bereitstellen [einer Windows Server 2008](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc731174(v=ws.10))-Gesamtstruktur-Stamm Domäne.

## <a name="upgrading-functional-levels-in-a-new-windows-server-2008-forest"></a>Aktualisieren von Funktionsebenen in einer neuen Windows Server 2008-Gesamtstruktur
Wenn Sie den ersten Domänen Controller in einer neuen Windows Server 2008-Gesamtstruktur installieren, werden die Funktionsebenen standardmäßig auf die folgenden Ebenen festgelegt und bleiben so lange erhalten, bis Sie Sie manuell erhöhen:

- Funktionsebene der systemeigenen Windows 2000-Domäne

- Windows 2000-Gesamtstruktur Funktionsebene

Funktionsebenen werden auf diesen Standard Ebenen festgelegt, um Ihnen das Hinzufügen von Windows 2000-oder Windows Server 2003-basierten Domänen Controllern zur neuen Windows Server 2008-Gesamtstruktur zu gestatten. Nachdem Sie eine Gesamtstruktur-Stamm Domäne erstellt haben, wird die Domänen Funktionsebene für jede Domäne, die Sie der Windows Server 2008-Gesamtstruktur hinzufügen, auf Windows 2000 native festgelegt. Wenn Sie jedoch möchten, dass alle Domänen Controller in der neuen Windows Server 2008-Umgebung Windows Server 2008 ausführen, legen Sie die Gesamtstruktur Funktionsebene und dann die Domänen Funktionsebene auf Windows Server 2008 fest, wenn Sie den ersten Domänen Controller in der Gesamtstruktur installieren. Dies spart Zeit und ermöglicht alle Features auf Gesamtstruktur Ebene und auf Domänen Ebene in Windows Server 2008.

> [!IMPORTANT]
> Wenn die Gesamtstruktur auf der Windows Server 2008-Funktionsebene ausgeführt wird und Sie versuchen, Active Directory auf einem Windows Server 2003-basierten Mitglieds Server oder einem Windows 2000-basierten Mitglieds Server zu installieren, tritt bei der Installation ein Fehler auf.

Weitere Informationen zum Erhöhen der Gesamtstruktur-und Domänen Funktionsebenen sowie zu Verfahren zum Ausführen dieser Aufgaben finden Sie unter Bereitstellen [einer Windows Server 2008](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc731174(v=ws.10))-Gesamtstruktur-Stamm Domäne.

## <a name="upgrading-functional-levels-in-a-new-windows-server-2008-r2-forest"></a>Aktualisieren von Funktionsebenen in einer neuen Windows Server 2008 R2-Gesamtstruktur
Wenn Sie den ersten Domänen Controller in einer neuen Windows Server 2008 R2-Gesamtstruktur installieren, werden die Funktionsebenen standardmäßig auf die folgenden Ebenen festgelegt, und Sie verbleiben auf diesen Ebenen, bis Sie Sie manuell erhöhen:

- Windows Server 2003-Domänen Funktionsebene

- Windows Server 2003-Gesamtstruktur Funktionsebene

Funktionsebenen werden auf diesen Standard Ebenen festgelegt, um Ihnen das Hinzufügen von Windows Server 2003-basierten Domänen Controllern zur neuen Windows Server 2008 R2-Gesamtstruktur zu gestatten. Nachdem Sie eine Gesamtstruktur-Stamm Domäne erstellt haben, wird die Domänen Funktionsebene für jede Domäne, die Sie der Windows Server 2008 R2-Gesamtstruktur hinzufügen, auf Windows Server 2003 festgelegt. Wenn Sie jedoch möchten, dass alle Domänen Controller in der neuen Windows Server 2008 R2-Umgebung Windows Server 2008 R2 ausführen, legen Sie die Gesamtstruktur Funktionsebene und dann die Domänen Funktionsebene auf Windows Server 2008 R2 fest, wenn Sie den ersten Domänen Controller in der Gesamtstruktur installieren. Dies spart Zeit und ermöglicht alle Features auf Gesamtstruktur Ebene und auf Domänen Ebene in Windows Server 2008 R2.

> [!IMPORTANT]
> Wenn die Gesamtstruktur auf der Windows Server 2008 R2-Funktionsebene ausgeführt wird und Sie versuchen, Active Directory auf einem Windows Server 2008-basierten oder Windows Server 2003-basierten Mitglieds Server oder auf einem Windows 2000-basierten Mitglieds Server zu installieren, tritt bei der Installation ein Fehler auf.

Weitere Informationen zum Erhöhen der Gesamtstruktur-und Domänen Funktionsebenen sowie zu Verfahren zum Ausführen dieser Aufgaben finden Sie unter Bereitstellen [einer Windows Server 2008](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc731174(v=ws.10))-Gesamtstruktur-Stamm Domäne.

> [!NOTE]
> Obwohl ADMT v 3.1 auf Windows Server 2008 installiert werden muss, können Sie ADMT v 3.1 zum Migrieren von Objekten zu einer Domäne verwenden, die von einem oder mehreren Windows Server 2008 R2-Domänen Controllern gehostet wird. Weitere Informationen finden Sie im Artikel 976659 in der Microsoft Knowledge Base, [bekannte Probleme, die auftreten können, wenn Sie ADMT 3,1 zum Migrieren zu einer Domäne verwenden, die Windows Server 2008 R2-Domänen Controller enthält](https://support.microsoft.com/help/976659/).
