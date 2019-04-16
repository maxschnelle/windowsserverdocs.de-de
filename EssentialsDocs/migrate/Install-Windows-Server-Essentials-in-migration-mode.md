---
title: Installieren von Windows Server Essentials in Migration Modus 1
description: Beschreibt, wie Sie Windows Server Essentials
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
ms.openlocfilehash: 808a4b1e120fa559d603b34ad006b18de6b94378
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="install-windows-server-essentials-in-migration-mode1"></a>Installieren von Windows Server Essentials in Migration Modus 1

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

Kann von Ihnen nur ein Server im Netzwerk, auf denen Windows Server Essentials ausgeführt wird, und dieser Server muss ein Domänencontroller für das Netzwerk sein.  
  
 Wenn Sie Windows Server Essentials im Migrationsmodus installieren, führt der Installations-Assistent die folgenden Aufgaben aus:  
  
1.  Installiert und konfiguriert die Windows Server Essentials-Server-Software auf dem Zielserver.  
  
2.  Aktualisierung des domänenschemas auf die neueste Version.  
  
3.  Verknüpft den Zielserver mit der vorhandenen Domäne. Der Quellserver und Zielserver können beide Mitglieder derselben Domäne sein, bis der Migrationsvorgang abgeschlossen ist. Nachdem die Migration abgeschlossen ist, müssen Sie den Quellserver innerhalb von 21 Tagen aus dem Netzwerk entfernen.  
  
    > [!WARNING]
    >  Eine Fehlermeldung wird jeden Tag während der Karenzzeit von 21 Tagen bis Sie den Quellserver aus dem Netzwerk entfernen, in das Ereignisprotokoll hinzugefügt. Der Text, der die Fehlermeldung lautet: "die Überprüfung der FSMO-Rolle eine Bedingung in Ihrer Umgebung, die nicht mit der Lizenzierungsrichtlinie konform ist erkannt. Der Verwaltungsserver muss der primäre Domänencontroller und der Domänennamenmaster Active Directory enthalten. Fahren Sie die Active Directory-Rollen jetzt an den Verwaltungsserver. Dieser Server wird automatisch heruntergefahren, wenn das Problem nicht innerhalb von 21 Tagen ab dem Zeitpunkt behoben wird, die diese Bedingung zuerst erkannt wurde." Nach der Toleranzperiode von 21 Tagen wird der Quellserver heruntergefahren.  
  
4.  Die (auch als flexible einfache Mastervorgänge oder FSMO bezeichnet) Betriebsmasterrollen übertragen vom Quellserver auf den Zielserver. Betriebsmasterrollen sind spezialisierte Aufgaben, die verwendet werden, wenn Standardmethoden für die Datenübertragung und Updates unzureichend sind. Wenn der Zielserver ein Domänencontroller ist, muss er die Betriebsmasterrollen enthalten.  
  
5.  Konfiguriert den Zielserver als globalen Katalogserver. Der globale Katalogserver ist ein Domänencontroller, der ein verteiltes Datenrepository verwaltet. Sie enthält eine durchsuchbare teildarstellung jedes Objekts in jeder Domäne in Active Directory-Gesamtstruktur.  
  
6.  Konfiguriert den Zielserver als den Standortlizenzserver.  
  
##  <a name="BKMK_Install"></a>Installieren von Windows Server Essentials auf dem Zielserver  
 Installieren und Konfigurieren von Windows Server Essentials auf dem Zielserver im Migrationsmodus, führen Sie die folgenden Schritte aus.  
  
#### <a name="to-install-windows-server-essentials-on-the-destination-server"></a>So installieren Sie Windows Server Essentials auf dem Zielserver  
  
