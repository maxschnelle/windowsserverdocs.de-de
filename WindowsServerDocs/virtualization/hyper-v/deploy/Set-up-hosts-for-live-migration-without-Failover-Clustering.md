---
title: Einrichten von Hosts für die Livemigration ohne Failoverclustering
description: Bietet eine Anleitung zum Einrichten von Livemigration in einer Umgebung ohne Cluster
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b5e3c405-cb76-4ff2-8042-c2284448c435
author: KBDAzure
ms.author: kathydav
ms.date: 9/30/2016
ms.openlocfilehash: 49e36d7fae5eec07772fd6f82c5a5d69838351d8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59821991"
---
# <a name="set-up-hosts-for-live-migration-without-failover-clustering"></a>Einrichten von Hosts für die Livemigration ohne Failoverclustering

>Gilt für: WindowsServer 2016 wird Microsoft Hyper-V Server 2016, WindowsServer 2019, Microsoft Hyper-V-Server 2019

In diesem Artikel veranschaulicht, um Hosts einzurichten, die gruppiert werden nicht, damit Sie Migrationen zwischen ihnen Leben können. Verwenden Sie diese Anweisungen, wenn Sie live-Migration eingerichtet haben, bei der Installation von Hyper-V, oder wenn Sie die Einstellungen ändern möchten. Um geclusterte Hosts einzurichten, verwenden Sie Tools für die Failover-Clusterunterstützung ein.  
  
## <a name="requirements-for-setting-up-live-migration"></a>Anforderungen für die Einrichtung von live-migration  
  
Um nicht geclusterten Hosts für die Livemigration einzurichten, müssen Sie:   
  
-  Ein Benutzerkonto mit der Berechtigung zum Ausführen der verschiedenen Schritte. Mitgliedschaft in der lokalen Administratorengruppe von Hyper-V oder die Gruppe "Administratoren" auf den Quell-und Ziel erfüllt diese Anforderung, aus, es sei denn, Sie eingeschränkten Delegierung konfigurieren. Mitgliedschaft in der Gruppe der Domänenadministratoren ist erforderlich, um die eingeschränkte Delegierung konfigurieren.  
  
- Die Hyper-V-Rolle in Windows Server 2016 oder Windows Server 2012 R2 auf den Quell- und Ziel-Servern installiert werden soll. Sie erreichen eine Livemigration zwischen Hosts, auf denen Windows Server 2016 und Windows Server 2012 R2, ob die virtuelle Maschine mindestens Version 5. <br>Version Anweisungen finden Sie unter [Upgrade VM-Konfigurationsversion in Hyper-V unter Windows 10 oder Windows Server 2016](Upgrade-virtual-machine-version-in-Hyper-V-on-Windows-or-Windows-Server.md). Installationsanweisungen finden Sie unter [Installieren der Hyper-V-Serverrolle unter Windows Server](../get-started/Install-the-Hyper-V-role-on-Windows-Server.md).  
  
- Quelle und Ziel-Computer, die entweder zu derselben Active Directory-Domäne gehören, oder gehören zu Domänen, die sich gegenseitig vertrauen.    
- Die Hyper-V-Verwaltungstools auf einem Computer unter Windows Server 2016 oder Windows 10 installiert werden, es sei denn, auf dem Quell- oder Ziel-Server, und Sie die Tools installiert sind, werden die Tools auf dem Server ausführen.  
  
## <a name="consider-options-for-authentication-and-networking"></a>Erwägen Sie die Optionen für die Authentifizierung und Netzwerk  
  
Beachten Sie, wie Sie Folgendes einrichten möchten:  
  
