---
title: Installieren von Windows Server Essentials in Migration MODE1
description: Beschreibt die Verwendung von Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fd7196ac-cfa6-46a5-ba77-6962b47a825e
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: dbbd9f7303995e1547e48aa9701467b45e4bad34
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80318998"
---
# <a name="install-windows-server-essentials-in-migration-mode1"></a>Installieren von Windows Server Essentials in Migration MODE1

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

In Ihrem Netzwerk, auf dem Windows Server Essentials ausgeführt wird, kann nur ein Server vorhanden sein, und dieser Server muss ein Domänen Controller für das Netzwerk sein.  
  
 Wenn Sie Windows Server Essentials im Migrations Modus installieren, führt der Installations-Assistent die folgenden Aufgaben aus:  
  
1.  Installiert und konfiguriert die Windows Server Essentials-Server Software auf dem Ziel Server.  
  
2.  Aktualisiert das Domänenschema auf die neueste Version.  
  
3.  Verknüpft den Zielserver mit der vorhandenen Domäne Der Quellserver und der Zielserver können beide Mitglieder derselben Domain sein, bis der Migrationsvorgang abgeschlossen ist. Nachdem die Migration abgeschlossen wurde, müssen Sie den Quellserver innerhalb von 21 Tagen aus dem Netzwerk entfernen.  
  
    > [!WARNING]
    >  Eine Fehlermeldung wird täglich innerhalb des 21-Tage-langen Aktivierungszeitraums in das Ereignisprotokoll hinzugefügt, bis Sie den Quellserver aus dem Netzwerk entfernen. Die Fehlermeldung lautet: „Bei der Überprüfung der FSMO-Rolle wurde eine Bedingung in der Umgebung festgestellt, die nicht mit der Lizenzierungsrichtlinie konform ist. Der Verwaltungsserver muss die Active Directory-Rollen des primären Domänencontrollers und des Domänennamenmasters aufweisen. Verschieben Sie diese Active Directory-Rollen jetzt zum Verwaltungsserver. Der Server wird automatisch heruntergefahren, wenn das Problem nicht innerhalb von 21 Tagen nach Feststellung dieser Bedingung behoben wird.“ Nach der Toleranzperiode von 21 Tagen wird der Quellserver heruntergefahren.  
  
4.  Er überträgt die Betriebsmasterrollen (auch als "Flexible Single Master Operations" oder FSMO bezeichnet) vom Quellserver auf den Zielserver. Betriebsmasterrollen sind spezialisierte Domänencontrolleraufgaben, die verwendet werden, wenn Standardmethoden für die Datenübertragung und Updates unzureichend sind. Wenn der Zielserver zum Domänencontroller wird, muss er die Betriebsmasterrollen haben.  
  
5.  Er konfiguriert den Zielserver als globalen Katalogserver. Der globale Katalogserver ist ein Domänencontroller, der ein verteiltes Datenrepository verwaltet. Er enthält eine durchsuchbare Teildarstellung jedes Objekts in jeder Domäne der Active Directory-Gesamtstruktur.  
  
6.  Konfiguriert den Zielserver als den Standortlizenzserver.  
  
##  <a name="install-windows-server-essentials-on-the-destination-server"></a><a name="BKMK_Install"></a>Installieren von Windows Server Essentials auf dem Ziel Server  
 Führen Sie das folgende Verfahren aus, um Windows Server Essentials im Migrations Modus auf dem Ziel Server zu installieren und zu konfigurieren.  
  
#### <a name="to-install-windows-server-essentials-on-the-destination-server"></a>So installieren Sie Windows Server Essentials auf dem Ziel Server  
  
