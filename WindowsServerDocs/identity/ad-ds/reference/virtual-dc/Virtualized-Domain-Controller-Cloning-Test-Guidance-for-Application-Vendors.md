---
ms.assetid: fde99b44-cb9f-49bf-b888-edaeabe6b88d
title: 'Testleitfaden: Klonen von virtualisierten Domänencontrollern für Anwendungsanbieter'
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 0b2303bc837cdaf9f6e7ebd4b3ccbf6c66aa7ad2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59879341"
---
# <a name="virtualized-domain-controller-cloning-test-guidance-for-application-vendors"></a>Testleitfaden: Klonen von virtualisierten Domänencontrollern für Anwendungsanbieter

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

In diesem Thema wird erläutert, was Anbieter von Anwendungen berücksichtigen sollten, um sicherzustellen, dass ihre Anwendung weiterhin funktioniert wie erwartet, nachdem der Prozess für das Klonen virtualisierter Domänencontroller (DC) abgeschlossen ist. Hierin sind die Aspekte des klonprozesses, Anbieter von Interesse sind Anwendungen und Szenarien, in denen möglicherweise zusätzliche Tests zu rechtfertigen. Anbieter von Anwendungen, die überprüft haben, dass ihre Anwendung auf virtuellen Domänencontrollern funktioniert, die geklont wurden, werden aufgefordert, den Namen der Anwendung in der Community-Inhalt am Ende dieses Themas zusammen mit einem Link zur Liste Ihrer Website der Organisation, in denen Benutzer mehr über die Validierung erfahren können.  
  