-  **Authentifizierung**: Welches Protokoll zum Authentifizieren des livemigrations-Datenverkehr zwischen Quell-und Ziel verwendet wird? Die Auswahl bestimmt, ob Sie vor dem Starten einer Livemigration auf dem Quellserver anmelden müssen:   
   - Kerberos können Sie die zu vermeiden, dass sich an den Server im, erfordert jedoch die eingeschränkte Delegierung eingerichtet werden. Anweisungen finden Sie unten.  
   - CredSSP können Sie vermeiden, Konfigurieren der eingeschränkten Delegierung, erfordert jedoch, dass Sie auf dem Quellserver anmelden. Sie erreichen dies über eine lokale konsolensitzung, eine Remotedesktopsitzung oder eine Windows PowerShell-Remotesitzung.  
  
      CredSPP muss die Anmeldung für Situationen, in denen möglicherweise nicht offensichtlich. Wenn Sie sich testserver01 zum Verschieben eines virtuellen Computers auf testserver02 anmelden anmelden, und klicken Sie dann die virtuelle Maschine wieder auf TestServer01 verschieben möchten, müssen Sie z. B. TestServer02 anmelden, bevor Sie versuchen, den virtuellen Computer wieder auf TestServer01 verschieben. Wenn Sie dies nicht tun, wird der Authentifizierungsversuch fehlschlägt, ein Fehler auftritt, und die folgende Meldung wird angezeigt:  
    
      "VM-Migration Fehler bei Vorgang an der Migrationsquelle.  
      Fehler beim Herstellen einer Verbindung mit Host *Computername*: Sind keine Anmeldeinformationen im Sicherheitspaket 0x8009030E verfügbar."
  
-   **Leistung**: Sinnvoll es, Leistungsoptionen konfigurieren? Diese Optionen können reduzieren, Netzwerk- und CPU-Auslastung, als auch live-Migrationen schneller machen. Betrachten Sie Ihren Anforderungen und Ihrer Infrastruktur, und Testen Sie unterschiedliche Konfigurationen, damit Sie entscheiden können. Die Optionen werden am Ende von Schritt 2 beschrieben.  
  
-  **Netzwerk-Einstellung**: Lassen Sie den Datenverkehr für die Livemigration über ein beliebiges verfügbares Netzwerk zu, oder möchten Sie den Datenverkehr in speziellen Netzwerken isolieren? Als bewährte Sicherheitsmethode wird empfohlen, den Datenverkehr auf vertrauenswürdige, private Netzwerken zu isolieren, da der Datenverkehr für die Livemigration beim Senden über das Netzwerk nicht verschlüsselt wird. Die Netzwerkisolation kann über ein physisch isoliertes Netzwerk oder über eine andere vertrauenswürdige Netzwerktechnologie, z. B. VLANs, erreicht werden.  
  
## <a name="BKMK_Step1"></a>Schritt 1: Konfigurieren der eingeschränkten Delegierung (optional)  
Wenn Sie entschieden haben, die Verwendung von Kerberos zur Authentifizierung von live Migration-Traffic, konfigurieren Sie eingeschränkte Delegierung mit einem Konto an, die Mitglied der Gruppe der Domänenadministratoren ist.  
  
### <a name="use-the-users-and-computers-snap-in-to-configure-constrained-delegation"></a>Verwenden Sie den Benutzer und Computer-Snap-in zum Konfigurieren der eingeschränkten Delegierung  
  
1.  Öffnen Sie das Snap-In %%amp;quot;Active Directory-Benutzer und -Computer%%amp;quot;. (In Server-Manager, wählen Sie den Server, wenn es nicht aktiviert ist, klicken Sie auf **Tools** >> **Active Directory-Benutzer und-Computer**).  
  
2.  Im Navigationsbereich in **Active Directory-Benutzer und-Computer**, wählen Sie die Domäne, und doppelklicken Sie auf die **Computer** Ordner.  
  
3.  Von der **Computer** Ordner mit der rechten Maustaste in des Computerkontos des Quellservers, und klicken Sie dann auf **Eigenschaften**.  
  
4.  Von **Eigenschaften**, klicken Sie auf die **Delegierung** Registerkarte.  
  
5.  Wählen Sie auf der Registerkarte "Delegierung" **Computer bei Delegierungen angegebener Dienste vertrauen** und wählen Sie dann **Beliebiges Authentifizierungsprotokoll verwenden**.  
  
6.  Klicken Sie auf **Hinzufügen**.  
  
