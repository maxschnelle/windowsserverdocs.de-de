---
title: Installieren von Windows Server Essentials in Migration Modus 1
description: Beschreibt, wie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fd7196ac-cfa6-46a5-ba77-6962b47a825e
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 74c40cc0f06d73a922a3d7fb819f7e71b47ac088
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66432962"
---
# <a name="install-windows-server-essentials-in-migration-mode1"></a>Installieren von Windows Server Essentials in Migration Modus 1

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Sie können veranlassen, dass nur ein Server in Ihrem Netzwerk, auf denen Windows Server Essentials ausgeführt wird, und dieser Server muss ein Domänencontroller für das Netzwerk sein.  
  
 Wenn Sie Windows Server Essentials im Migrationsmodus installieren, führt der Installations-Assistenten die folgenden Aufgaben aus:  
  
1.  Installiert und konfiguriert die Windows Server Essentials-Server-Software auf dem Zielserver.  
  
2.  Aktualisiert das Domänenschema auf die neueste Version.  
  
3.  Verknüpft den Zielserver mit der vorhandenen Domäne Der Quellserver und der Zielserver können beide Mitglieder derselben Domain sein, bis der Migrationsvorgang abgeschlossen ist. Nachdem die Migration abgeschlossen wurde, müssen Sie den Quellserver innerhalb von 21 Tagen aus dem Netzwerk entfernen.  
  
    > [!WARNING]
    >  Eine Fehlermeldung wird täglich innerhalb des 21-Tage-langen Aktivierungszeitraums in das Ereignisprotokoll hinzugefügt, bis Sie den Quellserver aus dem Netzwerk entfernen. Die Fehlermeldung lautet: „Bei der Überprüfung der FSMO-Rolle wurde eine Bedingung in der Umgebung festgestellt, die nicht mit der Lizenzierungsrichtlinie konform ist. Der Verwaltungsserver muss die Active Directory-Rollen des primären Domänencontrollers und des Domänennamenmasters aufweisen. Verschieben Sie diese Active Directory-Rollen jetzt zum Verwaltungsserver. Der Server wird automatisch heruntergefahren, wenn das Problem nicht innerhalb von 21 Tagen nach Feststellung dieser Bedingung behoben wird.“ Nach der Toleranzperiode von 21 Tagen wird der Quellserver heruntergefahren.  
  
4.  Er überträgt die Betriebsmasterrollen (auch als "Flexible Single Master Operations" oder FSMO bezeichnet) vom Quellserver auf den Zielserver. Betriebsmasterrollen sind spezialisierte Domänencontrolleraufgaben, die verwendet werden, wenn Standardmethoden für die Datenübertragung und Updates unzureichend sind. Wenn der Zielserver zum Domänencontroller wird, muss er die Betriebsmasterrollen haben.  
  
5.  Er konfiguriert den Zielserver als globalen Katalogserver. Der globale Katalogserver ist ein Domänencontroller, der ein verteiltes Datenrepository verwaltet. Er enthält eine durchsuchbare Teildarstellung jedes Objekts in jeder Domäne der Active Directory-Gesamtstruktur.  
  
6.  Konfiguriert den Zielserver als den Standortlizenzserver.  
  
##  <a name="BKMK_Install"></a> Installieren von Windows Server Essentials auf dem Zielserver  
 Führen Sie zum Installieren und Konfigurieren von Windows Server Essentials im Migrationsmodus auf dem Zielserver, die folgenden Schritte aus.  
  
#### <a name="to-install-windows-server-essentials-on-the-destination-server"></a>So installieren Sie Windows Server Essentials auf dem Zielserver  
  
