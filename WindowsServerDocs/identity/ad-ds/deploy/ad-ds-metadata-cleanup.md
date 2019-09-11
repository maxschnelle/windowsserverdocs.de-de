---
title: Bereinigen von AD DS Server-Metadaten
description: Verwenden integrierter Tools zum Bereinigen von Metadaten von entfernten Domänen Controllern
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 11/14/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: e8adbaf07976569fdea86156e15f246aad2e4fe0
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70868243"
---
# <a name="clean-up-active-directory-domain-controller-server-metadata"></a>Active Directory-Domäne Controller-Server Metadaten bereinigen

Gilt für: Windows Server

Die Metadatenbereinigung ist eine erforderliche Prozedur nach der erzwungenen Entfernung von Active Directory Domain Services (AD DS). Sie führen die Metadatenbereinigung auf einem Domänen Controller in der Domäne des Domänen Controllers aus, den Sie zwangsweise entfernt haben. Bei der Metadatenbereinigung werden Daten aus AD DS entfernt, die einen Domänen Controller zum Replikationssystem identifizieren. Bei der Metadatenbereinigung werden auch Datei Replikations Dienst (File Replication Service, FRS) und verteiltes Dateisystem (DFS)-Replikations Verbindungen entfernt, und es wird versucht, Betriebs Master-Rollen (auch als Flexible Single Master Operations oder FSMO bezeichnet) zu übertragen, der Controller enthält.

Es gibt drei Optionen zum Bereinigen von Server Metadaten:

- Bereinigen von Server Metadaten mithilfe von GUI-Tools
- Bereinigen von Server Metadaten mithilfe der Befehlszeile
- Bereinigen von Server Metadaten mithilfe eines Skripts

> [!NOTE]
> Wenn Sie den Fehler "Zugriff verweigert" erhalten, wenn Sie eine dieser Methoden zum Durchführen der Metadatenbereinigung verwenden, stellen Sie sicher, dass das Computer Objekt und das NTDS-Einstellungs Objekt für den Domänen Controller nicht vor versehentlichem Löschen geschützt sind. Klicken Sie mit der rechten Maustaste auf das Computer Objekt oder das NTDS-Einstellungs Objekt, klicken Sie auf **Eigenschaften**, klicken Sie auf **Objekt**, und deaktivieren Sie das Kontrollkästchen **Objekt vor zufälligem Löschen schützen** . In Active Directory Benutzer und Computer wird die Registerkarte **Objekt** eines Objekts angezeigt, wenn Sie auf **Ansicht** und dann auf **Erweiterte Features**klicken.

## <a name="clean-up-server-metadata-using-gui-tools"></a>Bereinigen von Server Metadaten mithilfe von GUI-Tools

Wenn Sie Remoteserver-Verwaltungstools (RSAT) oder die Konsole "Active Directory Benutzer und-Computer" (DSA. msc) verwenden, die in Windows Server enthalten ist, um ein Domänen Controller-Computer Konto aus der Domänen Controller-Organisationseinheit (OU) zu löschen, wird der der Bereinigung der Server Metadaten wird automatisch durchgeführt. Vor Windows Server 2008 mussten Sie eine separate Metadatenbereinigungs Prozedur durchführen.

Sie können auch die Active Directory Sites und Dienste-Konsole (dssite. msc) verwenden, um das Computer Konto eines Domänen Controllers zu löschen. Dadurch wird auch die Metadatenbereinigung automatisch abgeschlossen. Wenn Sie das NTDS-Einstellungs Objekt zum ersten Mal unter dem Computer Konto in dssite. msc löschen, werden die Metadaten jedoch von Active Directory Websites und Diensten automatisch entfernt.

Solange Sie Windows Server 2008 oder neuere RSAT-Versionen von DSA. msc oder dssite. msc verwenden, können Sie die Metadaten für Domänen Controller, auf denen frühere Versionen von Windows-Betriebssystemen ausgeführt werden, automatisch bereinigen.

Sie müssen mindestens Mitglied der Gruppe **Domänen-Admins**oder einer entsprechenden Gruppe sein, um diese Verfahren ausführen zu können.

