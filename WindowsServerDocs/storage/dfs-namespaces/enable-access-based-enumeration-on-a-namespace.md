---
title: Aktivieren Sie zugriffsbasierte Aufzählungen für einen Namespace
description: In diesem Artikel wird beschrieben, wie Sie die Zugriffs basierte Enumeration für einen Namespace aktivieren.
ms.date: 6/5/2017
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 507af0f3cdd76ab7af59092f8f099225c113edaa
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87936124"
---
# <a name="enable-access-based-enumeration-on-a-namespace"></a>Aktivieren der Zugriffs basierten Enumeration für einen Namespace

> Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

Die Zugriffs basierte Enumeration blendet Dateien und Ordner aus, für die Benutzer keine Zugriffsberechtigungen haben. Standardmäßig ist dieses Feature für DFS-Namespaces nicht aktiviert. Sie können die Zugriffs basierte Enumeration von DFS-Ordnern mithilfe der DFS-Verwaltung aktivieren. Um die Zugriffs basierte Enumeration von Dateien und Ordnern in Ordner Zielen zu steuern, müssen Sie die Zugriffs basierte Enumeration für jeden freigegebenen Ordner mithilfe der Freigabe-und Speicherverwaltung aktivieren.

Um die Zugriffs basierte Enumeration für einen Namespace zu aktivieren, muss auf allen Namespace Servern Windows Server 2008 oder höher ausgeführt werden. Außerdem müssen Domänen basierte Namespaces den Windows Server 2008-Modus verwenden. Informationen zu den Anforderungen des Windows Server 2008-Modus finden Sie unter [Auswählen eines Namespace Typs](choose-a-namespace-type.md).

In einigen Umgebungen kann die Aktivierung der Zugriffs basierten Aufzählung zu einer hohen CPU-Auslastung auf dem Server und zu langsamen Reaktionszeiten für Benutzer führen.

> [!NOTE]
> Wenn Sie die Domänen Funktionsebene auf Windows Server 2008 aktualisieren, während vorhandene Domänen basierte Namespaces vorhanden sind, ermöglicht Ihnen die DFS-Verwaltung die Aktivierung der Zugriffs basierten Enumeration für diese Namespaces. Es ist jedoch nicht möglich, Berechtigungen zu bearbeiten, um Ordner aus beliebigen Gruppen oder Benutzern auszublenden, es sei denn, Sie migrieren die Namespaces zum Windows Server 2008-Modus. Weitere Informationen finden Sie unter [Migrieren eines domänenbasierten Namespaces zum Windows Server 2008-Modus](migrate-a-domain-based-namespace-to-windows-server-2008-mode.md).


Wenn Sie die Zugriffs basierte Enumeration mit DFS-Namespaces verwenden möchten, müssen Sie die folgenden Schritte ausführen:

-   Aktivieren der Zugriffs basierten Enumeration für einen Namespace
-   Steuern, welche Benutzer und Gruppen einzelne DFS-Ordner anzeigen können


> [!WARNING]
> Die Zugriffs basierte Enumeration verhindert nicht, dass Benutzer einen Verweis auf ein Ordner Ziel erhalten, wenn Sie den DFS-Pfad bereits kennen. Nur die Freigabe Berechtigungen oder die NTFS-Dateisystem Berechtigungen des Ordner Ziels (frei gegebener Ordner) können verhindern, dass Benutzer auf ein Ordner Ziel zugreifen. DFS-Ordner Berechtigungen werden nur zum Anzeigen oder Ausblenden von DFS-Ordnern verwendet, nicht zum Steuern des Zugriffs, sodass Lesezugriff auf die einzige relevante Berechtigung auf der DFS-Ordnerebene ermöglicht wird. Weitere Informationen finden Sie unter [Verwenden von geerbten Berechtigungen mit Zugriffs basierter Enumeration](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd834874(v=ws.11)) .

<br />
Sie können die Zugriffs basierte Enumeration für einen Namespace aktivieren, indem Sie entweder die Windows-Benutzeroberfläche oder eine Befehlszeile verwenden.

## <a name="to-enable-access-based-enumeration-by-using-the-windows-interface"></a>So aktivieren Sie die Zugriffs basierte Enumeration mithilfe der Windows-Benutzeroberfläche

1.  Klicken Sie in der Konsolen Struktur unter dem Knoten **Namespaces** mit der rechten Maustaste auf den entsprechenden Namespace, und klicken Sie dann auf **Eigenschaften** .

2.  Klicken Sie auf die Registerkarte **erweitert** , und aktivieren Sie dann das Kontrollkästchen **Zugriffs basierte Enumeration für diesen Namespace aktivieren** .

## <a name="to-enable-access-based-enumeration-by-using-a-command-line"></a>So aktivieren Sie die Zugriffs basierte Enumeration mithilfe einer Befehlszeile