1. Aktivieren Sie auf dem Zielserver aus, und fügen Sie Windows Server Essentials-DVD1 in das DVD-Laufwerk. Wenn eine Meldung angezeigt wird, in der Sie gefragt werden, ob von einer CD oder DVD gestartet werden soll, drücken Sie dazu eine beliebige Taste.  
  
   > [!NOTE]
   >  Wenn der Zielserver das Starten von einem USB-Flashlaufwerk unterstützt, können Sie die **Windows 7 USB/DVD Download Tool** um einen startbaren USB-Speicherstick aus der Windows Server Essentials-ISO-Datei zu erstellen. Mit einem USB-Speicherstick können Sie den Installationsvorgang deutlich beschleunigen, da Speichersticks Daten sehr viel schneller als DVD-ROM-Laufwerke lesen. Nach dem Erstellen eines startbaren USB-Speichersticks können Sie eine Antwortdatei zum Speicherstick hinzufügen. Sie können [Herunterladen der Windows 7 USB/DVD Download Tool](https://go.microsoft.com/fwlink/p/?LinkId=248282) kostenlos von Microsoft Store-Website.  
  
   > [!NOTE]
   >  Wenn der Zielserver nicht von der DVD startet, starten Sie den Computer neu, und überprüfen Sie das BIOS-Setup, um sicherzustellen, dass **DVD-ROM** an erster Stelle in der Startreihenfolge aufgeführt ist. Weitere Informationen zum Ändern der Startreihenfolge im BIOS-Setup finden Sie in der Dokumentation des Hardwareherstellers.  
  
2. Klicken Sie auf **Neue Installation**.  
  
3. Wenn Sie eine interne Festplatte haben, die nicht in der Liste angezeigt wird, klicken Sie auf **Treiber laden**, und installieren Sie den erforderlichen Treiber, bevor Sie fortfahren.  
  
4. Aktivieren Sie das Kontrollkästchen, das überprüft, dass alle Dateien und Ordner auf Ihrer primären Festplatte gelöscht werden, und klicken Sie dann auf **Installieren**.  
  
5. Auf der Seite **Installationsmodus auswählen** klicken Sie auf **Servermigration**, und geben dann die erforderlichen Migrationsinformationen ein.  
  
6. Sobald die Meldung **Der Server wurde erfolgreich migriert** angezeigt wird, klicken Sie auf **Schließen**.  
  
   Nach Abschluss der Installation werden Sie automatisch mit dem Benutzerkonto und Kennwort des Administrators angemeldet, die Sie in der Antwortdatei für die Migration bereitgestellt haben.  
  
> [!NOTE]
>  Um den Desktop entsperren, während Windows Server Essentials installiert wird, verwenden Sie das integrierte Administratorkonto aus, und lassen Sie das Kennwort leer.  
  
##  <a name="BKMK_VerifyTheHealthOfDC"></a> Überprüfen Sie die Integrität des Domänencontrollers  
 Bevor Sie mit der Migration fortfahren, sollten Sie sicherstellen, dass der Domänencontroller und Windows Server Essentials-Netzwerk fehlerfrei sind.  
  
 Die folgende Tabelle listet die Tools auf, die Sie für die Diagnose von Problemen auf Ihrem Zielserver, im Netzwerk oder in der Domäne verwenden können:  
  
|Tool|Beschreibung|  
|----------|-----------------|  
|Netdiag|Unterstützt Sie bei der Isolation von Netzwerk- und Verbindungsproblemen. Unter [Netdiag](https://go.microsoft.com/fwlink/?LinkId=217388)finden Sie weitere Informationen und können auch das Tool herunterladen.|  
|Dcdiag.exe|Analysiert den Zustand von Domänencontrollern in einer Gesamtstruktur oder einem Unternehmen und meldet Probleme, um Sie bei der Problembehandlung zu unterstützen. Unter [Dcdiag](https://go.microsoft.com/fwlink/?LinkId=217389)finden Sie weitere Informationen und können auch das Tool herunterladen.|  
|Repadmin.exe|Unterstützt Sie bei der Diagnose von Replikationsproblemen zwischen Domänencontrollern. Zur Ausführung dieses Tools sind Befehlszeilenparameter erforderlich. Unter [Repadmin](https://go.microsoft.com/fwlink/?LinkId=217387)finden Sie weitere Informationen und können auch das Tool herunterladen.|  
  
 Alle von diesen Tools erfassten Probleme sollten behoben werden, bevor Sie mit der Migration fortfahren.  
  
> [!NOTE]
>  Wenn Sie e-Mail-Adresse zu einem anderen lokalen Exchange-Server migrieren möchten, finden Sie unter [Integrieren eines lokalen Exchange-Servers mit Windows Server Essentials](../manage/Integrate-an-On-Premises-Exchange-Server-with-Windows-Server-Essentials.md) Informationen zum Einrichten Ihrer lokalen Exchange-Servers.
