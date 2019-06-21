---
title: Problembehandlung für Einstellungen für Einstiegspunkte und Domänencontroller
description: Dieses Thema ist Teil des Handbuchs bereitstellen mehrere RAS-Server in einer Bereitstellung für mehrere Standorte in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b12dd0e8-1d80-4d4b-bb45-586f19d17ef0
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 5e7e09a6715df22882c8a88aedf95a5158dd2a0d
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67280916"
---
# <a name="troubleshooting-setting-the-entry-point-domain-controller"></a>Problembehandlung für Einstellungen für Einstiegspunkte und Domänencontroller

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Dieses Thema enthält Informationen zum Beheben von Problemen mit dem Befehl `Set-DAEntryPointDC`. Überprüfen Sie, ob das Windows-Ereignisprotokoll ein Ereignis mit der ID 10065 enthält, um sicherzustellen, dass der Fehler mit den Einstellungen für Einstiegspunkte und Domänencontroller zusammenhängt.  
  
## <a name="SaveGPOSettings"></a>Server-GPO-Einstellungen werden gespeichert.  
**Fehler**. Fehler beim Speichern der Remotezugriffseinstellungen GPO < GPO_name >.  
  
Um diesen Fehler zu beheben, finden Sie in Server-GPO-Einstellungen werden gespeichert.  
  
## <a name="remote-access-is-not-configured"></a>Nicht konfigurierter Remotezugriff  
**Fehler**. Remotezugriff ist auf < Servername > nicht konfiguriert. Geben Sie den Namen eines Servers an, der zu einer Bereitstellung für mehrere Standorte gehört.  
  
oder  
  
Remotezugriff ist auf dem Server < Servername > nicht konfiguriert. Geben Sie einen Computer an, auf dem DirectAccess aktiviert ist.  
  
**Ursache**  
  
Remotezugriff ist auf dem mit dem *ComputerName*-Parameter angegebenen Computer nicht konfiguriert.  
  
Das Cmdlet `Set-DaEntryPointDC` ist nur auf Servern verfügbar, die zu einer konfigurierten Bereitstellung für mehrere Standorte gehören.  
  
**Lösung**  
  
Führen Sie den Befehl aus, und geben Sie im *ComputerName*-Parameter den Namen des Servers an, der bereits als Teil der Bereitstellung für mehrere Standorte konfiguriert ist.  
  
## <a name="multisite-is-not-enabled"></a>Bereitstellung für mehrere Standorte ist nicht aktiviert  
**Fehler**. Eine Bereitstellung für mehrere Standorte vor dem Ausführen dieses Vorgangs muss aktiviert werden. Verwenden Sie hierzu das Cmdlet `Enable-DAMultiSite`.  
  
**Ursache**  
  
Die Funktionen für mehrere Standorte sind auf dem Server, der durch den Parameter *ComputerName* angegeben wird, nicht aktiviert.  
  
Das Cmdlet `Set-DaEntryPointDC` ist nur auf Servern verfügbar, die zu einer konfigurierten Bereitstellung für mehrere Standorte gehören.  
  
**Lösung**  
  
Führen Sie den Befehl aus, und geben Sie im *ComputerName*-Parameter den Namen des Servers an, der bereits als Teil der Bereitstellung für mehrere Standorte konfiguriert ist.  
  
## <a name="entry-point-and-domain-controller-not-provided-in-cmdlet"></a>Einstiegspunkt und Domänencontroller wurden nicht im Cmdlet angegeben  
Das Cmdlet `Set-DaEntryPointDC` bietet Ihnen die Möglichkeit, den zugeordneten Domänencontroller für verschiedene Einstiegspunkte zu ändern, z. B. wenn ein bestimmter Domänencontroller nicht mehr verfügbar ist. Sie können einen spezifischen Einstiegspunkt zur Verwendung eines anderen Domänencontrollers aktualisieren oder alle Einstiegspunkte mit einem bestimmten Domänencontroller zur Verwendung eines neuen Domänencontrollers aktualisieren. In ersten Fall sollten Sie den zu aktualisierenden Einstiegspunkt mit dem *EntryPointName*-Parameter angeben. In zweiten Fall sollten Sie den zu ersetzenden Domänencontroller mit dem *ExistingDC*-Parameter angeben. Sie können nur einen dieser Parameter angeben.  
  
**Fehler**. Ohne erforderliche Parameter wurden angegeben. Geben Sie einen Einstiegspunktnamen oder den Namen eines vorhandenen Domänencontrollers an.  
  
oder  
  
Für das Cmdlet `Set-DaEntryPointDC` fehlen alle erforderlichen Parameter.  
  
**Ursache**  
  
