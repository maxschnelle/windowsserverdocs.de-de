---
title: Wiederherstellung der AD-Gesamtstruktur - Wiederherstellung von Windows Server 2003
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 5a291f65-794e-4fc3-996e-094c5845a383
ms.technology: identity-adds
ms.openlocfilehash: bd15df5360a50e417881d83319344dbdf48f35fa
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59829641"
---
# <a name="ad-forest-recovery---windows-server-2003-recovery"></a>Wiederherstellung der AD-Gesamtstruktur - Wiederherstellung von Windows Server 2003

>Gilt für: Windows Server 2003

Dieses Thema enthält Prozeduren für Domänencontroller (DCs), auf denen Windows Server 2003 ausgeführt wird. Der allgemeine Prozess für die Wiederherstellung der Gesamtstruktur unterscheidet sich nicht mit Windows Server 2003-Domänencontrollern, aber bestimmte Verfahren können sich aufgrund der verschiedenen Tools unterscheiden. Beispielsweise können Ntdsutil.exe verwendet werden, Sichern und Wiederherstellen von DCs, auf denen Windows Server 2003-Domänencontrollern ausgeführt, während Windows Server-Sicherung oder Wbadmin.exe ist, verwendet für Domänencontroller mit Windows Server 2008 oder höher.  
  
