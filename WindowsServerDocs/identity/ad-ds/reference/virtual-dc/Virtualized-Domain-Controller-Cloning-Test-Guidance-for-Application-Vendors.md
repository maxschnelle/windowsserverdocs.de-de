---
ms.assetid: fde99b44-cb9f-49bf-b888-edaeabe6b88d
title: "Für Anwendungsanbieter Testleitfaden: Klonen von virtualisierten Domänencontrollern"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 72c4e818f82d3252c45776b26fb59e095893f2c7
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="virtualized-domain-controller-cloning-test-guidance-for-application-vendors"></a>Für Anwendungsanbieter Testleitfaden: Klonen von virtualisierten Domänencontrollern

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

In diesem Thema wird erläutert, was Anwendungsanbieter berücksichtigen sollten, um sicherzustellen, dass die Anwendung weiterhin funktioniert wie erwartet, wenn der Prozess für das Klonen virtualisierter Domänencontroller (DC) abgeschlossen ist. Es behandelt diese Aspekte des klonprozesses dieses Interesse Anwendungsanbieter und Szenarien, die zusätzlichen Tests erfordern können. Anwendung Lieferanten überprüft haben, dass ihre Anwendung für virtualisierte Domänencontroller, die geklont wurden, wird empfohlen, den Namen der Anwendung in den Community-Inhalten unten in diesem Thema mit einem Link zur Website Ihrer Organisation aufgelistet, in denen Benutzer über die Validierung informieren können.  
  