## <a name="clean-up-server-metadata-using-activedirectory-users-and-computers"></a>Bereinigen von Server Metadaten mithilfe von Active Directory Benutzern und Computern

1. Öffnen Sie **Active Directory-Benutzer und -Computer**.
2. Wenn Sie die Replikations Partner als Vorbereitung für dieses Verfahren identifiziert haben und Sie nicht mit einem Replikations Partner des entfernten Domänen Controllers verbunden sind, dessen Metadaten Sie bereinigen, klicken Sie mit der rechten Maustaste auf den Knoten " **Benutzer und Computer" Active Directory** . , und klicken Sie dann auf **Domänen Controller ändern**. Klicken Sie auf den Namen des Domänen Controllers, von dem Sie die Metadaten entfernen möchten, und klicken Sie dann auf **OK**.
3. Erweitern Sie die Domäne des Domänen Controllers, der zwangsweise entfernt wurde, und klicken Sie dann auf **Domänen Controller**.
4. Klicken Sie im Detailfenster mit der rechten Maustaste auf das Computer Objekt des Domänen Controllers, dessen Metadaten Sie bereinigen möchten, und klicken Sie dann auf **Löschen**.
5. Bestätigen Sie im Dialogfeld **Active Directory Domain Services** , dass der Name des Domänen Controllers, den Sie löschen möchten, angezeigt wird, und klicken Sie auf **Ja** , um das Löschen des Computer Objekts zu bestätigen.
6. Wählen Sie im Dialogfeld **Domänen Controller löschen** die Option **dieser Domänen Controller ist dauerhaft offline und kann nicht mehr mithilfe des Assistent zum Installieren von Active Directory Domain Services (Dcpromo) herabgestuft werden**aus, und klicken Sie dann auf **Löschen**.
7. Wenn der Domänen Controller ein globaler Katalogserver ist, klicken Sie im Dialogfeld **Domänen Controller löschen** auf **Ja** , um den Löschvorgang fortzusetzen.
8. Wenn der Domänen Controller derzeit mindestens eine Betriebs Master Rolle enthält, klicken Sie auf **OK** , um die Rolle oder Rollen auf den angezeigten Domänen Controller zu verschieben. Dieser Domänen Controller kann nicht geändert werden. Wenn Sie die Rolle auf einen anderen Domänen Controller verschieben möchten, müssen Sie die Rolle nach Abschluss des Bereinigungs Verfahrens für die Server Metadaten verschieben.

## <a name="clean-up-server-metadata-using-activedirectory-sites-and-services"></a>Bereinigen von Server Metadaten mithilfe von Active Directory-Sites und-Diensten

1. Öffnen Sie Active Directory-Standorte und -Dienste.
2. Wenn Sie die Replikations Partner als Vorbereitung für dieses Verfahren identifiziert haben und Sie nicht mit einem Replikations Partner des entfernten Domänen Controllers verbunden sind, dessen Metadaten Sie bereinigen, klicken Sie mit der rechten Maustaste auf **Active Directory Standorte und Dienste**, und Klicken Sie dann auf **Domänen Controller ändern**. Klicken Sie auf den Namen des Domänen Controllers, von dem Sie die Metadaten entfernen möchten, und klicken Sie dann auf **OK**.
3. Erweitern Sie den Standort des Domänen Controllers, der zwangsweise entfernt wurde, erweitern Sie **Server**, erweitern Sie den Namen des Domänen Controllers, klicken Sie mit der rechten Maustaste auf das NTDS-Einstellungs Objekt, und klicken Sie dann auf **Löschen**.
4. Klicken Sie im Dialogfeld **Active Directory Websites und Dienste** auf **Ja** , um das Löschen der NTDS-Einstellungen zu bestätigen.
5. Wählen Sie im Dialogfeld **Domänen Controller löschen** die Option **dieser Domänen Controller ist dauerhaft offline und kann nicht mehr mithilfe des Assistent zum Installieren von Active Directory Domain Services (Dcpromo) herabgestuft werden**aus, und klicken Sie dann auf **Löschen**.
6. Wenn der Domänen Controller ein globaler Katalogserver ist, klicken Sie im Dialogfeld **Domänen Controller löschen** auf **Ja** , um den Löschvorgang fortzusetzen.
7. Wenn der Domänen Controller derzeit mindestens eine Betriebs Master Rolle enthält, klicken Sie auf **OK** , um die Rolle oder Rollen auf den angezeigten Domänen Controller zu verschieben.
8. Klicken Sie mit der rechten Maustaste auf den Domänen Controller, der entfernt wurde, und klicken Sie dann auf Löschen.
9. Klicken Sie im Dialogfeld **Active Directory Domain Services** auf **Ja** , um zu bestätigen, dass der Domänen Controller gelöscht wird.

