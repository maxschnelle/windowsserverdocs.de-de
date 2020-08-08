---
ms.assetid: fde99b44-cb9f-49bf-b888-edaeabe6b88d
title: 'Testleitfaden: Klonen von virtualisierten Domänencontrollern für Anwendungsanbieter'
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: f1cb3db67e12e0d0b8947c22c5acc2b2ffc6f077
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87956697"
---
# <a name="virtualized-domain-controller-cloning-test-guidance-for-application-vendors"></a>Testleitfaden: Klonen von virtualisierten Domänencontrollern für Anwendungsanbieter

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

In diesem Thema wird erläutert, welche Anwendungshersteller in Erwägung gezogen werden sollten, um sicherzustellen, dass Ihre Anwendung nach Abschluss des Klonens des virtualisierten Domänen Controllers (DC) weiterhin erwartungsgemäß funktioniert. Dabei werden die Aspekte des Klon Prozesses behandelt, bei denen es sich um Anwendungsanbieter und Szenarios handelt, die möglicherweise zusätzliche Tests rechtfertigen Anwendungshersteller, die überprüft haben, ob Ihre Anwendung auf virtualisierten Domänen Controllern funktioniert, die geklont wurden, werden aufgefordert, den Namen der Anwendung im Inhalt der Community am Ende dieses Themas zusammen mit einem Link zur Website Ihres Unternehmens aufzulisten, auf der die Benutzer mehr über die Validierung erfahren können.

## <a name="overview-of-virtualized-dc-cloning"></a>Übersicht über das Klonen virtualisierter Domänen Controller
Der Prozess für das Klonen virtualisierter Domänen Controller wird ausführlich in [Einführung in Active Directory Domain Services (AD DS) Virtualisierung (Stufe 100)](../../introduction-to-active-directory-domain-services-ad-ds-virtualization-level-100.md) und [Technische Referenz für virtualisierte Domänen Controller (Level 300)](../../deploy/virtual-dc/virtualized-domain-controller-technical-reference--level-300-.md)beschrieben. Aus der Perspektive eines Anwendungs Herstellers sind dies einige Aspekte zu berücksichtigen, die bei der Bewertung der Auswirkungen des Klonens auf Ihre Anwendung zu berücksichtigen sind:

-   Der ursprüngliche Computer wird nicht zerstört. Sie verbleibt im Netzwerk und interagiert mit Clients. Im Gegensatz zu einem umbenennen, bei dem die DNS-Einträge des ursprünglichen Computers entfernt werden, verbleiben die ursprünglichen Datensätze für den Quell Domänen Controller.

-   Während des Klon Vorgangs wird der neue Computer zunächst für einen kurzen Zeitraum unter der Identität des alten Computers ausgeführt, bis der Klonprozess initiiert wird und die erforderlichen Änderungen vorgenommen werden. Anwendungen, die Datensätze über den Host erstellen, sollten sicherstellen, dass der geklonte Computer während des Klon Vorgangs keine Datensätze zum ursprünglichen Host überschreibt.

-   Das Klonen ist eine bestimmte Bereitstellungs Funktion ausschließlich für virtualisierte Domänen Controller und keine allgemeine Erweiterung zum Klonen anderer Server Rollen. Einige Server Rollen werden für das Klonen nicht unterstützt:

    -   Dynamic Host Configuration-Protokoll (DHCP)

    -   Active Directory-Zertifikatdienste (AD CS)

    -   Active Directory Lightweight Directory Services (ADLDS)

-   Im Rahmen des Klon Vorgangs wird die gesamte VM, die den ursprünglichen Domänen Controller darstellt, kopiert, sodass jeder Anwendungs Zustand auf diesem virtuellen Computer ebenfalls kopiert wird. Überprüfen Sie, ob die Anwendung an diese Änderung im Status des lokalen Hosts auf dem geklonten Domänen Controller angepasst ist oder ob ein Eingriff erforderlich ist, z. b. ein Neustart des Diensts.

-   Im Rahmen des Klonens erhält der neue Domänen Controller eine neue Computer Identität und stellt sich selbst als Replikat-DC in der Topologie bereit. Überprüfen Sie, ob die Anwendung von der Computer Identität abhängt, z. b. Name, Konto, sid usw. Wird es automatisch an die Änderung der Computer Identität im Klon angepasst? Wenn diese Anwendung Daten zwischenspeichert, müssen Sie sicherstellen, dass Sie sich nicht auf Computer Identitätsdaten verlassen, die zwischengespeichert werden können.

## <a name="what-is-interesting-for-application-vendors"></a>Was ist für Anwendungshersteller interessant?

### <a name="customdccloneallowlistxml"></a>CustomDCCloneAllowList.xml
Ein Domänen Controller, auf dem die Anwendung oder der Dienst ausgeführt wird, kann erst geklont werden, wenn die Anwendung bzw. der Dienst

-   Wird der CustomDCCloneAllowList.xml Datei mithilfe des Windows PowerShell-Cmdlets Get-addccloningexcludedapplicationlist hinzugefügt.

-Oder-

-   Vom Domänen Controller entfernt

