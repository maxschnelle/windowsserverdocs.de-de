---
ms.assetid: 231158d8-5e81-4630-b8d5-93fee16e0cd3
title: Bestimmen der Funktionsebenenupgrades
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 8aee6a5560edfae656582b3c2812ca69c6b90f57
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59812041"
---
# <a name="identifying-your-functional-level-upgrade"></a>Bestimmen der Funktionsebenenupgrades

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Bevor Sie die Domänen- und Gesamtstruktur-Funktionsebenen auslösen können, müssen Sie Bewertung Ihrer aktuellen Umgebung, und identifizieren die Anforderungen an die Domänenfunktionsebene, dass die Anforderungen Ihrer Organisation am besten erfüllt. Bewerten Sie Ihre aktuelle Umgebung durch Identifizieren der Domänen in der Gesamtstruktur, die Domänencontroller, die in jeder Domäne, das Betriebssystem und Servicepacks, die jedem Domänencontroller ausgeführt wird und das Datum, das Sie die Domäne ein upgrade planen befinden Controller. Wenn Sie einen Domänencontroller außer Kraft setzen möchten, stellen Sie sicher, dass Sie die vollständige Auswirkung wissen, dass dies also in Ihrer Umgebung.  
  
Die folgenden Situationen möglicherweise verhindern, dass Sie ein Upgrade einer früheren Version des Betriebssystems Windows Server auf der Funktionsebene der Windows Server 2008 oder Windows Server 2008 R2:  
  
-   Unzureichende hardware  
  
-   Einem Domänencontroller mit einem Antivirenprogramm, das nicht mit Windows Server 2008 oder Windows Server 2008 R2 kompatibel ist.   
  
-   Verwenden eines Programms hängt von der Version, die nicht auf Windows Server 2008 oder Windows Server 2008 R2 ausgeführt wird   
  
-   Die Notwendigkeit, ein Programm mit dem neuesten Servicepack aktualisieren  
  
Dokumentieren diese Informationen können Sie die Schritte zum Ausführen, um sicherzustellen, dass Sie eine voll funktionsfähige Windows Server 2008 oder Windows Server 2008 R2-Umgebung identifizieren können.  
  
Nachdem Sie Ihre aktuelle Umgebung einzuschätzen, müssen Sie die funktionsebenenaktualisierung zu identifizieren, die für Ihre Organisation gilt. Diese Optionen sind verfügbar:  
  
-   Im einheitlichen Modus-Umgebung für Windows 2000, Windows Server 2008 oder Windows Server 2008 R2   
  
-   Windows Server 2003-Gesamtstruktur auf Windows Server 2008 oder Windows Server 2008 R2   
  
-   Neue Windows Server 2008-Gesamtstruktur  
  
-   Neue Windows Server 2008 R2-Gesamtstruktur  
  
## <a name="upgrading-functional-levels-in-a-native-windows-2000-active-directory-forest"></a>Aktualisieren die Funktionsebenen in einer einheitlichen Windows 2000 Active Directory-Gesamtstruktur  
In einer nativen Windows 2000-Umgebung, die nur von Windows 2000-Domäne-Controllern besteht, werden die funktionalen Ebenen der standardmäßig auf den folgenden Ebenen festgelegt, und sie auf diesen Ebenen bleiben, bis Sie sie manuell auslösen:  
  
-   Funktionsebene für Windows 2000-Domäne im einheitlichen Modus  
  
-   Gesamtstrukturfunktionsebene Windows 2000  
  
Um alle auf Gesamtstrukturebene und Domänenebenen-Features in Windows Server 2008 oder Windows Server 2008 R2 verwenden zu können, müssen Sie diese Umgebung Windows 2000, Windows Server 2008 oder Windows Server 2008 R2 zu aktualisieren. Sie können das Upgrade auf eine der folgenden Arten ausführen:  
  
-   Führen Sie die neu installierte Windows Server 2008-basierte oder Windows Server 2008 R2--basierte Domänencontroller in der Gesamtstruktur, und Koppeln Sie es dann auf allen Domänencontrollern unter Windows 2000.  
  