1.  Aktivieren Sie auf dem Zielserver, und legen Sie die Windows Server Essentials-DVD1 in das DVD-Laufwerk. Wenn Sie eine Meldung, die der Frage angezeigt, ob Sie von einer CD oder DVD zu starten möchten, drücken Sie eine beliebige Taste dazu.  
  
    > [!NOTE]
    >  Wenn der Zielserver das Starten von einem USB-Speicherstick unterstützt, können Sie mithilfe der **Windows 7 USB/DVD Download Tool** um einen startbaren USB-Speicherstick aus der Windows Server Essentials-ISO-Datei zu erstellen. Mit einem USB-Speicherstick kann deutlich während des Installationsvorgangs beschleunigen, da Speichersticks Daten sehr viel schneller als DVD-ROM-Laufwerke lesen. Nachdem Sie einen startbaren USB-Speicherstick erstellen, können Sie eine Antwortdatei zum Speicherstick hinzufügen. Sie können [Herunterladen von Windows7 USB/DVD Download Tool](https://go.microsoft.com/fwlink/p/?LinkId=248282) kostenlos von Microsoft Store-Website.  
  
    > [!NOTE]
    >  Wenn der Zielserver nicht von der DVD startet, starten Sie den Computer neu, und überprüfen Sie die BIOS-Setup, um sicherzustellen, dass **DVD-ROM-** ist in der Startsequenz zuerst aufgeführt. Weitere Informationen zur Vorgehensweise beim Ändern der BIOS-Setup-Startsequenz finden Sie in der Dokumentation des Hardwareherstellers.  
  
2.  Klicken Sie auf **Neuinstallation**.  
  
3.  Wenn Sie eine interne Festplatte, die nicht in der Liste angezeigt wird haben, klicken Sie auf **Treiber laden** und den erforderlichen Treiber installieren, bevor Sie fortfahren.  
  
4.  Aktivieren Sie das Kontrollkästchen, die überprüft, alle Dateien und Ordner auf der primären Festplatte gelöscht werden, und klicken Sie dann auf **installieren**.  
  
5.  Auf der **Installationsmodus auswählen** auf **Servermigration**, und geben Sie die erforderlichen Migrationsinformationen.  
  
6.  Wenn die **Ihr Server wurde erfolgreich migriert** Meldung angezeigt wird, klicken Sie auf **schließen**.  
  
 Nach Abschluss der Installation werden Sie automatisch angemeldet mit dem Benutzerkonto und Kennwort, die Sie in der Antwortdatei für die Migration bereitgestellt.  
  
> [!NOTE]
>  Zum Entsperren des Desktops beim Installieren von Windows Server Essentials verwenden Sie das integrierte Administratorkonto und lassen Sie das Kennwort leer.  
  
##  <a name="BKMK_VerifyTheHealthOfDC"></a>Überprüfen der Integrität des Domänencontrollers  
 Bevor Sie mit der Migration fortfahren, sollten Sie sicherstellen, dass der Domänencontroller und Windows Server Essentials-Netzwerk fehlerfrei sind.  
  
 Die folgende Tabelle enthält die Tools, die Sie für die diagnose von Problemen, die auf dem Zielserver und dem Netzwerk, und klicken Sie in der Domäne verwenden können:  
  
|Tool|Beschreibung|  
|----------|-----------------|  
|Netdiag|Hilft bei der Isolierung Netzwerk- und Verbindungsproblemen. Weitere Informationen und zum Herunterladen finden Sie unter [Netdiag](https://go.microsoft.com/fwlink/?LinkId=217388).|  
|Dcdiag.exe|Der Status von Domänencontrollern in einer Gesamtstruktur oder Organisation analysiert und meldet Probleme, die Sie bei der Problembehandlung unterstützen. Weitere Informationen und zum Herunterladen finden Sie unter [Dcdiag](https://go.microsoft.com/fwlink/?LinkId=217389).|  
|Repadmin.exe|Unterstützt Sie bei der Diagnose von Replikationsproblemen zwischen Domänencontrollern. Diese Tools sind Befehlszeilenparameter Ausführung erforderlich. Weitere Informationen und zum Herunterladen finden Sie unter [Repadmin](https://go.microsoft.com/fwlink/?LinkId=217387).|  
  
 Korrigieren Sie alle Probleme, die diese Tools melden, bevor Sie mit der Migration fortfahren.  
  
> [!NOTE]
>  Wenn Sie die e-Mail zu einem anderen lokalen Exchange-Server migrieren möchten, finden Sie unter [Integration eines lokalen Exchange-Servers in Windows Server Essentials](../manage/Integrate-an-On-Premises-Exchange-Server-with-Windows-Server-Essentials.md) Informationen dazu, wie Sie Ihre lokalen Exchange-Server einrichten.