7.  Von **Dienste hinzufügen**, klicken Sie auf **Benutzer oder Computer**.  
  
8.  Von **Benutzer oder Computer auswählen**, geben Sie den Namen des Zielservers. Klicken Sie auf **Namen überprüfen** zu überprüfen, und klicken Sie dann auf **OK**.  
  
9. Von **Dienste hinzufügen**, in der Liste der verfügbaren Dienste, gehen Sie folgendermaßen vor, und klicken Sie dann auf **OK**:  
  
    -   Wenn Sie den Speicher des virtuellen Computers entfernen möchten, wählen Sie **cifs**aus. Dies ist erforderlich, wenn Sie möchten den Speicher zusammen mit dem virtuellen Computer verschieben sowie als wenn nur ein VM Speicher verschoben werden soll. Wenn der Server für die Verwendung des SMB-Speichers für Hyper-V konfiguriert ist, wurde diese Auswahl bereits getroffen.  
  
    -   Wenn Sie virtuelle Computer verschieben möchten, wählen Sie den **Migrationsdienst für virtuelles System von Microsoft** aus.  
  
10. Stellen Sie auf der Registerkarte **Delegierung** des Dialogfelds %%amp;quot;Eigenschaften%%amp;quot; sicher, dass die von Ihnen im vorherigen Schritt ausgewählten Dienste als Dienste aufgelistet sind, für die der Zielcomputer delegierte Anmeldeinformationen bereitstellen kann. Klicken Sie auf **OK**.  
  
11. Wählen Sie im Ordner **Computers** das Computerkonto des Zielservers aus, und wiederholen Sie den Prozess. Vergewissern Sie sich, dass Sie im Dialogfeld **Benutzer oder Computer auswählen** den Namen des Quellservers angegeben haben.  
  
Die konfigurationsänderungen wirksam, nach dem Auftreten von beide der folgenden:  
  
  -  Die Änderungen werden auf die Domänencontroller repliziert, denen die Server mit Hyper-V angemeldet sind.  
  -  Der Domänencontroller gibt ein neues Kerberos-Ticket.  
  
## <a name="BKMK_Step2"></a>Schritt 2: Einrichten der Quelle und Ziel-Computer für die Livemigration  
Dieser Schritt umfasst die Auswahl der Option für die Authentifizierung und Netzwerk. Als best Practice für die Sicherheit wird empfohlen, dass Sie bestimmte Netzwerke für livemigrations-Datenverkehr verwenden auswählen, wie oben beschrieben. Dieser Schritt zeigt, auch die Option "Performance" auswählen.   
  
### <a name="use-hyper-v-manager-to-set-up-the-source-and-destination-computers-for-live-migration"></a>Verwenden von Hyper-V-Manager der Quelle und Ziel für die Livemigration eingerichtet  
  
1.  Öffnen Sie den Hyper-V-Manager. (In Server-Manager, klicken Sie auf **Tools** >>**Hyper-V-Manager**.)  
  
2.  Wählen Sie im Navigationsbereich einen der Server aus. (Wenn er nicht angegeben ist, mit der rechten Maustaste **Hyper-V-Manager**, klicken Sie auf **Herstellen einer Verbindung mit Server**, geben Sie den Servernamen ein, und klicken Sie auf **OK**. Wiederholen Sie zum Hinzufügen weiterer Server.)  
  
3.  In der **Aktion** Bereich, klicken Sie auf **Hyper-V-Einstellungen** >>**Livemigrationen**.  
  
4.  Aktivieren Sie im Bereich **Livemigrationen** die Option **Ein- und ausgehende Livemigrationen ermöglichen**.  
  
5.  Klicken Sie unter **gleichzeitige livemigrationen**, eine andere Anzahl angeben, wenn Sie nicht die Standardeinstellung 2 verwenden möchten.  
  
6.  Wenn spezielle Netzwerkverbindungen den Datenverkehr für die Livemigration akzeptieren sollen, klicken Sie unter **Eingehende Livemigrationen**auf **Hinzufügen** , um die IP-Adressinformationen einzugeben. Klicken Sie anderenfalls auf **Beliebiges Netzwerk für Livemigration verwenden**. Klicken Sie auf **OK**.  
  