1.  Öffnen Sie ein Eingabe Aufforderungs Fenster auf einem Server, auf dem die Funktion **verteiltes Dateisystem** Rollen Dienst oder **verteiltes Dateisystem Tools** installiert ist.

2.  Geben Sie den folgenden Befehl ein, wobei *<Namespace Stamm \_>* der Stamm des-Namespace ist:

    ```
    dfsutil property abe enable \\ <namespace_root>
    ```

> [!TIP]
> Verwenden Sie zum Verwalten der Zugriffs basierten Enumeration für einen Namespace mithilfe von Windows PowerShell die Cmdlets [Set-dfsnroot](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd834874(v=ws.11)), [Grant-dfsnaccess](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd834874(v=ws.11))und [Revo-dfsnaccess](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd834874(v=ws.11)) . Das DFSN-Windows PowerShell-Modul wurde in Windows Server 2012 eingeführt.

Sie können steuern, welche Benutzer und Gruppen einzelne DFS-Ordner anzeigen können, indem Sie entweder die Windows-Benutzeroberfläche oder eine Befehlszeile verwenden.

## <a name="to-control-folder-visibility-by-using-the-windows-interface"></a>So steuern Sie die Ordner Sichtbarkeit mithilfe der Windows-Benutzeroberfläche

1.  Suchen Sie in der Konsolen Struktur unter dem Knoten **Namespaces** den Ordner mit den Zielen, für die Sie die Sichtbarkeit steuern möchten, klicken Sie mit der rechten Maustaste darauf, und klicken Sie dann auf **Eigenschaften**.

2.  Klicken Sie auf die Registerkarte **Erweitert**.

3.  Klicken Sie **im DFS-Ordner auf explizite Anzeige Berechtigungen festlegen** , und konfigurieren Sie dann **Berechtigungen anzeigen**.

4.  Wenn Sie Gruppen oder Benutzer hinzufügen oder entfernen, klicken Sie auf **Hinzufügen** oder **Entfernen**.

5.  Um Benutzern den DFS-Ordner anzuzeigen, wählen Sie die Gruppe oder den Benutzer aus, und aktivieren Sie dann das Kontrollkästchen **zulassen** .

    Wenn Sie den Ordner einer Gruppe oder eines Benutzers ausblenden möchten, wählen Sie die Gruppe oder den Benutzer aus, und aktivieren Sie dann das Kontrollkästchen **ablehnen** .

## <a name="to-control-folder-visibility-by-using-a-command-line"></a>So steuern Sie die Ordner Sichtbarkeit mithilfe einer Befehlszeile

1. Öffnen Sie ein Eingabe Aufforderungs Fenster auf einem Server, auf dem die Funktion **verteiltes Dateisystem** Rollen Dienst oder **verteiltes Dateisystem Tools** installiert ist.

2. Geben Sie den folgenden Befehl ein, wobei * &lt; dfspath &gt; * der Pfad des DFS-Ordners (Link), *<Domänen \\ Kontos>* der der Name des Gruppen-oder Benutzerkontos ist, und *(...)* durch zusätzliche Access Control Einträge (ACEs) ersetzt wird:

   ```
   dfsutil property sd grant <DFSPath> DOMAIN\Account:R (...) Protect Replace
   ```

   Geben Sie beispielsweise den folgenden Befehl ein, um vorhandene Berechtigungen durch Berechtigungen zu ersetzen, die den Domänen-Admins und den Zugriffsgruppen von "Azure" den \\ Zugriff auf den Ordner "Order \\ . office\public\training" ermöglichen:

   ```
   dfsutil property sd grant \\contoso.office\public\training "CONTOSO\Domain Admins":R CONTOSO\Trainers:R Protect Replace
   ```

3. Verwenden Sie die folgenden Befehle, um zusätzliche Aufgaben an der Eingabeaufforderung auszuführen:


| Befehl | BESCHREIBUNG |
|---|---|
|[Dfsutil-Eigenschaft SD Deny](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd759150(v=ws.11))|Verweigert einer Gruppe oder einem Benutzer die Möglichkeit, den Ordner anzuzeigen.|
|[Dfsutil-Eigenschaft SD Reset](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd759150(v=ws.11)) |Entfernt alle Berechtigungen aus dem Ordner.|
|[Dfsutil-Eigenschaft, SD-Widerruf](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd759150(v=ws.11))| Entfernt einen Gruppen-oder Benutzer-ACE aus dem Ordner. |

## <a name="additional-references"></a>Weitere Verweise

-   [Erstellen eines DFS-Namespaces](create-a-dfs-namespace.md)
-   [Delegieren von Verwaltungsberechtigungen für DFS-Namespaces](delegate-management-permissions-for-dfs-namespaces.md)
-   [Installieren von DFS](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731089(v=ws.11))
-   [Verwenden von geerbten Berechtigungen mit Zugriffs basierter Enumeration](using-inherited-permissions-with-access-based-enumeration.md)