- [Sicherung der Systemstatusdaten](#Backing-up-the-System-State-data)  
- [Eine nicht autoritative Wiederherstellung ausführen](#Performing-a-nonauthoritative restore)  
- [Installieren Sie und konfigurieren Sie den DNS-Serverdienst](#Install-and-configure-the-DNS-Server-service)  

## <a name="backing-up-the-system-state-data"></a>Sicherung der Systemstatusdaten
Gehen Sie folgendermaßen vor, um die Daten für den Systemstatus zu sichern, wird zusammen mit anderen Daten, die Sie für die aktuelle Sicherung ausgewählt haben, von einem Domänencontroller, die Windows Server 2003 ausgeführt. Windows Server 2003 enthält die Tools "Ntbackup", die Sie verwenden können, um Daten von Systemstatus zu sichern.  
  
Mitgliedschaft in **Administratoren** oder **Sicherungs-Operatoren**, oder einer entsprechenden Gruppe sein, um Dateien und Ordner sichern.   
  
Wenn Sie die Systemstatusdaten auf ein Band sichern aus, und das Backup-Programm gibt an, dass es keine Medien verfügbar ist, müssen Sie möglicherweise die Verwendung von Wechselmedien. Dadurch wird das Band in den Pool freier Medien hinzugefügt, damit, dass die Sicherung, die sie verwenden kann.  
  
Sie können nur die Daten von Systemstatus auf einem lokalen Computer sichern. Sie können es auf einem Remotecomputer sichern.  
  
### <a name="to-back-up-the-system-state-data-on-a-domain-controller-that-runs-windows-server-2003"></a>Zum Sichern der Daten von Systemstatus auf einem Domänencontroller ausgeführt wird, Windows Server 2003  
  
1. Klicken Sie auf **starten**, zeigen Sie auf **Programme**, zeigen Sie auf **Zubehör**, zeigen Sie auf **Systemprogramme**, und klicken Sie dann auf **Sicherung** .  
2. Auf der **Willkommen** auf **Erweiterter Modus**.  
3. Auf der **Sicherung** Registerkarte, wählen Sie das Kontrollkästchen für Laufwerk, Ordner oder Datei, die Sie sichern möchten.  
4. Wählen Sie die **Systemstatus** Kontrollkästchen.  
5. Klicken Sie auf **Sicherung starten**.  
  
## <a name="performing-a-nonauthoritative-restore"></a>Eine nicht autoritative Wiederherstellung ausführen  

Verwenden Sie das folgende Verfahren, um eine nicht autorisierende Wiederherstellung eines Domänencontrollers durchführen, die Windows Server 2003 ausgeführt wird. Eine nicht autorisierende Wiederherstellung auf Active Directory in Windows Server 2003 ausführen, führen Sie automatisch eine nicht autoritative Wiederherstellung von SYSVOL. Es sind keine zusätzlichen Schritte erforderlich.  
  
> [!NOTE]
> Wenn Sie auch das Windows Server 2003-Betriebssystem neu installieren, Sie oder den Computer möglicherweise nicht in die Domäne hinzugefügt, und geben Sie einen beliebigen Namen auf dem Computer, während der Installation des Betriebssystems. Installieren Sie Active Directory nicht. Nach der Neuinstallation des Betriebssystems, wechseln Sie direkt mit Schritt 4 fort.  
  
Auf Windows Server 2003-Domänencontrollern, in dem Sie nur die Systemstatusdaten wiederhergestellt haben, müssen Sie auch alle softwareanwendungen installieren, die vor der Wiederherstellung auf Domänencontrollern ausgeführt wurden. Wiederherstellen von AD DS auf des ersten Domänencontrollers in der Domäne wird auch die Registrierung wiederhergestellt, da sie beide Teil des Systemstatus-Daten sind. Beachten Sie, dass wenn Sie alle Anwendungen, die auf diese DCs ausgeführt haben und wenn sie alle Informationen, die in der Registrierung gespeichert haben.  
  
Um den Zeitaufwand für die Neuinstallation der Software zu speichern, zu bestimmen, ob es sich bei Anwendungen, die auf den Domänencontrollern installiert werden müssen, mit Klonen virtueller Domänencontroller kompatibel sind. Solche Anwendungen können auf der Quell-DC installiert werden, vor dem Klonen, um sparen Zeit und Aufwand erforderlich, um sie auf die geklonte virtuelle DCs zu installieren.  
  
### <a name="to-perform-a-nonauthoritative-restore"></a>Zum Ausführen einer nicht autoritativen Wiederherstellung
  
1. Nachdem der Domänencontroller gestartet wurde, drücken Sie F8, um den Computer im Verzeichnis Verzeichnisdienst-Wiederherstellungsmodus (DSRM) neu starten.  
2. Wählen Sie **Wiederherstellungsmodus für Verzeichnisdienste (nur für Windows-Domänencontroller)**.  
3. Wählen Sie das Betriebssystem, das im Wiederherstellungsmodus gestartet werden soll.  
4. Melden Sie sich als Administrator (Sie können nur verwenden, ein lokales Computerkonto und kein Anmeldeoption Domäne verfügbar ist).  
5. Geben Sie an einer Eingabeaufforderung den Befehl **Ntbackup**, und drücken Sie dann die EINGABETASTE.  
6. Auf der **Willkommen** auf **Erweiterter Modus**, und wählen Sie dann die **Medien wiederherstellen und verwalten** Registerkarte. (Wählen Sie nicht **Systemwiederherstellungs-Assistenten**.)  
7. Wählen Sie die entsprechenden Sicherungsdatei zum Wiederherstellen aus, und stellen sicher, dass die **Systemdatenträger** und **Systemstatus** Kontrollkästchen aktiviert sind.  
8. Klicken Sie auf **Wiederherstellung starten**.  
9. Wenn der Wiederherstellungsvorgang abgeschlossen ist, starten Sie den Computer neu.  
  
Verwenden Sie das folgende Verfahren, um eine autorisierende Wiederherstellung SYSVOL (auch bekannt als "Primär") auf einem Domänencontroller ausführen, die Windows Server 2003 ausgeführt wird. Führen Sie dieses Verfahren nur auf den ersten Windows Server 2003-Domänencontroller, die in der Domäne wiederhergestellt wird.  
  
### <a name="to-perform-an-authoritative-restore-of-sysvol"></a>Um eine autorisierende Wiederherstellung von SYSVOL durchführen  
  
1. Führen Sie die Schritte 1 bis 8, in der vorherigen Prozedur.  
2. In der **Bestätigen der Wiederherstellung der** Dialogfeld klicken Sie auf **erweitert**.  
3. Aktivieren Sie das Kontrollkästchen zum Durchführen einer autorisierenden Wiederherstellung von SYSVOL **bei replizierten, markieren Sie die wiederhergestellten Daten als die primären Daten für alle Replikate**.  

   > [!NOTE]
   > Markieren die wiederhergestellten Daten, wie die primären Daten in der Sicherung entsprechend der Einstellung der **BurFlags** auf D4-Eintrag unter den folgenden Registrierungsunterschlüssel:  
   >   
   > **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NtFrs\Parameters\Cumulative-Replikatsätze\\**  *GUID*  

4. Wenn der Wiederherstellungsvorgang abgeschlossen ist, starten Sie den Computer neu.  
  
## <a name="install-and-configure-the-dns-server-service"></a>Installieren Sie und konfigurieren Sie den DNS-Serverdienst

Wenn der Domänencontroller, die Sie aus einer Sicherung wiederhergestellt, Windows Server 2003 ausgeführt wird, können Sie die DNS-Server installieren, ohne eine Verbindung herstellen den DC mit einem Netzwerk.  
  
### <a name="to-install-and-configure-the-dns-server-service"></a>Installieren und konfigurieren den DNS-Serverdienst  
  
1. Öffnen Sie die Assistenten für die Windows-Komponenten. Um den Assistenten zu öffnen:  

   - Klicken Sie auf **Start**, klicken Sie auf **Systemsteuerung**, und klicken Sie dann auf **Programme hinzufügen oder entfernen**.  
   - Klicken Sie auf **Windows-Komponenten hinzufügen/entfernen**.  

2. In **Komponenten**, wählen die **Netzwerkdienste** , und klicken Sie dann auf **Details**.  
3. In **Unterkomponenten von Netzwerkdienste**, wählen die **Domain Name System (DNS)** Kontrollkästchen, klicken Sie auf **OK**, und klicken Sie dann auf **Weiter**.  
4. Wenn Sie, in aufgefordert werden **kopieren Dateien aus**, geben Sie den vollständigen Pfad der-Dateien, und klicken Sie dann auf **OK**.  

   Nach Abschluss der Installation die folgenden Schritte aus, um den DNS-Server konfigurieren.  

5. Klicken Sie auf **starten**, zeigen Sie auf **Programme**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **DNS**.  
6. Erstellen Sie DNS-Zonen für die gleiche DNS-Domänennamen, die gehostet wurden, auf die DNS-Server, bevor Sie die kritischen Fehler. Weitere Informationen finden Sie unter Hinzufügen einer Forward-Lookupzone ([https://go.microsoft.com/fwlink/?LinkId=74574](https://go.microsoft.com/fwlink/?LinkId=74574)).  
7. Konfigurieren Sie die DNS-Daten, wie sie vor der Fehlfunktion kritische vorhanden waren. Zum Beispiel:  

   - Konfigurieren Sie DNS-Zonen, die in AD DS gespeichert werden. Weitere Informationen finden Sie unter Ändern des Zonentyps ([https://go.microsoft.com/fwlink/?LinkId=74579](https://go.microsoft.com/fwlink/?LinkId=74579)).  
   - Konfigurieren Sie die DNS-Zone, die für Domänencontroller (DC Locator) Ressource-Locatoreinträgen um sichere dynamische Updates ermöglichen autorisierend ist. Weitere Informationen finden Sie ermöglichen nur sichere dynamische Updates ([https://go.microsoft.com/fwlink/?LinkId=74580](https://go.microsoft.com/fwlink/?LinkId=74580)).  

8. Stellen Sie sicher, dass die übergeordneten DNS-Zone Delegation-Ressourceneinträge (Namen der Namenserver (NS) und "Klebstoff", Host (A) Ressource Datensätze) für die untergeordnete Zone enthält, die auf diesen DNS-Server gehostet wird. Weitere Informationen finden Sie unter Erstellen einer Zonendelegierung ([https://go.microsoft.com/fwlink/?LinkId=74562](https://go.microsoft.com/fwlink/?LinkId=74562)).  
9. Nach der Konfiguration von DNS Geben Sie an der Eingabeaufforderung den folgenden Befehl aus, und drücken Sie dann die EINGABETASTE:  

   **Net Stop netlogon**

10. Geben Sie den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE:  

   **Net Start netlogon**

   > [!NOTE]
   > Der Anmeldedienst wird die Domänencontrollerlocator-Ressourceneinträge in DNS für diesen Domänencontroller registriert. Wenn Sie den DNS-Serverdienst auf einem Server in die untergeordnete Domäne installieren, werden diesem DC nicht sofort der Datensätze zu registrieren. Dies ist, da er derzeit isoliert ist als Bestandteil der Wiederherstellung, und den primären DNS-Server den Gesamtstruktur-Stamm-DNS-Server. Konfigurieren Sie ihn mit der gleichen IP-Adresse wie vor dem Notfall um DC-Dienst Fehler bei der kontosuche zu vermeiden.

## <a name="next-steps"></a>Nächste Schritte

- [Wiederherstellung der Gesamtstruktur der Active Directory - Voraussetzungen](AD-Forest-Recovery-Prerequisties.md)  
- [Wiederherstellung der Active Directory-Gesamtstruktur - Ausarbeiten eines Wiederherstellungsplans für die benutzerdefinierte Gesamtstruktur](AD-Forest-Recovery-Devising-a-Plan.md)  
- [Wiederherstellung der Gesamtstruktur des Active Directory - Ermittlung des Problems](AD-Forest-Recovery-Identify-the-Problem.md)
- [AD-Gesamtstruktur-Wiederherstellung: Bestimmen der Vorgehensweise beim Wiederherstellen](AD-Forest-Recovery-Determine-how-to-Recover.md)
- [Wiederherstellung der Active Directory-Gesamtstruktur - erste Wiederherstellung ausführen](AD-Forest-Recovery-Perform-initial-recovery.md)  
- [Wiederherstellung der Gesamtstruktur der Active Directory - Prozeduren](AD-Forest-Recovery-Procedures.md)  
- [Wiederherstellung der Active Directory-Gesamtstruktur – häufig gestellte Fragen](AD-Forest-Recovery-FAQ.md)  
- [AD-Gesamtstruktur-Wiederherstellung: Wiederherstellen einer einzelnen Domäne innerhalb einer Gesamtstruktur Multidomain](AD-Forest-Recovery-Single-Domain-in-Multidomain-Recovery.md)  
- [Wiederherstellung der Active Directory-Gesamtstruktur - Wiederherstellung der Gesamtstruktur mit Windows Server 2003-Domänencontrollern](AD-Forest-Recovery-Windows-Server-2003.md) 
