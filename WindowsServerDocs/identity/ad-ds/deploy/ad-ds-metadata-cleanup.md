---
title: Der Cleanup von Metadaten für AD DS-server
description: Verwenden der integrierten Tools, um Metadaten aus der entfernten Domänencontroller zu bereinigen
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 11/14/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: fbb6e720c9289c608d71d3c36695ba623a9df5f6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59818081"
---
# <a name="clean-up-active-directory-domain-controller-server-metadata"></a>Bereinigen von Servermetadaten Active Directory-Domänencontroller

Gilt für: Windows Server

Cleanup der Metadaten ist eine erforderliche Prozedur nach einem erzwungenen Entfernen von Active Directory Domain Services (AD DS). Führen Sie Metadatencleanup auf einem Domänencontroller in der Domäne des Domänencontrollers, den Sie zwangsweise entfernt. Metadatencleanup entfernt Daten aus AD DS, das einen Domänencontroller im Replikationssystem identifiziert. Metadatencleanup auch entfernt (File Replication Service, FRS) und die Replikation des verteilten Dateisystems (Distributed File System, DFS)-Verbindungen und versucht, übertragen, oder übernehmen Sie alle Operations Master (auch bekannt als flexible einfache Mastervorgänge oder FSMO) Funktionen, die die deaktivierten Domäne Controller enthält.

Es gibt drei Möglichkeiten, um Metadaten zu bereinigen:

- Bereinigen von Servermetadaten mithilfe der GUI-tools
- Bereinigen von Servermetadaten, die über die Befehlszeile
- Bereinigen von Servermetadaten mithilfe eines Skripts

> [!NOTE]
> Wenn Sie Fehler "Zugriff verweigert" erhalten, wenn Sie eine dieser Methoden verwenden, um die Metadatenbereinigung ausführen, stellen Sie sicher, dass das Computerobjekt und das NTDS-Einstellungsobjekt für den Domänencontroller nicht vor versehentlichem Löschen geschützt sind. Um diese mit der rechten Maustaste auf das Computerobjekt oder das NTDS-Einstellungsobjekt überprüfen, klicken Sie auf **Eigenschaften**, klicken Sie auf **Objekt**, und deaktivieren Sie die **schützen Objekt vor zufälligem Löschen** das Kontrollkästchen. In Active Directory-Benutzer und-Computer die **Objekt** Registerkarte eines Objekts, das angezeigt wird, wenn Sie auf **Ansicht** , und klicken Sie dann auf **erweiterte Features**.

## <a name="clean-up-server-metadata-using-gui-tools"></a>Bereinigen von Servermetadaten mithilfe der GUI-tools

Bei Verwendung von Remoteserver-Verwaltungstools (RSAT) oder die Active Directory-Benutzer und Computer-Konsole (Dsa.msc), die Bestandteil von Windows Server zum Löschen eines Domänencontrollerkontos für die Computer aus der Domänencontroller-Organisationseinheit (OU), ist die Bereinigen von Servermetadaten wird automatisch ausgeführt. Vor Windows Server 2008 mussten Sie eine separate Metadaten Cleanup-Prozedur auszuführen.

Sie können auch über die Konsole Active Directory-Standorte und-Dienste (Dssite.msc) auf einem Domänencontroller-Computerkonto und löschen die Metadatencleanup automatisch nach Abschluss. Jedoch entfernt Active Directory-Standorte und-Dienste die Metadaten automatisch nur, wenn Sie zuerst das NTDS-Einstellungsobjekt, unter dem Computerkonto in Dssite.msc löschen.

Solange Sie die Windows Server 2008 oder neueren Versionen von RSAT Dsa.msc oder Dssite.msc verwenden, können Sie die Metadaten für Domänencontroller unter früheren Versionen von Windows-Betriebssysteme automatisch bereinigen.

Mitgliedschaft in **Domänen-Admins**, oder einer entsprechenden Gruppe sein, um diese Verfahren abzuschließen.