Die Parameter *EntryPointName* oder *ExistingDC* wurden nicht angegeben oder es wurden beide Parameter für das Cmdlet `Set-DaEntryPointDC` angegeben.  
  
**Lösung**  
  
Führen Sie den Befehl aus, und geben Sie dabei entweder den *EntryPointName*-Parameter oder den *ExistingDC*-Parameter an.  
  
## <a name="could-not-locate-domain-controller"></a>Domänencontroller wurde nicht gefunden  
**Fehler**. Nicht möglich, einen neuen Domänencontroller automatisch gesucht werden soll. Versuchen Sie es später noch einmal, oder überprüfen Sie die Einstellungen des Domänencontrollers.  
  
**Ursache**  
  
Der mit dem *ComputerName*-Parameter angegebene Computer ist nicht über RPC erreichbar, oder die Domäne enthält keine verfügbaren beschreibbaren Domänencontroller.  
  
**Lösung**  
  
Stellen Sie sicher, dass der Remotecomputer über RPC erreichbar und ein beschreibbarer Domänencontroller für die Domäne verfügbar ist. Falls ein beschreibbarer Domänencontroller für die Domäne verfügbar ist, können Sie seinen Namen auch explizit mit dem *NewDC*-Parameter angeben.  
  
## <a name="could-not-connect-to-domain-controller"></a>Es konnte keine Verbindung mit dem Domänencontroller hergestellt werden  
  
-   **Problem 1**  
  
    **Fehler**. Der Domänencontroller < Domänencontroller > kann nicht erreicht werden. Überprüfen Sie die Netzwerkkonnektivität und die Serververfügbarkeit.  
  
    **Ursache**  
  
    Der Domänencontroller ist nicht erreichbar. Dieses Problem tritt nur auf, wenn der Administrator mit den Parametern *NewDC* oder *ExistingDC* einen Domänencontroller angibt.  
  
    **Lösung**  
  
    Stellen Sie sicher, dass der Name des Domänencontrollers richtig geschrieben ist. Falls Sie einen Kurznamen als Namen angegeben haben, verwenden Sie den vollqualifizierten Domänennamen (FQDN), und versuchen Sie es noch einmal.  
  
-   **Problem 2**  
  
    **Fehler**. Der Domänencontroller < Domänencontroller > kann nicht kontaktiert werden.  
  
    **Ursache**  
  
    Möglicherweise liegt ein Netzwerkproblem vor, aufgrund dessen der mit dem *NewDC*-Parameter angegebene Domänencontroller oder ein anderer vorhandener Domänencontroller in der Konfiguration nicht erreicht werden kann.  
  
    **Lösung**  
  
    Stellen Sie sicher, dass der Name des Domänencontrollers richtig geschrieben ist, dass er aktiv und beschreibbar ist und eine Vertrauensstellung zwischen dem Domänencontroller und der Domäne besteht.  
  
