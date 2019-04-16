---
title: "Aktivieren Sie die zugriffsbasierte Aufzählungen für einen Namespace"
description: "Dieser Artikel beschreibt, wie Sie die zugriffsbasierte Aufzählungen für einen Namespace aktivieren."
ms.date: 6/5/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 8c7ff3bde0a88c7c64cb5b1b6e656adab0e14452
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2017
---
# <a name="enable-access-based-enumeration-on-a-namespace"></a>Aktivieren Sie die zugriffsbasierte Aufzählungen für einen Namespace

> Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server2012 R2, Windows Server 2012, Windows Server2008 R2, Windows Server 2008

Bei der zugriffsbasierten Aufzählung werden Dateien und Ordner ausgeblendet, für die die Benutzer keine Zugriffsberechtigung besitzen. Standardmäßig ist dieses Feature nicht für DFS-Namespaces aktiviert. Sie können die zugriffsbasierte Aufzählung von DFS-Ordnern mithilfe der DFS-Verwaltung aktivieren. Zum Steuern der zugriffsbasierten Aufzählung von Dateien und Ordnern in Ordnerzielen müssen Sie die zugriffsbasierte Aufzählung für jeden freigegebenen Ordner mithilfe der Freigabe- und Speicherverwaltung aktivieren.

Zum Aktivieren der zugriffsbasierten Aufzählung für einen Namespace muss auf allen Namespaceservern Windows Server 2008 oder höher ausgeführt werden. Darüber hinaus müssen domänenbasierte Namespaces den Windows Server2008-Modus ausführen. Informationen zu den Anforderungen des Windows Server2008-Modus finden Sie unter [Namespacetyp auswählen](choose-a-namespace-type.md).

In einigen Umgebungen kann das Aktivieren der zugriffsbasierten Aufzählung eine hohe CPU-Auslastung auf dem Server hervorrufen und eine langsame Reaktionszeiten für Benutzer verursachen.

> [!NOTE]
> Wenn Sie die Domänenfunktionsebene auf Windows Server2008 aktualisieren, während vorhandene domänenbasierte Namespaces existieren, ermöglicht die DFS-Verwaltung Ihnen, die zugriffsbasierte Aufzählung in diesen Namespaces zu aktivieren. Sie sind allerdings nicht in der Lage, Berechtigungen zum Ausblenden von Ordner für Gruppen oder Benutzer zu bearbeiten, es sei denn, Sie migrieren die Namespaces auf den Windows Server2008-Modus. Weitere Informationen finden Sie unter [Migrieren eines domänenbasierten Namespaces zum Windows Server 2008-Modus](migrate-a-domain-based-namespace-to-windows-server-2008-mode.md).


Um die zugriffsbasierte Aufzählung mit DFS-Namespaces zu verwenden, müssen Sie folgende Schritteausführen:

-   Aktivieren Sie die zugriffsbasierte Aufzählungen für einen Namespace
-   Kontrollieren Sie, welche Benutzer und Gruppen einzelne DFS-Ordner anzeigen können


