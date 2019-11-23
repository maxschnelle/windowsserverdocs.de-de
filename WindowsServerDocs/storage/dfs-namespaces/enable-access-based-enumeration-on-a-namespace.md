---
title: Aktivieren der zugriffsbasierten Aufzählungen für einen Namespace
description: Dieser Artikel beschreibt, wie Sie die zugriffsbasierte Aufzählungen für einen Namespace aktivieren.
ms.date: 6/5/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 246df5b13a1dbea614886ab7fe445dd448ae1763
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402177"
---
# <a name="enable-access-based-enumeration-on-a-namespace"></a>Aktivieren Sie die zugriffsbasierte Aufzählungen für einen Namespace

> Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

Bei der zugriffsbasierten Aufzählung werden Dateien und Ordner ausgeblendet, für die die Benutzer keine Zugriffsberechtigung besitzen. Standardmäßig ist dieses Feature nicht für DFS-Namespaces aktiviert. Sie können die zugriffsbasierte Aufzählung von DFS-Ordnern mithilfe der DFS-Verwaltung aktivieren. Zum Steuern der zugriffsbasierten Aufzählung von Dateien und Ordnern in Ordnerzielen müssen Sie die zugriffsbasierte Aufzählung für jeden freigegebenen Ordner mithilfe der Freigabe- und Speicherverwaltung aktivieren.

Um die Zugriffs basierte Enumeration für einen Namespace zu aktivieren, muss auf allen Namespace Servern Windows Server 2008 oder höher ausgeführt werden. Außerdem müssen Domänen basierte Namespaces den Windows Server 2008-Modus verwenden. Informationen zu den Anforderungen des Windows Server 2008-Modus finden Sie unter [Auswählen eines Namespace Typs](choose-a-namespace-type.md).

In einigen Umgebungen kann das Aktivieren der zugriffsbasierten Aufzählung eine hohe CPU-Auslastung auf dem Server hervorrufen und eine langsame Reaktionszeiten für Benutzer verursachen.

> [!NOTE]
> Wenn Sie die Domänen Funktionsebene auf Windows Server 2008 aktualisieren, während vorhandene Domänen basierte Namespaces vorhanden sind, ermöglicht Ihnen die DFS-Verwaltung die Aktivierung der Zugriffs basierten Enumeration für diese Namespaces. Es ist jedoch nicht möglich, Berechtigungen zu bearbeiten, um Ordner aus beliebigen Gruppen oder Benutzern auszublenden, es sei denn, Sie migrieren die Namespaces zum Windows Server 2008-Modus. Weitere Informationen finden Sie unter [Migrieren eines domänenbasierten Namespaces zum Windows Server 2008-Modus](migrate-a-domain-based-namespace-to-windows-server-2008-mode.md).


Um die zugriffsbasierte Aufzählung mit DFS-Namespaces zu verwenden, müssen Sie folgende Schritte ausführen:

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

2.  Geben Sie den folgenden Befehl ein, wobei *< Namespace\_root >* der Stamm des-Namespace ist:

    ```  
    dfsutil property abe enable \\ <namespace_root>
    ```

> [!TIP]
> Verwenden Sie zum Verwalten der zugriffsbasierten Aufzählung auf einem Namespace mithilfe von Windows PowerShell die Cmdlets [Set-DfsnRoot](https://technet.microsoft.com/library/jj884281.aspx), [Grant-DfsnAccess](https://technet.microsoft.com/library/jj884272.aspx) und [Revoke-DfsnAccess](https://technet.microsoft.com/library/jj884273.aspx). Das DFSN Windows PowerShell-Modul wurde in Windows Server 2012 eingeführt.

Sie können steuern, welche Benutzer und Gruppen einzelne DFS-Ordner mithilfe der Windows-Benutzeroberfläche oder über eine Befehlszeile sehen können.

## <a name="to-control-folder-visibility-by-using-the-windows-interface"></a>Steuern Sie die Sichtbarkeit der Ordner mit der Windows-Benutzeroberfläche

1.  Suchen Sie in der Konsolenstruktur unter dem **Namespaces** Knoten den Ordner mit den Zielen, für die Sie die Sichtbarkeit steuern möchten, klicken Sie mit der rechten Maustaste darauf und klicken Sie dann auf **Eigenschaften**.

2.  Klicken Sie auf die Registerkarte **Erweitert**.

3.  Klicken Sie auf **Explizite Berechtigungen für den DFS-Ordner festlegen** und dann auf **Berechtigungen konfigurieren**.

4.  Hinzufügen oder Entfernen von Gruppen oder Benutzern durch klicken auf **Hinzufügen** oder **Entfernen**.

5.  Um Benutzern die Ansicht von DFS-Ordnern zu ermöglichen, wählen Sie den Gruppen- oder Benutzernamen, und wählen Sie dann das Kontrollkästchen **Zulassen** aus.

    Um Benutzern die Ansicht der Ordnern auszublenden, wählen Sie den Gruppen- oder Benutzernamen, und wählen Sie dann das Kontrollkästchen **Zulassen** aus.

## <a name="to-control-folder-visibility-by-using-a-command-line"></a>So steuern Sie die Sichtbarkeit der Ordner über eine Befehlszeile

1. Öffnen Sie ein Eingabeaufforderungsfenster auf einem Server, auf dem der Rollendienst **Verteiltes Dateisystem** oder die Funktion **DFS-Tools** installiert ist.

2. Geben Sie den folgenden Befehl ein, wobei *&lt;dfspath&gt;* der Pfad des DFS-Ordners (Link), *< Domänen\\Kontos >* der Name der Gruppe bzw. des Benutzerkontos ist, und *(...)* durch zusätzliche Access Control Einträge (ACEs) ersetzt wird:

   ```
   dfsutil property sd grant <DFSPath> DOMAIN\Account:R (...) Protect Replace
   ```

   Wenn Sie z. b. vorhandene Berechtigungen durch Berechtigungen ersetzen möchten, die dem Ordner Domänen-Admins und der Gruppe "Azure-\\-Trainer" Lesezugriff (R) auf den Ordner "\\Ordner" "" von "Azure".

   ```
   dfsutil property sd grant \\contoso.office\public\training "CONTOSO\Domain Admins":R CONTOSO\Trainers:R Protect Replace 
   ```

3. Um zusätzliche Aufgaben über die Befehlszeile auszuführen, verwenden Sie folgende Befehle:


| Befehl | Beschreibung |
|---|---|
|[Dfsutil-Eigenschaft SD Deny](https://msdn.microsoft.com/library/dd759150(v=ws.11).aspx)|Dies verweigert Gruppen oder Benutzern die Möglichkeit, den Ordner zu sehen.|
|[Dfsutil-Eigenschaft SD Reset](https://msdn.microsoft.com/library/dd759150(v=ws.11).aspx) |Entfernt sämtliche Berechtigungen aus dem Ordner.|
|[Dfsutil-Eigenschaft, SD-Widerruf](https://msdn.microsoft.com/library/dd759150(v=ws.11).aspx)| Entfernt den ACE einer Gruppe oder eines Benutzers aus dem Ordner. |

## <a name="see-also"></a>Weitere Informationen

-   [Erstellen eines DFS-Namespaces](create-a-dfs-namespace.md)
-   [Delegieren von Verwaltungsberechtigungen für DFS-Namespaces](delegate-management-permissions-for-dfs-namespaces.md)
-   [Installieren von DFS](https://technet.microsoft.com/library/cc731089(v=ws.11).aspx)
-   [Verwenden von geerbten Berechtigungen mit Zugriffs basierter Enumeration](using-inherited-permissions-with-access-based-enumeration.md)