## <a name="clean-up-server-metadata-using-the-command-line"></a>Bereinigen von Server Metadaten mithilfe der Befehlszeile

Als Alternative können Sie die Metadaten mithilfe von "Ntdsutil. exe" bereinigen, ein Befehlszeilen Tool, das automatisch auf allen Domänen Controllern und Servern installiert wird, auf denen Active Directory Lightweight Directory Services (AD LDS) installiert ist. Ntdsutil. exe ist auch auf Computern mit installiertem RSAT verfügbar.

## <a name="to-clean-up-server-metadata-by-using-ntdsutil"></a>So bereinigen Sie Server Metadaten mithilfe von Ntdsutil

1. Öffnen Sie eine Eingabeaufforderung als Administrator: Klicken Sie im **Startmenü** mit der rechten Maustaste auf **Eingabeaufforderung**, und klicken Sie dann auf **als Administrator ausführen**. Wenn das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, geben Sie bei Bedarf die Anmelde Informationen eines Unternehmens Administrators an, und klicken Sie dann auf **weiter**.
2. Geben Sie an der Eingabeaufforderung den folgenden Befehl ein, und drücken Sie die EINGABETASTE:

   `ntdsutil`

3. Geben Sie an der Eingabeaufforderung `ntdsutil:` den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE:

   `metadata cleanup`

4. Geben Sie an der Eingabeaufforderung `metadata cleanup:` den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE:

   `remove selected server <ServerName>`

5. Überprüfen Sie im **Dialog Feld Server Entfernungs Konfiguration**die Informationen und Warnungen, und klicken Sie dann auf **Ja** , um das Server Objekt und die Metadaten zu entfernen.

   An diesem Punkt bestätigt Ntdsutil, dass der Domänen Controller erfolgreich entfernt wurde. Wenn Sie eine Fehlermeldung erhalten, die angibt, dass das Objekt nicht gefunden werden kann, wurde der Domänen Controller möglicherweise bereits zuvor entfernt.

6. Geben `ntdsutil:` `metadata cleanup:` SieanderEingabeaufforderungein,unddrückenSiedanndieEINGABETASTE.`quit`

7. So bestätigen Sie das Entfernen des Domänen Controllers:

   Öffnen Sie Active Directory Benutzer und Computer. Klicken Sie in der Domäne des entfernten Domänen Controllers auf **Domänen Controller**. Im Detailfenster sollte ein Objekt für den Domänen Controller, den Sie entfernt haben, nicht angezeigt werden.

   Öffnen Sie Active Directory Websites und Dienste. Navigieren Sie zum **Container Servers** , und vergewissern Sie sich, dass das Server Objekt für den Domänen Controller, den Sie entfernt haben, kein NTDS-Einstellungs Objekt enthält. Wenn keine untergeordneten Objekte unterhalb des Server Objekts angezeigt werden, können Sie das Server Objekt löschen. Wenn ein untergeordnetes Objekt angezeigt wird, löschen Sie das Server Objekt nicht, da das Objekt von einer anderen Anwendung verwendet wird.

## <a name="see-also"></a>Siehe auch

* [Tieferstufen von Domänencontrollern](Demoting-Domain-Controllers-and-Domains--Level-200-.md)
* [Ntdsutil-Befehlsreferenz](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc753343(v=ws.10))