-   **Problem 3**  
  
    **Fehler**. Domänencontroller < Domänencontroller > kann nicht für %2! s! nicht erreicht werden.  
  
    **Ursache**  
  
    Um die Einheitlichkeit der Konfiguration in einer Bereitstellung für mehrere Standorte zu wahren, müssen Sie sicherstellen, dass jedes GPO von einem einzigen Domänencontroller verwaltet wird. Wenn der Domänencontroller, der einen Einstiegspunkt-Server-Gruppenrichtlinienobjekt verwaltet nicht verfügbar ist, können nicht RAS-Konfigurationseinstellungen gelesen oder geändert werden.  
  
    **Lösung**  
  
    Führen Sie das Verfahren "So ändern den Domänencontroller, die Server-GPOs verwaltet", die in beschriebenen [2.4. Konfigurieren der Gruppenrichtlinienobjekte](assetId:///b1960686-a81e-4f48-83f1-cc4ea484df43#ConfigGPOs).  
  
-   **Problem 4**  
  
    **Fehler**. Der primäre Domänencontroller in die Domäne < Domänenname > kann nicht erreicht werden.  
  
    **Ursache**  
  
    Um die Einheitlichkeit der Konfiguration in einer Bereitstellung für mehrere Standorte zu wahren, müssen Sie sicherstellen, dass jedes GPO von einem einzigen Domänencontroller verwaltet wird. Client-GPOs werden auf dem primären Domänencontroller verwaltet. Wenn der primäre Domänencontroller nicht verfügbar ist, können die RAS-Konfigurationseinstellungen nicht gelesen oder geändert werden.  
  
    **Lösung**  
  
    Folgen Sie das Verfahren "So übertragen die PDC-Emulatorrolle" in [2.4. Konfigurieren der Gruppenrichtlinienobjekte](assetId:///b1960686-a81e-4f48-83f1-cc4ea484df43#ConfigGPOs).  
  
## <a name="read-only-domain-controller"></a>Schreibgeschützter Domänencontroller  
**Fehler**. Der Domänencontroller < Domänencontroller > ist schreibgeschützt. Geben Sie einen Domänencontroller an, der nicht schreibgeschützt ist.  
  
**Ursache**  
  
Der mit dem *NewDC*-Parameter angegebene Domänencontroller ist schreibgeschützt.  
  
**Lösung**  
  
Bei der Verwendung von `Set-DAEntryPointDC` wird der *NewDC*-Parameter zum Aktualisieren des zugeordneten Domänencontrollers eines bestimmten Einstiegspunkts oder zum Aktualisieren aller zugeordneten Einstiegspunkte eines Domänencontrollers verwendet. Der neue Domänencontroller muss daher beschreibbar sein. Geben Sie einen beschreibbaren Domänencontroller im *NewDC*-Parameter an, und versuchen Sie es noch einmal.  
  
## <a name="cannot-retrieve-gpo"></a>GPO kann nicht abgerufen werden  
  
-   **Problem 1**  
  
    **Fehler**. GPO < GPO_name > auf < vorheriger_domänencontroller > "Domänencontroller" kann nicht von Domänencontroller < neuer_domänencontroller > abgerufen werden, da sie nicht in derselben Domäne sind.  
  
    **Ursache**  
  
    Der RAS-Server und der Domänencontroller befinden sich nicht in derselben Domäne. Daher kann das GPO nicht abgerufen werden.  
  
    **Lösung**  
  
    Falls Sie versucht haben, einen bestimmten Einstiegspunkt zu aktualisieren, vergewissern Sie sich, dass sich der neue Domänencontroller in derselben Domäne befindet wie der Einstiegspunktserver. Falls Sie versucht haben, einen bestimmten Domänencontroller zu aktualisieren, vergewissern Sie sich, dass sich der neue Domänencontroller in derselben Domäne befindet wie der, den Sie ersetzen möchten.  
  
-   **Problem 2**  
  
    **Fehler**. GPO < GPO_name > auf < vorheriger_domänencontroller > "Domänencontroller" kann nicht von Domänencontroller < neuer_domänencontroller > abgerufen werden. Warten Sie, bis die Domänenreplikation abgeschlossen ist, und wiederholen Sie den Vorgang.  
  
    **Ursache**  
  
    Wenn Sie den Domänencontroller für einen Einstiegspunkt aktualisieren, versucht das Cmdlet, das Server-GPO vom neuen Domänencontroller zu lesen. Das GPO wird jedoch nicht auf dem neuen Domänencontroller gefunden, weil es noch nicht repliziert wurde.  
  
    **Lösung**  
  
    Das Server-GPO ist nicht auf dem neuen Domänencontroller vorhanden. Stellen Sie sicher, dass die GPOs erfolgreich zum neuen Domänencontroller repliziert wurden, und versuchen Sie es noch einmal.  
  
-   **Problem 3**  
  
    **Fehler**. Sie sind nicht berechtigt GPO < GPO_name > auf.  
  
    **Ursache**  
  
    Wenn Sie den Domänencontroller für einen Einstiegspunkt aktualisieren, versucht das Cmdlet, das Server-GPO vom neuen Domänencontroller zu lesen. Das GPO kann jedoch nicht vom neuen Domänencontroller gelesen werden, weil Sie nicht über die entsprechenden Berechtigungen verfügen.  
  
    **Lösung**  
  
    Das GPO ist auf dem Domänencontroller vorhanden, kann aber nicht gelesen werden. Stellen Sie sicher, dass Sie über die erforderlichen Berechtigungen verfügen, und versuchen Sie es noch einmal.  
  
## <a name="entry-point-not-part-of-multisite-deployment"></a>Einstiegspunkt ist nicht Teil der Bereitstellung für mehrere Standorte  
**Fehler**. Einstiegspunkt < Einstiegspunktname > ist nicht Teil der Bereitstellung für mehrere Standorte. Geben Sie einen anderen Wert an.  
  
**Ursache**  
  
Der angegebene Einstiegspunktname wurde nicht gefunden.  
  
**Lösung**  
  
Stellen Sie sicher, dass der Name des Einstiegspunkts richtig geschrieben ist und GPOs zu den erforderlichen Domänencontrollern repliziert wurden, und versuchen Sie es noch einmal. Verwenden Sie `Get-DAEntryPointDC`, um den zugewiesenen Domänencontroller für jeden Einstiegspunkt anzuzeigen.  
  
## <a name="remote-access-server-settings"></a>Einstellungen des RAS-Servers  
  
-   **Problem 1**  
  
    **Fehler**. Server < Servername > in < Einstiegspunktname >-Einstiegspunkt kann nicht zugegriffen werden.  
  
    **Ursache**  
  
    Wenn Sie den Domänencontroller für einen Einstiegspunkt aktualisieren, versucht das Cmdlet, den Domänencontroller für den Einstiegspunkt von allen relevanten RAS-Servern zu lesen und zu schreiben. Das Cmdlet konnte die Daten von mindestens einem RAS-Server nicht lesen.  
  
    **Lösung**  
  
    Stellen Sie sicher, dass alle relevanten RAS-Server aktiv sind und Sie auf allen Servern über lokale Administratorberechtigungen verfügen, und versuchen Sie es noch einmal.  
  
-   **Problem 2**  
  
    **Fehler**. Einstellungen können nicht in der Registrierung auf Server < Servername > Einstiegspunkt < Einstiegspunktname > gespeichert.  
  
    **Ursache**  
  
    Wenn Sie den Domänencontroller für einen Einstiegspunkt aktualisieren, versucht das Cmdlet, den Domänencontroller für den Einstiegspunkt von allen relevanten RAS-Servern zu lesen und zu schreiben. Das Cmdlet konnte die Daten auf mindestens einen RAS-Server nicht schreiben.  
  
    **Lösung**  
  
    Stellen Sie sicher, dass alle relevanten RAS-Server aktiv sind und Sie auf allen Servern über lokale Administratorberechtigungen verfügen, und versuchen Sie es noch einmal.  
  
-   **Problem 3**  
  
    **Fehler**. GPO-Aktualisierungen können nicht auf < Servername > angewendet werden. Die Änderungen werden erst nach der nächsten Richtlinienaktualisierung wirksam.  
  
    **Ursache**  
  
    Bei der Verwendung des Cmdlets `Set-DAEntryPointDC` ist der angegebene *ComputerName*-Parameter ein RAS-Server an einem anderen Einstiegspunkt als dem, der der Bereitstellung für mehrere Standorte zuletzt hinzugefügt wurde.  
  
    **Lösung**  
  
    Alle Server, die nicht aktualisiert wurden, können mithilfe des **Konfigurationsstatus** im **DASHBOARD** der Remotezugriffs-Verwaltungskonsole angezeigt werden. Dieser Fehler verursacht keine Funktionsprobleme. Sie können jedoch auf allen nicht aktualisierten Servern `gpupdate /force` ausführen, damit der Konfigurationsstatus sofort aktualisiert wird.  
  
## <a name="problem-resolving-fqdn"></a>Problem bei der Auflösung des vollqualifizierten Domänennamens (FQDN)  
**Fehler**. Server < Servername > in < Einstiegspunktname >-Einstiegspunkt kann nicht zugegriffen werden.  
  
**Ursache**  
  
Beim Abrufen der Liste zu ändernder DirectAccess-Server konnte das Cmdlet den vollqualifizierten Domänennamen (FQDN) eines der Server nicht aus der Computer-SID auflösen.  
  
**Lösung**  
  
Der in der Fehlermeldung angegebene Einstiegspunkt ist einem Domänencontroller zugeordnet. Stellen Sie sicher, dass der Domänencontroller für den Einstiegspunkt verfügbar ist. Falls der Computer, zu dem die angegebene SID gehört, aus der Domäne entfernt wurde, ignorieren Sie die Meldung, und entfernen Sie den Server aus der Bereitstellung für mehrere Standorte.  
  
## <a name="no-entry-points-to-update"></a>Keine zu aktualisierenden Einstiegspunkte vorhanden  
**Empfangene Warnung**. Domänencontrollereinstellungen wurden nicht geändert werden. Wenn Ihrer Meinung nach Änderungen erforderlich sind, stellen Sie sicher, dass die Cmdlet-Parameter richtig konfiguriert sind und GPOs auf den erforderlichen Domänencontrollern repliziert werden.  
  
**Ursache**  
  
Wenn das Cmdlet `Set-DaEntryPointDC` mit dem *ExistingDC*-Parameter aufgerufen wird, überprüft DirectAccess alle Einstiegspunkte und aktualisiert die Einstiegspunkte, die dem angegebenen Domänencontroller zugeordnet sind. Es ist jedoch kein Einstiegspunkt mit dem angegebenen *ExistingDC* vorhanden.  
  
**Lösung**  
  
Verwenden Sie das Cmdlet `Get-DAEntryPointDC`, um eine Liste der Einstiegspunkte und der zugeordneten Domänencontroller anzuzeigen. Falls Änderungen vorgenommen wurden, stellen Sie sicher, dass die Cmdlet-Parameter richtig geschrieben sind und die GPOs zu den erforderlichen Domänencontrollern repliziert wurden, und versuchen Sie es noch einmal.  
  