Beim ersten Ausführen des Cmdlets "Get-addccloningexcludedapplicationlist" wird eine Liste der Dienste und Anwendungen zurückgegeben, die auf dem Domänen Controller ausgeführt werden, sich aber nicht in der Standardliste der Dienste und Anwendungen befinden, die für das Klonen unterstützt werden. Standardmäßig wird der Dienst oder die Anwendung nicht aufgelistet. Um den Dienst oder die Anwendung der Liste der Anwendungen und Dienste hinzuzufügen, die sicher geklont werden können, führt der Benutzer das Get-addccloningexcludedapplicationlist-Cmdlet erneut mit der Option-generatexml aus, um es der CustomDCCloneAllowList.xml-Datei hinzuzufügen. Weitere Informationen finden Sie unter [Schritt 2: Ausführen des Cmdlets "Get-addccloningexcludedapplicationlist](/powershell/module/addsadministration/get-addccloningexcludedapplicationlist)".

### <a name="distributed-system-interactions"></a>Verteilte System Interaktionen
In der Regel werden Dienste, die auf dem lokalen Computer isoliert sind, bei der Teilnahme am Klonen bestanden oder schlagen fehl Verteilte Dienste müssen sich für einen kurzen Zeitraum gleichzeitig mit zwei Instanzen des Host Computers im Netzwerk beschäftigen. Dies kann sich als eine Dienst Instanz erweisen, die versucht, Informationen von einem Partner System abzurufen, in dem sich der Klon als neuer Anbieter der Identität registriert hat. Oder beide Instanzen des dienstanzen können Informationen mit unterschiedlichen Ergebnissen zur gleichen Zeit in die AD DS Datenbank überführen. Beispielsweise ist es nicht deterministisch, mit welchem Computer kommuniziert wird, wenn sich zwei Computer mit dem Windows-Testtechnologie Dienst (WTT) im Netzwerk mit dem Domänen Controller befinden.

Für den verteilten DNS-Server Dienst vermeidet der Klon Vorgang sorgfältig das Überschreiben der DNS-Einträge des Quell Domänen Controllers, wenn der geklonte Domänen Controller mit einer neuen IP-Adresse beginnt.

Sie sollten sich nicht auf den Computer verlassen, um die alte Identität bis zum Ende des Klonens zu entfernen. Nachdem der neue Domänen Controller in den neuen Kontext herauf gestuft wurde, wählen Sie die Option systatp-Anbieter werden ausgeführt aus, um den zusätzlichen Status des Computers zu bereinigen. Beispielsweise können Sie an diesem Punkt die alten Zertifikate des Computers entfernen, und die kryptografiegeheimnisse, auf die der Computer zugreifen kann, werden geändert.

Der größte Faktor, der die zeitliche Steuerung des Klonens variiert, ist die Anzahl der Objekte, die vom PDC repliziert werden müssen. Ältere Medien erhöhen die Zeit, die zum Abschließen des Klonens benötigt wird.

Da der Dienst oder die Anwendung unbekannt ist, wird er noch nicht ausgeführt. Beim Klon Vorgang wird der Status von nicht-Windows-Diensten nicht geändert.

Außerdem hat der neue Computer eine andere IP-Adresse als der ursprüngliche Computer. Diese Verhaltensweisen können Nebenwirkungen auf Ihren Dienst oder Ihre Anwendung verursachen, abhängig davon, wie sich der Dienst oder die Anwendung in dieser Umgebung verhält.

## <a name="additional-scenarios-suggested-for-testing"></a>Weitere Szenarien, die für Tests vorgeschlagen werden

### <a name="cloning-failure"></a>Klon Fehler
Dienstanbieter sollten dieses Szenario testen, da der Computer beim Klonen nicht in den Verzeichnisdienst-Reparatur Modus (Directory Services Repair Mode, DSRM), eine Form des abgesicherten Modus wechselt. An diesem Punkt hat der Computer den Klon Vorgang nicht abgeschlossen. Möglicherweise hat sich ein Status geändert, und ein Status kann vom ursprünglichen Domänen Controller verbleiben. Testen Sie dieses Szenario, um zu verstehen, welche Auswirkungen es auf Ihre Anwendung haben kann.

Wenn Sie einen Klon Fehler auslösen möchten, versuchen Sie, einen Domänen Controller zu klonen, ohne ihm die Berechtigung zum Klonen zu erteilen. In diesem Fall hat der Computer nur die IP-Adressen geändert und hat weiterhin den Großteil seines Zustands vom ursprünglichen Domänen Controller. Weitere Informationen zum Erteilen der Berechtigung zum Klonen eines Domänen Controllers finden Sie unter [Schritt 1: gewähren der Berechtigung zum Klonen durch den virtualisierten Quell Domänen Controller](../../get-started/virtual-dc/virtualized-domain-controller-deployment-and-configuration.md).

### <a name="pdc-emulator-cloning"></a>Klonen des PDC-Emulators
Dienst-und Anwendungshersteller sollten dieses Szenario testen, da ein zusätzlicher Neustart erfolgt, wenn der PDC-Emulator geklont wird. Außerdem wird der Großteil des Klonens unter einer temporären Identität ausgeführt, damit der neue Klon während des Klon Vorgangs mit dem PDC-Emulator interagieren kann.

### <a name="writable-versus-read-only-domain-controllers"></a>Schreibgeschützte und schreibgeschützte Domänen Controller
Dienst-und Anwendungshersteller sollten das Klonen mithilfe desselben Domänen Controller Typs (d. h. auf einem beschreibbaren oder schreibgeschützten Domänen Controller) testen, auf dem der Dienst ausgeführt werden soll.