> [!WARNING]
> Benutzer können trotz der zugriffsbasierten einen Verweis auf ein Ordnerziel abrufen, wenn sie den DFS-Pfad bereits kennen. Nur die Freigabeberechtigungen oder die NTFS-Dateisystemberechtigungen für das Ordnerziel (freigegebener Ordner) selbst kann verhindern, dass Benutzer den Zugriff auf ein Ordnerziel erhalten. Berechtigungen für DFS-Ordner dienen nur zum Anzeigen oder Ausblenden von DFS-Ordnern, nicht für die Steuerung des Zugriffs und machen den Lesezugriff die einzige entsprechende Berechtigung auf der Ebene der DFS-Ordner. Weitere Informationen finden Sie unter [Verwenden vererbter Berechtigungen mit zugriffsbasierter Aufzählung](https://technet.microsoft.com/library/dd834874(v=ws.11).aspx)

<br />
Sie können die zugriffsbasierte Aufzählung für einen Namespace mithilfe der Windows-Benutzeroberfläche oder über eine Befehlszeile aktivieren.

## <a name="to-enable-access-based-enumeration-by-using-the-windows-interface"></a>So aktivieren Sie die zugriffsbasierte Aufzählung mithilfe der Windows-Benutzeroberfläche

1.  Klicken Sie in der Konsolenstruktur unter dem Knoten **Namespaces** mit der rechten Maustaste auf den entsprechenden Namespace, und klicken Sie dann auf **Eigenschaften**.

2.  Klicken Sie auf die Registerkarte **Erweitert** und wählen Sie das Kontrollkästchen **Aktivieren der zugriffsbasierten Aufzählung für diesen Namespace** aus.

## <a name="to-enable-access-based-enumeration-by-using-a-command-line"></a>So aktivieren Sie die zugriffsbasierte Aufzählung mithilfe einer Befehlszeile

1.  Öffnen Sie ein Eingabeaufforderungsfenster auf einem Server, auf dem der Rollendienst **Verteiltes Dateisystem** oder die Funktion **DFS-Tools** installiert ist.

2.  Geben Sie folgenden Befehl ein, wobei *<Namespace\_Stamm>* der Stamm des Namespace ist:

    ```  
    dfsutil property abe enable \\ <namespace_root>
    ```

> [!TIP]
> Verwenden Sie zum Verwalten der zugriffsbasierten Aufzählung auf einem Namespace mithilfe von Windows PowerShell die Cmdlets [Set-DfsnRoot](https://technet.microsoft.com/library/jj884281.aspx), [Grant-DfsnAccess](https://technet.microsoft.com/library/jj884272.aspx) und [Revoke-DfsnAccess](https://technet.microsoft.com/library/jj884273.aspx). Das DFSN Windows PowerShell-Modul wurde in Windows Server2012 eingeführt.

Sie können steuern, welche Benutzer und Gruppen einzelne DFS-Ordner mithilfe der Windows-Benutzeroberfläche oder über eine Befehlszeile sehen können.

## <a name="to-control-folder-visibility-by-using-the-windows-interface"></a>Steuern Sie die Sichtbarkeit der Ordner mit der Windows-Benutzeroberfläche

1.  Suchen Sie in der Konsolenstruktur unter dem **Namespaces** Knoten den Ordner mit den Zielen, für die Sie die Sichtbarkeit steuern möchten, klicken Sie mit der rechten Maustaste darauf und klicken Sie dann auf **Eigenschaften**.

2.  Klicken Sie auf die Registerkarte **Erweitert**.

3.  Klicken Sie auf **Explizite Berechtigungen für den DFS-Ordner festlegen** und dann auf **Berechtigungen konfigurieren**.

4.  Hinzufügen oder Entfernen von Gruppen oder Benutzern durch klicken auf **Hinzufügen** oder **Entfernen**.

5.  Um Benutzern die Ansicht von DFS-Ordnern zu ermöglichen, wählen Sie den Gruppen- oder Benutzernamen, und wählen Sie dann das Kontrollkästchen **Zulassen** aus.

    Um Benutzern die Ansicht der Ordnern auszublenden, wählen Sie den Gruppen- oder Benutzernamen, und wählen Sie dann das Kontrollkästchen **Zulassen** aus.

## <a name="to-control-folder-visibility-by-using-a-command-line"></a>So steuern Sie die Sichtbarkeit der Ordner über eine Befehlszeile

1.  Öffnen Sie ein Eingabeaufforderungsfenster auf einem Server, auf dem der Rollendienst **Verteiltes Dateisystem** oder die Funktion **DFS-Tools** installiert ist.

2.  Geben Sie folgenden Befehl ein, wobei *&lt;DFSPath&gt;* der Pfad des DFS-Ordners (Link) ist, *<DOMAIN\\Account>* der Name des Gruppen- oder Benutzerkontos ist und *(...)* mit zusätzlichen Zugriffssteuerungseinträgen (ACEs) ersetzt wird:

    ```
    dfsutil property sd grant <DFSPath> DOMAIN\Account:R (...) Protect Replace
    ```

    Um vorhandene Berechtigungen mit den Berechtigungen zu ersetzen, die den Domänen-Admins und CONTOSO\\Trainergruppen den Lesezugriff (R) auf den Ordner \\contoso.office\public\training zu ermöglichen, geben Sie folgenden Befehl ein:

   ```
   dfsutil property sd grant \\contoso.office\public\training "CONTOSO\Domain Admins":R CONTOSO\Trainers:R Protect Replace 
   ```

3. Um zusätzliche Aufgaben über die Befehlszeile auszuführen, verwenden Sie folgende Befehle:


| Befehl | Beschreibung |
|---|---|
|[Dfsutil property sd deny](https://msdn.microsoft.com/library/dd759150(v=ws.11).aspx)|Dies verweigert Gruppen oder Benutzern die Möglichkeit, den Ordner zu sehen.|
|[Dfsutil property sd reset](https://msdn.microsoft.com/library/dd759150(v=ws.11).aspx) |Entfernt sämtliche Berechtigungen aus dem Ordner.|
|[Dfsutil property sd revoke](https://msdn.microsoft.com/library/dd759150(v=ws.11).aspx)| Entfernt den ACE einer Gruppe oder eines Benutzers aus dem Ordner. |

## <a name="see-also"></a>Weitere Informationen:

-   [Erstellen eines DFS-Namespaces](create-a-dfs-namespace.md)
-   [Delegieren von Verwaltungsberechtigungen für DFS-Namespaces](delegate-management-permissions-for-dfs-namespaces.md)
-   [Installieren von DFS](https://technet.microsoft.com/library/cc731089(v=ws.11).aspx)
-   [Verwenden vererbter Berechtigungen mit zugriffsbasierter Aufzählung](using-inherited-permissions-with-access-based-enumeration.md)