---
ms.assetid: 231158d8-5e81-4630-b8d5-93fee16e0cd3
title: Identifizieren die funktionale Ebene Aktualisierung
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 9527a186cb20c470e0b5644fff58f90786520f97
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="identifying-your-functional-level-upgrade"></a>Identifizieren die funktionale Ebene Aktualisierung

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Bevor Sie die Domänen- und Gesamtstrukturfunktionsebenen auslösen können, müssen Sie die Bewertung Ihrer aktuellen Umgebung und identifizieren die funktionale Ebene Anforderung, dass am besten den Erfordernissen Ihrer Organisation entspricht. Bewerten Sie die aktuelle Umgebung durch Identifizieren von Domänen in der Gesamtstruktur Domänencontroller, die in jeder Domäne, Betriebssystem und Servicepacks, die jeder Domänencontroller ausgeführt wird und das Datum, an dem Sie planen ein upgrade der Domänencontroller befinden. Wenn Sie einen Domänencontroller nicht mehr verwenden möchten, stellen Sie sicher, dass Sie die volle Auswirkung wissen, dass dies daher in Ihrer Umgebung.  
  
Die folgenden Situationen möglicherweise verhindern, dass Sie ein Upgrade von einer früheren Version des Betriebssystems Windows Server auf die Domänenfunktionsebene Windows Server 2008 oder Windows Server 2008 R2:  
  
-   Unzureichender hardware  
  
-   Einen Domänencontroller mit einem Antivirenprogramm, das mit Windows Server 2008 oder Windows Server 2008 R2 nicht kompatibel ist   
  
-   Verwenden eines versionsspezifischen Programms, das nicht auf Windows Server 2008 oder Windows Server 2008 R2 ausgeführt wird   
  
-   Die Notwendigkeit, ein Programm mit dem neuesten Servicepack zu aktualisieren  
  
Dokumentieren diese Informationen können Sie identifizieren die Schritte zum durchführen, um sicherzustellen, dass Sie eine voll funktionsfähige Windows Server 2008 oder Windows Server 2008 R2-Umgebung verfügen.  
  
Nachdem Sie die aktuelle Umgebung bewerten, müssen Sie die funktionale Ebene Aktualisierung zu identifizieren, die für Ihr Unternehmen gilt. Diese Optionen sind verfügbar:  
  
-   Windows 2000-Umgebung im einheitlichen Modus auf Windows Server 2008 oder Windows Server 2008 R2   
  
-   Windows Server 2003-Gesamtstruktur auf Windows Server 2008 oder Windows Server 2008 R2   
  
-   Neue Gesamtstruktur für Windows Server 2008  
  
-   Neue Windows Server 2008 R2-Gesamtstruktur  
  
## <a name="upgrading-functional-levels-in-a-native-windows-2000-active-directory-forest"></a>Aktualisieren die Funktionsebenen in einer einheitlichen Windows 2000 Active Directory-Gesamtstruktur  
In einer einheitlichen Windows 2000-Umgebung, die nur von Windows 2000-basierten Domänencontrollern besteht, die funktionalen Ebenen der standardmäßig auf die folgenden Werte festgelegt werden, und sie auf diesen Ebenen bleiben, bis Sie manuell auslösen:  
  
-   Funktionsebene der Windows 2000-Domäne im einheitlichen Modus  
  
-   Gesamtstrukturfunktionsebene Windows 2000  
  
Um alle auf Gesamtstrukturebene und auf Domänenebene Features in Windows Server 2008 oder Windows Server 2008 R2 verwenden, müssen Sie diese Windows 2000-Umgebung auf Windows Server 2008 oder Windows Server 2008 R2 aktualisieren. Sie können dieses Upgrade auf eine der folgenden Weisen ausführen:  
  
-   Jetzt neu installierten Windows Server 2008-basierten oder Windows Server 2008 R2-basierte Domänencontroller in der Gesamtstruktur, und Koppeln Sie es dann alle Domänencontroller unter Windows 2000.  
  