## <a name="overview-of-virtualized-dc-cloning"></a>Übersicht über die virtualisierte Domänencontroller Klonen  
Der virtuelle Domänencontroller, der Prozess für das Klonen wird ausführlich beschrieben [Einführung in die Active Directory Domain Services (AD DS) Virtualization (Level 100)](https://technet.microsoft.com/library/hh831734.aspx) und [Domäne-Controller mit technischen virtualisiert Referenz (Stufe 300)](https://technet.microsoft.com/library/jj574214.aspx). Aus Sicht des Anbieters, der eine Anwendung sind dies einige Überlegungen zu berücksichtigen, bei der Bewertung der Auswirkungen des Klonens zu Ihrer Anwendung:  
  
-   Der ursprüngliche Computer wird nicht zerstört. Es bleibt im Netzwerk, die Interaktion mit Clients. Im Gegensatz zu einer Umbenennung, in denen die DNS-Einträge des ursprünglichen Computers entfernt werden, bleiben die ursprünglichen Datensätzen für die Quell-Domänencontroller.  
  
-   Während des Klonens wird der neue Computer ursprünglich für einen kurzen Zeitraum unter der Identität des vom alten Computer ausgeführt, bis der Prozess für das Klonen initiiert wird, und die erforderlichen Änderungen führt. Anwendungen, die Datensätze, die über den Host erstellen sorgen dafür, dass der geklonte Computer Datensätze über dem ursprünglichen Host nicht während des Klonens überschrieben wird.  
  
-   Das Klonen ist eine bestimmte Bereitstellung ausschließlich für virtualisierte Domänencontroller, kein allgemeiner Erweiterung anderer Serverrollen zu klonen. Einige Serverrollen werden insbesondere nicht für das Klonen unterstützt:  
  
    -   Dynamic Host Configuration-Protokoll (DHCP)  
  
    -   Active Directory-Zertifikatdienste (AD CS)  
  
    -   Active Directory Lightweight Directory Services (ADLDS)  
  
-   Als Teil des klonprozesses wird die gesamte VM, die den ursprünglichen DC darstellt kopiert, sodass auch alle Anwendungszustand auf diesem virtuellen Computer kopiert wird. Überprüfen Sie, dass die Anwendung an die Änderung des Status des lokalen Hosts auf dem geklonten Domänencontroller, anpasst, oder wenn Eingreifen erforderlich ist, z. B. ein Neustart des Diensts ist.  
  
-   Als Teil des Klonens erhält der neue Domänencontroller eine neue Computeridentität und Bestimmungen selbst als einen Replikat-DC in der Topologie. Überprüfen Sie, ob die Computeridentität z. B. Name, Konto, SID, und So weiter die Anwendung abhängig. Anpassen es automatisch auf die Änderung der Identität des Computers auf dem Klon? Wenn die Anwendung Daten zwischengespeichert werden, stellen Sie sicher, dass es nicht auf den Computer Identitätsdaten abhängig ist, die zwischengespeichert werden kann.  
  
## <a name="what-is-interesting-for-application-vendors"></a>Was ist für Anbieter von Anwendungen?  
  
### <a name="customdccloneallowlistxml"></a>CustomDCCloneAllowList.xml  
Ein Domänencontroller, der Ihre Anwendung oder Ihr Dienst ausgeführt wird kann nicht geklont werden, bis die Anwendung oder Dienst ist entweder:  
  
-   Die Datei %% amp;quot;customdccloneallowlist.XML%%amp;quot; hinzugefügt, mit dem Get-ADDCCloningExcludedApplicationList Windows PowerShell-cmdlet  
  
– Oder –  
  
-   Vom Domänencontroller entfernt  
  
Der ersten Ausführung der Benutzer das Cmdlet Get-ADDCCloningExcludedApplicationList gibt es eine Liste der Dienste und Anwendungen, die auf dem Domänencontroller ausgeführt werden, jedoch sind nicht in die Standardliste der Dienste und Anwendungen, die für das Klonen unterstützt werden. Standardmäßig wird Ihr Dienst oder diese Anwendung nicht aufgeführt werden. Zum Hinzufügen von Ihrem Dienst oder Anwendung in die Liste der Anwendungen und Dienste, die sicher sein können geklont, die Benutzer ausgeführt wird, die file-Get-ADDCCloningExcludedApplicationList-Cmdlet erneut mit der Option – GenerateXML, damit er zu CustomDCCloneAllowList.xml hinzugefügt. Weitere Informationen finden Sie unter [Schritt2: Führen Sie Get-ADDCCloningExcludedApplicationList Cmdlet](https://technet.microsoft.com/library/hh831734.aspx#bkmk6_run_get_addccloningexcludedapplicationlist_cmdlet).  
  
### <a name="distributed-system-interactions"></a>Verteiltes System Interaktionen  
In der Regel Dienste, die auf dem lokalen Computer isoliert entweder erfolgreich oder Fehler beim Klonen beteiligt. Verteilte Dienste müssen bedenken, die gleichzeitig mit zwei Instanzen des Host-Computers im Netzwerk für einen kurzen Zeitraum sein. Dies kann manifest als eine Dienstinstanz, die versuchen, das Abrufen von Informationen von einem Partnersystem, auf dem der Klon als der Identität des neuen Anbieter registriert. Oder beide Instanzen des Diensts möglicherweise push-Informationen in AD DS-Datenbank zur gleichen Zeit mit unterschiedlichen Ergebnissen. Beispielsweise ist es nicht deterministisch, mit welchem Computer kommuniziert werden wird, wenn zwei Computer, auf denen Windows testen WTT (Technologies)-Dienst auf dem Netzwerk mit dem Domänencontroller befinden.  
  
Für den verteilten DNS-Serverdienst vermeidet der Klonvorgang sorgfältig, überschreiben die DNS-Einträge dem Quelldomänencontroller beim Start des geklonten Domänencontrollers mit einer neuen IP-Adresse.  
  
Sie sollten nicht auf dem Computer zum Entfernen aller die alte Identität bis zum Ende des Klonens verlassen. Wählen Sie der neuen Domänencontroller in der neue Kontext höher gestuft worden ist, Sysprep-Anbieter ausgeführt werden, um den zusätzlichen Zustand des Computers zu bereinigen. Beispielsweise ist es an diesem Punkt werden die alten Zertifikate des Computers entfernt, und die Kryptografie-Geheimnisse, die auf der Computer zugreifen kann geändert werden.  
  
Der wichtigste Faktor ist, der die zeitplanung für das Klonen abhängig ist, wie viele Objekte vorhanden sind, von den PDC zu replizieren. Ältere Media erhöht den Zeitaufwand für die vollständige klonen.  
  
Da es sich bei Ihrem Dienst oder Anwendung unbekannt ist, wird es weiterhin ausgeführt. Der Klonvorgang ändert nicht den Status der nicht-Windows-Dienste.  
  
Darüber hinaus hat der neue Computer eine andere IP-Adresse als der ursprüngliche Computer. Dieses Verhalten können Nebeneffekte zu Ihrem Dienst oder die Anwendung wird je nach dem Dienst oder eine Anwendung in dieser Umgebung Verhalten führen.  
  
## <a name="additional-scenarios-suggested-for-testing"></a>Zusätzliche Szenarien, die für Tests empfohlen.  
  
### <a name="cloning-failure"></a>Fehler beim Klonen  
Dienstanbietern Testen dieses Szenarios sollten, da beim Klonen tritt der Computer in Directory Services Repair-Wiederherstellungsmodus (DSRM), eine Form des abgesicherten Modus gestartet wird. An diesem Punkt wurde der Computer nicht das Klonen abgeschlossen. Kann ein Status sich geändert haben, und ein Zustand, der von der ursprünglichen Domäne bleiben kann. Testen Sie dieses Szenario, um zu verstehen, welche Auswirkungen es auf Ihre Anwendung auswirken kann.  
  
Zum Auslösen eines Fehlers beim Klonen, versuchen Sie es auf einen Domänencontroller zu klonen, ohne das Erteilen der Berechtigung, geklont zu werden. In diesem Fall der Computer nur mehr IP-Adressen und immer noch über die meisten seinen Zustand aus dem ursprünglichen Domänencontroller. Weitere Informationen zum Gewähren von einer Domäne-Controller-Berechtigung, geklont zu werden, finden Sie unter [Schritt 1: Gewähren Sie dem virtualisierten Quelldomänencontroller die Berechtigung, geklont zu werden](https://technet.microsoft.com/library/hh831734.aspx#bkmk4_grant_source).  
  
### <a name="pdc-emulator-cloning"></a>Klonen der PDC-emulator  
Dienst- und Lieferanten Testen dieses Szenarios sollten, da bei einem weiteren Neustart vorhanden ist, wenn der PDC-Emulator geklont wird. Darüber hinaus wird die Mehrheit der Klonen in eine temporäre Identität zu dem neuen Klon für die Interaktion mit dem PDC-Emulator während des Klonvorgangs ausgeführt.  
  
### <a name="writable-versus-read-only-domain-controllers"></a>Im Vergleich zu schreibgeschützten Domänencontrollern beschreibbaren  
Dienst- und Lieferanten sollten testen, Klonen die gleiche Art von Domänencontroller mit (d. h. auf einem Domänencontroller beschreibbar oder schreibgeschützt) Dienst geplant ist, für die Ausführung auf.  
  