-   Führen Sie ein direktes Upgrade aller vorhandenen Domänencontroller unter Windows 2000 in der Gesamtstruktur auf Domänencontrollern unter Windows Server 2003. Führen Sie anschließend ein direktes Upgrade der Domänencontroller auf Windows Server 2008 oder Windows Server 2008 R2. Weitere Informationen finden Sie unter [Aktualisieren von Active Directory-Domänen auf Windows Server 2008 AD DS-Domänen \[LH\]](assetId:///9c91be5f-df14-40b2-b176-2b1852a51e61).  
  
    > [!IMPORTANT]  
    >  Windows Server 2008 R2 ist ein X64-basiertes Betriebssystem an. Wenn es sich bei Ihrem Server eine X64-basierten Version von Windows Server 2003 ausgeführt wird, können Sie erfolgreich ein direktes Upgrade des Betriebssystems des Computers, auf Windows Server 2008 R2 ausführen. Wenn Ihr Server eine X86-basierten Version von Windows Server 2003 ausgeführt wird, können nicht Sie diesen Computer zu Windows Server 2008 R2 aktualisieren.  
  
Um die Windows Server 2008 oder Windows Server 2008 R2 auf Domänenebene Funktionen ohne ein Upgrade Ihrer Windows 2000-Gesamtstruktur auf Windows Server 2008 oder Windows Server 2008 R2 zu verwenden, lösen Sie nur die Domänenfunktionsebene auf Windows Server 2008 oder Windows Server 2008 R2.  
  
> [!NOTE]  
> Bevor Sie die Domänenfunktionsebene auf Heraufstufen, müssen Sie alle Windows 2000-basierten Domänencontroller in dieser Domäne auf Windows Server 2008 oder Windows Server 2008 R2 aktualisieren.  
  
Nachdem Sie alle Windows 2000-basierten Domänencontroller in der Gesamtstruktur mit Domänencontrollern ersetzt, auf denen Windows Server 2008 oder Windows Server 2008 R2 ausgeführt haben, können Sie die Gesamtstrukturfunktionsebene auf Windows Server 2008 oder Windows Server 2008 R2 auslösen. Automatisch ausführen, löst die Funktionsebene aller Domänen in der Gesamtstruktur, die auf Windows 2000 einheitlich oder höher auf Windows Server 2008 oder Windows Server 2008 R2 festgelegt werden.  
  
Weitere Informationen über das Auslösen von Funktionsebenen Gesamtstruktur und Domäne, und Verfahren zum Ausführen dieser Aufgaben finden Sie [Bereitstellen einer Windows Server 2008-Gesamtstruktur-Stammdomäne \[LH\]](assetId:///92406e8d-dc1c-4740-a00a-2c4032896dd1).  
  
## <a name="upgrading-functional-levels-in-a-windows-server-2003-active-directory-forest"></a>Aktualisieren die Funktionsebenen in einer Windows Server 2003 Active Directory-Gesamtstruktur  
In einer Windows Server 2003-Umgebung, die der nur die Windows Server 2003-basierten Domänencontroller besteht, werden die funktionalen Ebenen der standardmäßig auf den folgenden Ebenen festgelegt, und sie auf diesen Ebenen bleiben, bis Sie sie manuell auslösen:  
  
-   Funktionsebene für Windows 2000-Domäne im einheitlichen Modus  
  
-   Gesamtstrukturfunktionsebene Windows 2000  
  
Um alle auf Gesamtstrukturebene und Domänenebenen-Features in Windows Server 2008 oder Windows Server 2008 R2 verwenden zu können, müssen Sie diese Windows Server 2003-Umgebung auf Windows Server 2008 oder Windows Server 2008 R2 aktualisieren. Sie können das Upgrade auf eine der folgenden Arten ausführen:  
  
-   Führen Sie ein neu installierter Windows Server 2008-basierte oder Windows Server 2008 R2--basierten Domänencontroller in der Gesamtstruktur, und klicken Sie dann außer Kraft setzen alle Domänencontroller unter Windows Server 2003 oder Windows Server 2008 oder Windows Server 2008 R2 aktualisieren.  
  
-   Führen Sie ein direktes Upgrade aller vorhandenen Domänencontroller unter Windows Server 2003 auf Domänencontrollern unter Windows Server 2008 oder Windows Server 2008 R2. Weitere Informationen finden Sie unter [Aktualisieren von Active Directory-Domänen auf Windows Server 2008 AD DS-Domänen \[LH\]](assetId:///9c91be5f-df14-40b2-b176-2b1852a51e61).  
  
> [!IMPORTANT]  
>  Windows Server 2008 R2 ist ein X64-basiertes Betriebssystem an. Wenn es sich bei Ihrem Server eine X64-basierten Version von Windows Server 2003 ausgeführt wird, können Sie erfolgreich ein direktes Upgrade des Betriebssystems des Computers, auf Windows Server 2008 R2 ausführen. Dieser Computer zum Ausführen von Windows Server 2008 R2 kann nicht aktualisiert werden, wenn Ihr Server eine X86-basierten Version von Windows Server 2003 ausgeführt wird.  
  
Um alle Windows Server 2008 oder Windows Server 2008 R2-Domain-Level-Funktionen ohne ein Upgrade Ihrer Windows Server 2003-Gesamtstruktur auf Windows Server 2008 oder Windows Server 2008 R2 zu verwenden, lösen Sie nur die Domänenfunktionsebene auf Windows Server 2008 oder Windows-S Server 2008 R2.  
  
> [!NOTE]  
> Bevor Sie die Domänenfunktionsebene auf Heraufstufen, müssen Sie alle Windows Server 2003 – basierten Domänencontroller in dieser Domäne auf Windows Server 2008 oder Windows Server 2008 R2 aktualisieren.  
  
Nachdem Sie alle Windows Server 2003 – basierten Domänencontroller in der Gesamtstruktur auf Windows Server 2008 oder Windows Server 2008 R2 aktualisieren, können Sie die Gesamtstrukturfunktionsebene auf Windows Server 2008 oder Windows Server 2008 R2 auslösen. Automatisch ausführen, löst die Funktionsebene aller Domänen in der Gesamtstruktur, die auf Windows Server 2003, Windows Server 2008 oder Windows Server 2008 R2 festgelegt werden.  
  
Weitere Informationen über das Auslösen von Funktionsebenen Gesamtstruktur und Domäne, und Verfahren zum Ausführen dieser Aufgaben finden Sie [Bereitstellen einer Windows Server 2008-Gesamtstruktur-Stammdomäne \[LH\]](assetId:///92406e8d-dc1c-4740-a00a-2c4032896dd1).  
  
## <a name="upgrading-functional-levels-in-a-new-windows-server-2008-forest"></a>Aktualisieren die Funktionsebenen in einer neuen Windows Server 2008-Gesamtstruktur  
Bei der Installation des ersten Domänencontrollers in einer neuen Gesamtstruktur mit Windows Server 2008 standardmäßig auf den folgenden Ebenen festgelegt, und sie auf diesen Ebenen bleiben, bis Sie sie manuell auslösen:  
  
-   Funktionsebene für Windows 2000-Domäne im einheitlichen Modus  
  
-   Gesamtstrukturfunktionsebene Windows 2000  
  
Auf diesen Ebenen standardmäßig festgelegt, die Sie die Option zum Hinzufügen von Windows 2000 oder Windows Server 2003-basierten Domänencontroller der neuen Windows Server 2008-Gesamtstruktur geben. Nach der Erstellung einer Stammdomäne der Gesamtstruktur ist die Funktionsebene der Domäne, für jede Domäne, die Sie in der Windows Server 2008-Gesamtstruktur hinzufügen zu Windows 2000 native festgelegt. Wenn jedoch alle Domänencontroller in Ihrer neuen Windows Server 2008-Umgebung, Windows Server 2008 ausgeführt werden sollen, legen Sie Funktionsebene der Gesamtstruktur, und klicken Sie dann die Domänenfunktionsebene auf Windows Server 2008 bei der Installation des ersten Domänencontrollers in Ihrer Struktur t. Dies spart Zeit und kann alle auf Gesamtstrukturebene und Domänenebenen-Features in Windows Server 2008.  
  
> [!IMPORTANT]  
> Wenn die Gesamtstruktur auf Windows Server 2008 funktionale erfolgt auf, und Sie versuchen, die Active Directory auf einem Windows Server 2003 – basierten Mitgliedsserver installieren, oder Windows 2000 – basierten Mitgliedsserver, der Installation ein Fehler auftritt.  
  
Weitere Informationen über das Auslösen von Funktionsebenen Gesamtstruktur und Domäne, und Verfahren zum Ausführen dieser Aufgaben finden Sie [Bereitstellen einer Windows Server 2008-Gesamtstruktur-Stammdomäne \[LH\]](assetId:///92406e8d-dc1c-4740-a00a-2c4032896dd1).  
  
## <a name="upgrading-functional-levels-in-a-new-windows-server-2008-r2-forest"></a>Aktualisieren die Funktionsebenen in einer neuen Windows Server 2008 R2-Gesamtstruktur  
Bei der Installation des ersten Domänencontrollers in einer neuen Windows Server 2008 R2-Gesamtstruktur die funktionale Ebenen werden standardmäßig auf den folgenden Ebenen festgelegt, und sie auf diesen Ebenen bleiben, bis Sie sie manuell auslösen:  
  
-   Windows Server 2003-Domänenfunktionsebene  
  
-   Windows Server 2003-Gesamtstrukturfunktionsebene  
  
Auf diesen Ebenen standardmäßig festgelegt, die Sie die Option zum Hinzufügen von Windows Server 2003-basierten Domänencontroller der neuen Windows Server 2008 R2-Gesamtstruktur geben. Nach der Erstellung einer Gesamtstruktur-Stammdomäne, wird die Funktionsebene der Domäne, für jede Domäne, die Sie in der Windows Server 2008 R2-Gesamtstruktur hinzufügen zu Windows Server 2003 festgelegt. Wenn jedoch alle Domänencontroller in Ihrer neuen Windows Server 2008 R2-Umgebung zu Windows Server 2008 R2 ausgeführt werden sollen, legen Sie Funktionsebene der Gesamtstruktur, und klicken Sie dann die Domänenfunktionsebene auf Windows Server 2008 R2, wenn Sie den ersten Domänencontroller in "yo" installieren die Gesamtstruktur. Dies spart Zeit und kann alle auf Gesamtstrukturebene und Domänenebenen-Features in Windows Server 2008 R2.  
  
> [!IMPORTANT]  
> Wenn die Gesamtstruktur, die auf der Funktionsebene von Windows Server 2008 R2 ausgeführt wird und Sie versuchen, die Active Directory auf einem Windows Server 2008 installieren-basiert oder Windows Server 2003 – basierten Mitgliedsserver oder auf einem Windows 2000-basierten Mitgliedsserver, auf die Installation fehl.  
  
Weitere Informationen über das Auslösen von Funktionsebenen Gesamtstruktur und Domäne, und Verfahren zum Ausführen dieser Aufgaben finden Sie [Bereitstellen einer Windows Server 2008-Gesamtstruktur-Stammdomäne \[LH\]](assetId:///92406e8d-dc1c-4740-a00a-2c4032896dd1).  
  
> [!NOTE]  
> Obwohl ADMT v3. 1 unter Windows Server 2008 installiert werden müssen, können Sie ADMT v3. 1, zum Migrieren von Objekten in eine Domäne, die durch eine oder mehrere Windows Server 2008 R2-Domänencontroller gehostet wird. Weitere Informationen finden Sie unter [Artikel 976659](https://go.microsoft.com/fwlink/?LinkId=180398) in der Microsoft Knowledge Base (https://go.microsoft.com/fwlink/?LinkId=180398).  
  