## <a name="overview-of-virtualized-dc-cloning"></a>Übersicht über das Klonen von virtualisierten Domänencontroller  
Ist der Prozess für das Klonen virtualisierten Domänencontrollers ausführlich beschrieben [Introduction to Active Directory-Domänendienste (AD DS) Virtualization (Level 100)](https://technet.microsoft.com/library/hh831734.aspx) und [virtualisierte technische Referenz für Domänencontroller (Level 300)](https://technet.microsoft.com/library/jj574214.aspx). Aus Sicht einer App-Anbieter sind dies einige Aspekte zu berücksichtigen, wenn Sie die Auswirkungen auf Ihre Anwendung Klonen:  
  
-   Der ursprüngliche Computer wird nicht gelöscht. Es bleibt im Netzwerk, die Interaktion mit Clients. Im Gegensatz zu einem umbenennen, in denen die DNS-Einträge des ursprünglichen Computers entfernt werden, bleiben die ursprünglichen Datensätze für die Quell-Domänencontroller.  
  
-   Während des Klonens wird der neue Computer zunächst für einen kurzen Zeitraum unter der Identität des alten Computer ausgeführt, bis der Klonvorgang initiiert, und nimmt die erforderlichen Änderungen vor. Anwendungen, die Einträge zum Host erstellen sollten sicherstellen, dass der geklonte Computer Datensätze zum ursprünglichen Host nicht während des Klonens überschrieben wird.  
  
-   Das Klonen ist eine bestimmte Bereitstellung-Funktion ausschließlich für virtualisierte Domänencontroller, keine allgemeine-Erweiterung für andere Serverrollen zu klonen. Einige Serverrollen werden nicht speziell für das Klonen unterstützt:  
  
    -   Dynamic Host Configuration-Protokoll (DHCP)  
  
    -   Active Directory-Zertifikatdienste (AD CS)  
  
    -   Active Directory Lightweight Directory Services (AD LDS)  
  
-   Als Teil der Klonvorgang ausgeführt wird der gesamte virtuelle Computer, der den ursprünglichen DC darstellt kopiert, sodass auch alle App-Status auf diesem virtuellen Computer kopiert wird. Überprüfen Sie, ob die Anwendung auf diese Änderung in den Zustand des lokalen Hosts auf dem geklonten Domänencontroller, passt sich oder Eingreifen erforderlich, z. B. einen Neustart des Diensts ist.  
  
-   Als Teil des Klonen ruft der neue Domänencontroller eine neue Computeridentität und Vorschriften selbst als ein Replikat-DC in der Topologie. Überprüfen Sie, ob die Anwendung die Computeridentität, z. B. Name, Konto, SID und usw. abhängig. Anpassen es automatisch auf die Änderung von Computeridentität auf dem Klon? Die Anwendung Daten zwischenspeichert, sicher, dass es nicht auf Computer Identitätsdaten angewiesen ist, die zwischengespeichert werden können.  
  
## <a name="what-is-interesting-for-application-vendors"></a>Was ist für Anwendungsanbieter interessant?  
  
### <a name="customdccloneallowlistxml"></a>CustomDCCloneAllowList.xml  
Ein Domänencontroller, der die Anwendung oder der Dienst ausgeführt wird kann nicht geklont werden, bis die Anwendung oder Dienst ist:  
  
-   Mithilfe von Get-ADDCCloningExcludedApplicationList Windows PowerShell-Cmdlets hinzugefügt zur Datei CustomDCCloneAllowList.xml  
  
– Oder –  
  
-   Vom Domänencontroller entfernt  
  
Der Benutzer das Cmdlet Get-ADDCCloningExcludedApplicationList führt zum ersten Mal gibt es eine Liste der Dienste und Anwendungen, die auf dem Domänencontroller ausgeführt werden, jedoch sind nicht in der Liste der Dienste und Anwendungen, die für das Klonen unterstützt werden. Standardmäßig wird der Dienst oder eine Anwendung nicht aufgeführt. Zum Hinzufügen von dem Dienst oder Anwendung in der Liste der Anwendungen und Dienste, die sicher sein können geklont, die Benutzer ausgeführt wird, die Datei-Cmdlet "Get-ADDCCloningExcludedApplicationList" erneut mit der Option - GenerateXML, damit er zu CustomDCCloneAllowList.xml hinzugefügt. Weitere Informationen finden Sie unter [Schritt2: Ausführen von Get-ADDCCloningExcludedApplicationList Cmdlet](https://technet.microsoft.com/library/hh831734.aspx#bkmk6_run_get_addccloningexcludedapplicationlist_cmdlet).  
  
### <a name="distributed-system-interactions"></a>Verteilte System-Interaktionen  
In der Regel auf dem lokalen Computer isoliert Dienste entweder erfolgreich oder Fehler beim Klonen teilnehmen. Verteilte Dienste Gedanken über zwei Instanzen der Host-PC gleichzeitig im Netzwerk damit für einen kurzen Zeitraum werden müssen. Dies kann-manifest als eine Instanz möchten, rufen Informationen von einem Partnersystem, auf dem der Klon als neue Anbieter der Identität registriert. Oder beide Instanzen des Diensts können in AD DS-Datenbank Informationen drücken Sie gleichzeitig mit anderen Ergebnissen. Beispielsweise ist es nicht deterministisch, welche Computer mit mitgeteilt wird, wenn zwei Computer, auf denen testen Technologien WTT (Windows) Service im Netzwerk mit dem Domänencontroller sind.  
  
Für die verteilte DNS-Serverdienst muss der Klonvorgang sorgfältig, überschreiben die DNS-Einträge mit dem Quelldomänencontroller beim Starten des geklonten Domänencontrollers mit einer neuen IP-Adresse.  
  
Sie sollten auf dem Computer So entfernen Sie alle der alte Identität bis zum Ende der Klonvorgang nicht verlassen. Nachdem der neue Domänencontroller in der neuen Kontext heraufgestuft wurde, wählen Sie Sysprep-Anbieter ausgeführt werden, um den zusätzlichen Zustand des Computers zu bereinigen. Beispielsweise ist es an diesem Punkt werden die alten Zertifikate des Computers entfernt und die Kryptografie-Schlüssel, die den Computer zugreifen können geändert werden.  
  
Der größte Faktor, der den Zeitpunkt für das Klonen variiert ist, wie viele Objekte vorhanden sind, vom primären Domänencontroller repliziert werden. Ältere Medien erhöht sich den Zeitaufwand für das Klonen abgeschlossen.  
  
Da es sich bei dem Dienst oder der Anwendung unbekannt ist, bleibt er ausgeführt wird. Der Klonvorgang ändert nicht den Status der nicht-Windows-Dienste.  
  
Darüber hinaus wurde der neue Computer eine andere IP-Adresse als den ursprünglichen Computer. Dieses Verhalten können Nebenwirkungen zu Ihrem Dienst oder Anwendung wird je nach dem Dienst oder eine Anwendung in dieser Umgebung Verhalten führen.  
  
## <a name="additional-scenarios-suggested-for-testing"></a>Weitere Szenarien zum Testen vorgeschlagene  
  
### <a name="cloning-failure"></a>Fehler beim Klonen  
Service-Anbieter sollte dieses Szenario getestet werden, da der Computer beim Klonen tritt ein Fehler in Directory Services Repair Verzeichnisdienstwiederherstellungsmodus (DSRM), eine Form des abgesicherten Modus startet. An dieser Stelle ist der Computer nicht das Klonen abgeschlossen. Ein Zustand möglicherweise geändert haben, und ein Zustand bleiben von den ursprünglichen Domänencontroller. Testszenario Sie folgendermaßen vor, um zu verstehen, welche Auswirkung es auf Ihrer Anwendung haben kann.  
  
Zum Auslösen eines Fehlers beim Klonen, versuchen Sie, einen Domänencontroller zu klonen, ohne diese Berechtigung, geklont zu werden. In diesem Fall der Computer wird nur haben die IP-Adressen und die Mehrzahl der Zustand von der ursprünglichen Domänencontroller immer noch. Weitere Informationen zu einer Domänencontroller Berechtigung, geklont zu werden, finden Sie unter [Schritt 1: erteilen Sie dem virtualisierten Quelldomänencontroller die Berechtigung, geklont zu werden](https://technet.microsoft.com/library/hh831734.aspx#bkmk4_grant_source).  
  
### <a name="pdc-emulator-cloning"></a>Beim Klonen des PDC-emulator  
Service und Anwendungsserver-Anbieter sollte dieses Szenario getestet werden, da bei einem weiteren Neustart vorhanden ist, wenn der PDC-Emulator geklont wird. Darüber hinaus erfolgt der Großteil der Klonvorgang unter einer temporären Identität auf den neuen Klon zu der PDC-Emulator während des Klonens interagieren können.  
  
### <a name="writable-versus-read-only-domain-controllers"></a>Beschreibbare im Vergleich zu Read-only-Domänencontroller  
Service und Anwendungsserver-Anbieter sollte getestet werden mit den gleichen Typ von Domänencontroller Klonen (d. h. auf einem beschreibbaren oder schreibgeschützter Domänencontroller), dass der Dienst für die Ausführung auf geplant ist.  
  