## <a name="clean-up-server-metadata-using-activedirectory-users-and-computers"></a>Bereinigen von Servermetadaten mithilfe von Active Directory-Benutzer und-Computer

1. Öffnen Sie **Active Directory-Benutzer und -Computer**.
2. Wenn Sie Replikationspartner als Vorbereitung für diese Prozedur identifiziert haben, und wenn Sie nicht an einen Replikationspartner des Domänencontrollers entfernt verbunden sind, deren Metadaten, die Sie bereinigen werden mit der rechten Maustaste **Active Directory-Benutzer und Computer** Knoten, und klicken Sie dann auf **Domänencontroller ändern**. Klicken Sie auf den Namen des Domänencontrollers aus dem Sie die Metadaten zu entfernen, und klicken Sie dann auf möchten **OK**.
3. Erweitern Sie die Domäne des Domänencontrollers, die zwangsweise entfernt wurde, und klicken Sie dann auf **Domänencontroller**.
4. Im Detailbereich mit der Maustaste des Computerobjekts des Domänencontrollers, deren Metadaten zu bereinigen, und klicken Sie dann auf **löschen**.
5. In der **Active Directory Domain Services** Dialogfeld bestätigen der Name des zu löschenden Domänencontrollers wird angezeigt, und klicken Sie auf **Ja** auf den Computer-Objekt-Löschvorgang zu bestätigen.
6. In der **Domänencontroller löschen** wählen Sie im Dialogfeld **dieser Domänencontroller ist dauerhaft offline und kann nicht mehr mit der Active Directory Domain Services Installation Assistenten (DCPROMO)herabgestuftwerden**, und klicken Sie dann auf **löschen**.
7. Ist der Domänencontroller ein globaler Katalogserver, in der **Domänencontroller löschen** Dialogfeld klicken Sie auf **Ja** um den Löschvorgang fortzusetzen.
8. Wenn der Domänencontroller derzeit eine oder mehrere Operationen zugewiesen sind, klicken Sie auf **OK** , verschieben Sie die Rolle bzw. Rollen mit dem Domänencontroller, die angezeigt wird. Sie können diesen Domänencontroller nicht ändern. Wenn Sie die Rolle auf einem anderen Domänencontroller verschieben möchten, müssen Sie die Rolle verschieben, nachdem Sie die Server-Metadaten-Cleanup-Prozedur abgeschlossen.

## <a name="clean-up-server-metadata-using-activedirectory-sites-and-services"></a>Bereinigen von Servermetadaten mithilfe von Active Directory-Standorte und-Dienste

1. Öffnen Sie Active Directory-Standorte und -Dienste.
2. Wenn Sie Replikationspartner als Vorbereitung für diese Prozedur identifiziert haben, und wenn Sie nicht an einen Replikationspartner des Domänencontrollers entfernt verbunden sind, deren Metadaten, die Sie bereinigen werden mit der rechten Maustaste **Active Directory-Standorte und-Dienste** , und klicken Sie dann auf **Domänencontroller ändern**. Klicken Sie auf den Namen des Domänencontrollers aus dem Sie die Metadaten zu entfernen, und klicken Sie dann auf möchten **OK**.
3. Erweitern Sie den Standort des Domänencontrollers, die zwangsweise entfernt wurde, erweitern Sie **Server**, erweitern Sie den Namen des Domänencontrollers, mit der rechten Maustaste in des NTDS-Einstellungsobjekts, und klicken Sie dann auf **löschen**.
4. In der **Active Directory-Standorte und-Dienste** Dialogfeld klicken Sie auf **Ja** zu NTDS-Einstellungen bestätigen.
5. In der **Domänencontroller löschen** wählen Sie im Dialogfeld **dieser Domänencontroller ist dauerhaft offline und kann nicht mehr mit der Active Directory Domain Services Installation Assistenten (DCPROMO)herabgestuftwerden**, und klicken Sie dann auf **löschen**.
6. Ist der Domänencontroller ein globaler Katalogserver, in der **Domänencontroller löschen** Dialogfeld klicken Sie auf **Ja** um den Löschvorgang fortzusetzen.
7. Wenn der Domänencontroller derzeit eine oder mehrere Operationen zugewiesen sind, klicken Sie auf **OK** , verschieben Sie die Rolle bzw. Rollen mit dem Domänencontroller, die angezeigt wird.
8. Mit der rechten Maustaste in des Domänencontrollers, der zwangsweise entfernt wurde, und klicken Sie dann auf Löschen.
9. In der **Active Directory Domain Services** Dialogfeld klicken Sie auf **Ja** zu Domain Controllers bestätigen.