7.  Um Kerberos und Leistungsoptionen auszuwählen, erweitern Sie **Livemigrationen** und wählen Sie dann **erweiterte Features**.  
  
    - Wenn Sie die eingeschränkte Delegierung unter konfiguriert haben **Authentifizierungsprotokoll**Option **Kerberos**.  
    - Klicken Sie unter **Leistungsoptionen**, überprüfen Sie die Details, und wählen Sie eine andere Option aus, wenn es für Ihre Umgebung geeignet ist.   
  
8. Klicken Sie auf **OK**.  
  
9. Wählen Sie den anderen Server im Hyper-V-Manager, und wiederholen Sie die Schritte.  
  
### <a name="use-windows-powershell-to-set-up-the-source-and-destination-computers-for-live-migration"></a>Verwenden von Windows PowerShell, um die Quelle und Ziel-Computer für die Livemigration einzurichten  
  
Drei Cmdlets sind verfügbar für die Konfiguration von Livemigration auf nicht geclusterten Hosts: [Enable-VMMigration](https://technet.microsoft.com/library/hh848544.aspx), [Set-VMMigrationNetwork](https://technet.microsoft.com/library/hh848467.aspx), und [Set-VMHost](https://technet.microsoft.com/library/hh848524.aspx). In diesem Beispiel alle drei verwendet und führt folgende Schritte aus:   
  - Live-Migration konfiguriert auf dem lokalen host  
  - Können eingehenden Datenverkehr nur in einem bestimmten Netzwerk  
  - Wählt Kerberos als Authentifizierungsprotokoll   
  
Jede Zeile entspricht einem separaten Befehl.  
  
```  
PS C:\> Enable-VMMigration  
  
PS C:\> Set-VMMigrationNetwork 192.168.10.1  
  
PS C:\> Set-VMHost -VirtualMachineMigrationAuthenticationType Kerberos  
  
```  
Set-VMHost kann auch eine Option "Performance" (und viele andere Einstellungen für den Host) auswählen. Geben Sie z. B., um zu SMB wählen lassen das Authentifizierungsprotokoll, das auf den Standardwert von CredSSP festgelegt:  
  
```  
PS C:\> Set-VMHost -VirtualMachineMigrationPerformanceOption SMBTransport  
  
```  
  
In dieser Tabelle wird beschrieben, wie die Leistungsoptionen zu funktionieren.  
  
|Option|Beschreibung|  
|----------|---------------|  
    |TCP/IP|Der Arbeitsspeicher des virtuellen Computers kopiert auf den Zielserver. über eine TCP/IP-Verbindung.|  
    |Komprimierung|Komprimiert der Speicherinhalt des virtuellen Computers, bevor Sie sie über eine TCP/IP-Verbindung auf den Zielserver kopieren. **Hinweis**: Dies ist die **Standard** festlegen.|  
    |SMB|Der Arbeitsspeicher des virtuellen Computers kopiert auf den Zielserver. über eine SMB 3.0-Verbindung.<br /><br />-SMB Direct wird verwendet, wenn die Netzwerkadapter auf dem Quell- und Ziel (Remote Direct Memory Access, RDMA)-Funktionen, die aktiviert haben.<br />-SMB Multichannel automatisch erkennt und verwendet mehrere Verbindungen, wenn eine ordnungsgemäße Konfiguration von SMB Multichannel identifiziert wird.<br /><br />Weitere Informationen finden Sie unter [Improve Performance of a File Server with SMB Direct](https://technet.microsoft.com/library/jj134210(WS.11).aspx).|  
      
 ## <a name="next-steps"></a>Nächste Schritte
 
 Nachdem Sie die Hosts eingerichtet haben, können Sie eine Livemigration. Anweisungen hierzu finden Sie unter [mit der Livemigration ohne Failoverclustering zum Verschieben eines virtuellen Computers](../manage/Use-live-migration-without-Failover-Clustering-to-move-a-virtual-machine.md). 
    