-   Durchführen einer direkten Aktualisierung aller vorhandenen Domänencontroller unter Windows 2000 in der Gesamtstruktur auf Domänencontrollern unter Windows Server 2003. Führen Sie dann ein direktes Upgrade der Domänencontroller auf Windows Server 2008 oder Windows Server 2008 R2. Weitere Informationen finden Sie unter [Aktualisieren von Active Directory-Domänen auf Windows Server 2008 AD DS-Domänen \[LH\]](assetId:///9c91be5f-df14-40b2-b176-2b1852a51e61).  
  
    > [!IMPORTANT]  
    >  Windows Server 2008 R2 ist eine X64-basiertes Betriebssystem. Wenn Ihr Server eine X64-basierte Version von Windows Server 2003 ausgeführt wird, können Sie ein direktes Upgrade des Betriebssystems des Computers, auf Windows Server 2008 R2 erfolgreich ausführen. Dieser Computer kann nicht auf Windows Server 2008 R2 aktualisiert werden, wenn der Server eine X86-basierten Version von Windows Server 2003 ausgeführt wird.  
  
Um die Windows Server 2008 oder Windows Server 2008 R2-Features auf Domänenebene verwenden, ohne ein Upgrade Ihrer Windows 2000-Gesamtstruktur auf Windows Server 2008 oder Windows Server 2008 R2, heben Sie nur die Domänenfunktionsebene auf Windows Server 2008 oder Windows Server 2008 R2.  
  
> [!NOTE]  
> Bevor Sie die Domänenfunktionsebene auf Heraufstufen, müssen Sie alle Windows 2000-basierten Domänencontrollern in der Domäne auf Windows Server 2008 oder Windows Server 2008 R2 aktualisieren.  
  
Nachdem Sie alle Windows 2000-basierten Domänencontrollern in der Gesamtstruktur mit Domänencontrollern ersetzt, auf denen Windows Server 2008 oder Windows Server 2008 R2 ausgeführt haben, können Sie die Gesamtstrukturfunktionsebene auf Windows Server 2008 oder Windows Server 2008 R2 heraufstufen. Automatisch ausführen, löst die funktionale Ebene des alle Domänen in der Gesamtstruktur, die auf Windows 2000 einheitlich oder höher, Windows Server 2008 oder Windows Server 2008 R2 festgelegt werden.  
  
Weitere Informationen zum Auslösen von Funktionsebenen der Gesamtstruktur und Domäne, und zum Ausführen dieser Aufgaben finden Sie [Bereitstellen einer Windows Server 2008-Gesamtstruktur Stamm Domäne \[LH\]](assetId:///92406e8d-dc1c-4740-a00a-2c4032896dd1).  
  
## <a name="upgrading-functional-levels-in-a-windows-server-2003-active-directory-forest"></a>Aktualisieren die Funktionsebenen in einer Windows Server 2003 Active Directory-Gesamtstruktur  
In einer Windows Server 2003-Umgebung, die der nur die Windows Server 2003-basierten Domänencontrollern besteht, die funktionalen Ebenen der standardmäßig auf die folgenden Werte festgelegt werden, und sie auf diesen Ebenen bleiben, bis Sie manuell auslösen:  
  
-   Funktionsebene der Windows 2000-Domäne im einheitlichen Modus  
  
-   Gesamtstrukturfunktionsebene Windows 2000  
  
Um alle auf Gesamtstrukturebene und auf Domänenebene Features in Windows Server 2008 oder Windows Server 2008 R2 verwenden, müssen Sie diese Umgebung Windows Server 2003 auf Windows Server 2008 oder Windows Server 2008 R2 aktualisieren. Sie können dieses Upgrade auf eine der folgenden Weisen ausführen:  
  
-   Stellen Sie vor einem neu installierten Windows Server 2008-basierten oder Windows Server 2008 R2-Domänencontroller in der Gesamtstruktur, und klicken Sie dann alle Domänencontroller unter Windows Server 2003 oder ein upgrade auf Windows Server 2008 oder Windows Server 2008 R2.  
  
-   Durchführen einer direkten Aktualisierung aller vorhandenen Domänencontroller unter Windows Server 2003 auf Domänencontrollern unter Windows Server 2008 oder Windows Server 2008 R2. Weitere Informationen finden Sie unter [Aktualisieren von Active Directory-Domänen auf Windows Server 2008 AD DS-Domänen \[LH\]](assetId:///9c91be5f-df14-40b2-b176-2b1852a51e61).  
  
> [!IMPORTANT]  
>  Windows Server 2008 R2 ist eine X64-basiertes Betriebssystem. Wenn Ihr Server eine X64-basierte Version von Windows Server 2003 ausgeführt wird, können Sie ein direktes Upgrade des Betriebssystems des Computers, auf Windows Server 2008 R2 erfolgreich ausführen. Wenn Ihr Server eine X86-basierten Version von Windows Server 2003 ausgeführt wird, wird dieser Computer zum Ausführen von Windows Server 2008 R2 kann nicht aktualisiert.  
  
Um die Windows Server 2008 oder Windows Server 2008 R2-Domäne-Level-Funktionen verwenden, ohne ein Upgrade Ihrer Windows Server 2003-Gesamtstruktur auf Windows Server 2008 oder Windows Server 2008 R2, heben Sie nur die Domänenfunktionsebene auf Windows Server 2008 oder Windows Server 2008 R2.  
  
> [!NOTE]  
> Bevor Sie die Domänenfunktionsebene auf Heraufstufen, müssen Sie alle Windows Server 2003-basierten Domänencontrollern in der Domäne auf Windows Server 2008 oder Windows Server 2008 R2 aktualisieren.  
  
Wenn Sie alle Windows Server 2003-basierten Domänencontrollern in der Gesamtstruktur auf Windows Server 2008 oder Windows Server 2008 R2 aktualisieren, können Sie die Gesamtstrukturfunktionsebene auf Windows Server 2008 oder Windows Server 2008 R2 heraufstufen. Automatisch ausführen, löst die funktionale Ebene des alle Domänen in der Gesamtstruktur, die auf Windows Server 2003 zu Windows Server 2008 oder Windows Server 2008 R2 festgelegt sind.  
  
Weitere Informationen zum Auslösen von Funktionsebenen der Gesamtstruktur und Domäne, und zum Ausführen dieser Aufgaben finden Sie [Bereitstellen einer Windows Server 2008-Gesamtstruktur Stamm Domäne \[LH\]](assetId:///92406e8d-dc1c-4740-a00a-2c4032896dd1).  
  
## <a name="upgrading-functional-levels-in-a-new-windows-server-2008-forest"></a>Aktualisieren die Funktionsebenen in einer neuen Windows Server 2008  
Bei der Installation des ersten Domänencontrollers in einer neuen Windows Server 2008 Funktionsebenen standardmäßig auf die folgenden Werte festgelegt werden, und sie auf diesen Ebenen bleiben, bis Sie manuell auslösen:  
  
-   Funktionsebene der Windows 2000-Domäne im einheitlichen Modus  
  
-   Gesamtstrukturfunktionsebene Windows 2000  
  
Funktionsebenen werden auf diesen Standardebenen festgelegt, damit Sie von Windows 2000 oder Windows Server 2003-basierten Domänencontrollern der neuen Windows Server 2008-Gesamtstruktur hinzufügen können. Nach der Erstellung einer Gesamtstruktur-Stammdomäne ist die Domänenfunktionsebene für jede Domäne, die Sie in der Windows Server 2008-Gesamtstruktur hinzufügen auf Windows 2000 pur. Wenn jedoch alle Domänencontroller in der neuen Windows Server 2008-Umgebung Windows Server 2008 ausgeführt werden soll, festlegen Sie Funktionsebene der Gesamtstruktur, und klicken Sie dann die Domänenfunktionsebene auf Windows Server 2008 bei der Installation des ersten Domänencontrollers in der Gesamtstruktur. Auf diese Weise sparen Sie Zeit und aktiviert alle auf Gesamtstrukturebene und auf Domänenebene Features in Windows Server 2008.  
  
> [!IMPORTANT]  
> Wenn die Gesamtstruktur auf Windows Server 2008-Domänenfunktionsebene verwendet wird Ebene und Sie versuchen, das Installieren von Active Directory auf einem Mitgliedsserver mit Windows Server 2003-basierten oder Windows 2000-basierten Mitgliedsserver, der Installation ein Fehler auftritt.  
  
Weitere Informationen zum Auslösen von Funktionsebenen der Gesamtstruktur und Domäne, und zum Ausführen dieser Aufgaben finden Sie [Bereitstellen einer Windows Server 2008-Gesamtstruktur Stamm Domäne \[LH\]](assetId:///92406e8d-dc1c-4740-a00a-2c4032896dd1).  
  
## <a name="upgrading-functional-levels-in-a-new-windows-server-2008-r2-forest"></a>Aktualisieren die Funktionsebenen in einer neuen Windows Server 2008 R2  
Bei der Installation des ersten Domänencontrollers in einer neuen Windows Server 2008 R2 Funktionsebenen standardmäßig auf die folgenden Werte festgelegt werden, und sie auf diesen Ebenen bleiben, bis Sie manuell auslösen:  
  
-   Windows Server 2003-Domänenfunktionsebene  
  
-   Windows Server 2003-Gesamtstrukturfunktionsebene  
  
Funktionsebenen werden auf diesen Standardebenen festgelegt, damit Sie von Windows Server 2003-basierten Domänencontroller der neuen Windows Server 2008 R2-Gesamtstruktur hinzufügen können. Nachdem Sie eine Gesamtstruktur-Stammdomäne erstellt haben, wird die Domänenfunktionsebene für jede Domäne, die Sie in der Windows Server 2008 R2-Gesamtstruktur hinzufügen auf Windows Server 2003 festgelegt. Wenn jedoch alle Domänencontroller in der neuen Windows Server 2008 R2-Umgebung Windows Server 2008 R2 ausgeführt werden soll, festlegen Sie Funktionsebene der Gesamtstruktur, und klicken Sie dann die Domänenfunktionsebene für Windows Server 2008 R2 bei der Installation des ersten Domänencontrollers in der Gesamtstruktur. Auf diese Weise sparen Sie Zeit und alle auf Gesamtstrukturebene und auf Domänenebene Features in Windows Server 2008 R2 aktiviert.  
  
> [!IMPORTANT]  
> Wenn die Gesamtstruktur, die auf der Funktionsebene von Windows Server 2008 R2 ausgeführt wird und Sie versuchen, Installieren von Active Directory unter Windows Server 2008-Basis oder Windows Server 2003-basierten Mitgliedsserver oder auf einem Windows 2000-basierten Mitgliedsserver, schlägt die Installation fehl.  
  
Weitere Informationen zum Auslösen von Funktionsebenen der Gesamtstruktur und Domäne, und zum Ausführen dieser Aufgaben finden Sie [Bereitstellen einer Windows Server 2008-Gesamtstruktur Stamm Domäne \[LH\]](assetId:///92406e8d-dc1c-4740-a00a-2c4032896dd1).  
  
> [!NOTE]  
> Obwohl ADMT v3. 1 unter Windows Server 2008 installiert werden müssen, können Sie ADMT v3. 1, zum Migrieren von Objekten zu einer Domäne, die durch eine oder mehrere Windows Server 2008 R2-Domänencontroller gehostet wird. Weitere Informationen finden Sie unter [Artikel 976659](https://go.microsoft.com/fwlink/?LinkId=180398) in der Microsoft Knowledge Base (https://go.microsoft.com/fwlink/?LinkId=180398).  
  