## <a name="clean-up-server-metadata-using-the-command-line"></a>Bereinigen von Servermetadaten, die über die Befehlszeile

Als Alternative können Sie Bereinigen von Metadaten mit Ntdsutil.exe, ein Befehlszeilentool, das automatisch, auf allen Domänencontrollern und Servern, die Active Directory Lightweight Directory Services (AD LDS installiert wird) installiert haben. Ntdsutil.exe steht auch auf Computern, die Remoteserver-Verwaltungstools installiert haben.

## <a name="to-clean-up-server-metadata-by-using-ntdsutil"></a>Bereinigen Sie Metadaten mithilfe von Ntdsutil

1. Öffnen Sie eine Eingabeaufforderung als Administrator aus: Auf der **starten** im Menü mit der rechten Maustaste **Eingabeaufforderung**, und klicken Sie dann auf **als Administrator ausführen**. Wenn die **User Account Control** Dialogfeld angezeigt wird, geben Sie Anmeldeinformationen eines Unternehmensadministrators bei Bedarf, und klicken Sie dann auf **Weiter**.
2. Geben Sie an der Eingabeaufforderung den folgenden Befehl ein, und drücken Sie die EINGABETASTE:

   `ntdsutil`

3. Geben Sie an der Eingabeaufforderung `ntdsutil:` den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE:

   `metadata cleanup`

4. Geben Sie an der Eingabeaufforderung `metadata cleanup:` den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE:

   `remove selected server <ServerName>`

5. In **Server entfernen Konfigurationsdialogfeld**, überprüfen Sie die Informationen und eine Warnung aus, und klicken Sie dann auf **Ja** -Serverobjekt und Metadaten entfernt.

   An diesem Punkt bestätigt Ntdsutil an, dass der Domänencontroller wurde erfolgreich entfernt wurde. Wenn Sie eine Fehlermeldung, die angibt erhalten, dass das Objekt nicht gefunden werden kann, der Domänencontroller möglicherweise zuvor entfernt wurden.

6. Auf der `metadata cleanup:` und `ntdsutil:` eingabeaufforderungen, Typ `quit`, und drücken Sie dann die EINGABETASTE.

7. So bestätigen Sie zum Entfernen des Domänencontrollers:

   Active Directory-Benutzer und-Computer zu öffnen. Klicken Sie in der Domäne der entfernten Domänencontroller, auf **Domänencontroller**. Klicken Sie im Detailbereich klicken sollte ein Objekt für den Domänencontroller, den Sie entfernt nicht angezeigt werden.

   Öffnen Sie Active Directory-Standorte und Dienste. Navigieren Sie zu der **Server** Container, und bestätigen Sie, dass das Serverobjekt für den Domänencontroller, den Sie entfernt kein NTDS-Einstellungsobjekt. Wenn keine untergeordneten Objekte unterhalb des Serverobjekts angezeigt werden, können Sie das Server-Objekt löschen. Wenn ein untergeordnetes Objekt angezeigt wird, löschen Sie nicht das Serverobjekt da eine andere Anwendung das Objekt verwendet wird.

## <a name="see-also"></a>Siehe auch

* [Herabstufen von Domänencontrollern](Demoting-Domain-Controllers-and-Domains--Level-200-.md)
* [Ntdsutil-Befehlsreferenz](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc753343(v=ws.10))