1. Schalten Sie den Ziel Server ein, und fügen Sie Windows Server Essentials DVD1 in das DVD-Laufwerk ein. Wenn eine Meldung angezeigt wird, in der Sie gefragt werden, ob von einer CD oder DVD gestartet werden soll, drücken Sie dazu eine beliebige Taste.  
  
   > [!NOTE]
   >  Wenn der Ziel Server das Starten von einem USB-Speicherstick unterstützt, können Sie das **Windows 7 USB/DVD Download Tool** verwenden, um einen Start fähigen USB-Speicherstick aus der Windows Server Essentials-ISO-Datei zu erstellen. Mit einem USB-Speicherstick können Sie den Installationsvorgang deutlich beschleunigen, da Speichersticks Daten sehr viel schneller als DVD-ROM-Laufwerke lesen. Nach dem Erstellen eines startbaren USB-Speichersticks können Sie eine Antwortdatei zum Speicherstick hinzufügen. Sie können [das Windows 7 USB/DVD Download Tool](https://go.microsoft.com/fwlink/p/?LinkId=248282) kostenlos auf Microsoft Store Website herunterladen.  
  
   > [!NOTE]
   >  Wenn der Zielserver nicht von der DVD startet, starten Sie den Computer neu, und überprüfen Sie das BIOS-Setup, um sicherzustellen, dass **DVD-ROM** an erster Stelle in der Startreihenfolge aufgeführt ist. Weitere Informationen zum Ändern der Startreihenfolge im BIOS-Setup finden Sie in der Dokumentation des Hardwareherstellers.  
  
2. Klicken Sie auf **Neue Installation**.  
  
3. Wenn Sie eine interne Festplatte haben, die nicht in der Liste angezeigt wird, klicken Sie auf **Treiber laden**, und installieren Sie den erforderlichen Treiber, bevor Sie fortfahren.  
  
4. Aktivieren Sie das Kontrollkästchen, das überprüft, dass alle Dateien und Ordner auf Ihrer primären Festplatte gelöscht werden, und klicken Sie dann auf **Installieren**.  
  
5. Auf der Seite **Installationsmodus auswählen** klicken Sie auf **Servermigration**, und geben dann die erforderlichen Migrationsinformationen ein.  
  
6. Sobald die Meldung **Der Server wurde erfolgreich migriert** angezeigt wird, klicken Sie auf **Schließen**.  
  
   Nach Abschluss der Installation werden Sie automatisch mit dem Benutzerkonto und Kennwort des Administrators angemeldet, die Sie in der Antwortdatei für die Migration bereitgestellt haben.  
  
> [!NOTE]
>  Wenn Sie den Desktop bei der Installation von Windows Server Essentials entsperren möchten, verwenden Sie das integrierte Administrator Konto, und lassen Sie das Kennwort leer.  
  
##  <a name="verify-the-health-of-the-domain-controller"></a><a name="BKMK_VerifyTheHealthOfDC"></a>Überprüfen der Integrität des Domänen Controllers  
 Bevor Sie mit der Migration fortfahren, sollten Sie sicherstellen, dass der Domänen Controller und das Windows Server Essentials-Netzwerkfehler frei sind.  
  
 Die folgende Tabelle listet die Tools auf, die Sie für die Diagnose von Problemen auf Ihrem Zielserver, im Netzwerk oder in der Domäne verwenden können:  
  
|Tool|Beschreibung|  
|----------|-----------------|  
|Netdiag|Unterstützt Sie bei der Isolation von Netzwerk- und Verbindungsproblemen. Unter [Netdiag](https://go.microsoft.com/fwlink/?LinkId=217388)finden Sie weitere Informationen und können auch das Tool herunterladen.|  
|Dcdiag.exe|Analysiert den Zustand von Domänencontrollern in einer Gesamtstruktur oder einem Unternehmen und meldet Probleme, um Sie bei der Problembehandlung zu unterstützen. Unter [Dcdiag](https://go.microsoft.com/fwlink/?LinkId=217389)finden Sie weitere Informationen und können auch das Tool herunterladen.|  
|Repadmin.exe|Unterstützt Sie bei der Diagnose von Replikationsproblemen zwischen Domänencontrollern. Zur Ausführung dieses Tools sind Befehlszeilenparameter erforderlich. Unter [Repadmin](https://go.microsoft.com/fwlink/?LinkId=217387)finden Sie weitere Informationen und können auch das Tool herunterladen.|  
  
 Alle von diesen Tools erfassten Probleme sollten behoben werden, bevor Sie mit der Migration fortfahren.  
  
> [!NOTE]
>  Wenn Sie beabsichtigen, eine e-Mail zu einem anderen lokalen Exchange-Server zu migrieren, finden Sie unter [integrieren eines lokalen Exchange-Servers mit Windows Server Essentials](../manage/Integrate-an-On-Premises-Exchange-Server-with-Windows-Server-Essentials.md) Informationen zum Einrichten Ihres lokalen Exchange-Servers.
