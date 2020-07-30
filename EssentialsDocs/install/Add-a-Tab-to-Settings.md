---
title: Hinzufügen einer Registerkarte zu "Einstellungen"
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.topic: article
ms.assetid: aac6b7f3-9020-46c3-a83f-b81542300385
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: d974f4dc53b9ce389254b162a3305b277181ceed
ms.sourcegitcommit: d99bc78524f1ca287b3e8fc06dba3c915a6e7a24
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/27/2020
ms.locfileid: "87181536"
---
# <a name="add-a-tab-to-settings"></a>Hinzufügen einer Registerkarte zu "Einstellungen"

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Sie können eine Registerkarte zu "Einstellungen" auf dem Dashboard hinzufügen. Dazu erstellen und installieren Sie eine Codeassembly, die vom Einstellungs-Manager im Betriebssystem verwendet wird.

## <a name="add-a-tab-to-settings"></a>Hinzufügen einer Registerkarte zu "Einstellungen"
 Zum Hinzufügen einer Registerkarte zu "Einstellungen" führen Sie folgende Aufgaben aus:

-   [Hinzufügen einer Implementierung der ISettingsData-Schnittstelle zur Assembly](Add-a-Tab-to-Settings.md#BKMK_ISettingsData).

-   [Signieren der Assembly mit einer Authenticode-Signatur](Add-a-Tab-to-Settings.md#BKMK_SignAssembly).

-   [Installieren der Assembly auf dem Referenzcomputer](Add-a-Tab-to-Settings.md#BKMK_InstallAssembly).

###  <a name="add-an-implementation-of-the-isettingsdata-interface-to-the-assembly"></a><a name="BKMK_ISettingsData"></a>Hinzufügen einer Implementierung der isettingsdata-Schnittstelle zur Assembly
 Die ISettingsData-Schnittstelle ist im Namespace "Microsoft.WindowsServerSolutions.Settings" der Assembly "AdminCommon.dll" enthalten, die sich im Ordner "\Programme\Windows Server\Bin" befindet.

##### <a name="to-add-the-isettingsdata-code-to-the-assembly"></a>So fügen Sie der Assembly den Code für "ISettingsData" hinzu

1.  Öffnen Sie Visual Studio 2010 als Administrator, indem Sie im Menü **Start** auf das Programm klicken und **Als Administrator ausführen** auswählen.

2.  Klicken Sie auf **Datei**, auf **Neu** und anschließend auf **Projekt**.

3.  Klicken Sie im Dialogfeld **Neues Projekt** auf **Visual C#**, klicken Sie auf **Klassenbibliothek**, geben Sie **DashboardSettingsPage** als Namen für die Projektmappe ein, und klicken Sie dann auf **OK**.

    > [!IMPORTANT]
    >  Die auf dem Server installierte Assembly muss die Bezeichnung "DashboardSettingsPage.dll" erhalten. Kopieren Sie anschließend die DLL in %ProgramFiles%\Windows Server\Bin\OEM.

4.  Erstellen Sie das Steuerelement, das Sie auf der Registerkarte verwenden möchten. In diesem Beispiel hat das Einstellungs Steuerelement den Namen mysettingscontrol.

5.  Benennen Sie die Datei "Class1.cs" um, beispielsweise zu "MySettingTab.cs".

6.  Fügen Sie einen Verweis auf die Datei "AdminCommon.dll" hinzu.

7.  Fügen Sie die folgende using-Anweisung hinzu:

    ```c#
    using Microsoft.WindowsServerSolutions.Settings;
    ```

8.  Ändern Sie den Namespace und den Klassenheader entsprechend dem folgenden Beispiel:

    ```

    namespace DashboardSettingsPage
    {
        public class MySettingTab : ISettingsData
        {
        }
    }

    ```

9. Instanziieren Sie eine Instanz des Steuer Elements, das Sie für die Registerkarte erstellt haben. Zum Beispiel:

    ```c#
    private MySettingsControl tab;
    ```

10. Fügen Sie den Konstruktor für die Klasse hinzu. Mit dem folgenden Codebeispiel wird der Konstruktor veranschaulicht:

    ```

    public MySettingTab()
    {
       tab = new MySettingsControl();
    }
    ```

11. Fügen Sie die Commit-Methode hinzu, die Änderungen an Einstellungen übermittelt. Mit dem folgenden Codebeispiel wird die Commit-Methode veranschaulicht:

    ```

    void ISettingsData.Commit(bool dismissed)
    {
       // Implement the code that is required to submit your setting changes
    }
    ```

12. Fügen Sie die TabControl-Methode hinzu, die das Steuerelement für die Registerkarte identifiziert. Im folgenden Codebeispiel wird die TabControl-Methode veranschaulicht:

    ```

    System.Windows.Forms.Control ISettingsData.TabControl
    {
       get { return tab; }
    }
    ```

13. Fügen Sie die tabid-Methode hinzu, die einen eindeutigen Bezeichner für die Registerkarte bereitstellt. Im folgenden Codebeispiel wird die tabid-Methode veranschaulicht:

    ```

    private Guid id = Guid.NewGuid();

    Guid ISettingsData.TabId
    {
       get { return id; }
    }
    ```

14. Fügen Sie die TabOrder-Methode hinzu, die die Reihenfolge der Registerkarten zurückgibt. Im folgenden Codebeispiel wird die TabOrder-Methode veranschaulicht:

    ```

    int ISettingsData.TabOrder
    {
       get { return 0; }
    }
    ```

    > [!NOTE]
    >  Die Reihenfolge der Registerkarten wird mithilfe von Zahlen definiert. Die erste Zahl ist 0. Die integrierten Microsoft-Registerkarten mit Einstellungen werden zuerst angezeigt. Dann werden Ihre Registerkarten in der von Ihnen definierten Reihenfolge angezeigt. Wenn Sie beispielsweise über drei Registerkarten mit Einstellungen verfügen, geben Sie die Reihenfolge der Registerkarten mit 0, 1 und 2 an, basierend auf der gewünschten Anzeigereihenfolge.

15. Fügen Sie die tabtitle-Methode hinzu, die den Titel der Registerkarte bereitstellt. Im folgenden Codebeispiel wird die tabtitle-Methode veranschaulicht:

    ```

    string ISettingsData.TabTitle
    {
      get { return "My Settings Tab"; }
    }
    ```

    > [!NOTE]
    >  Um eine Lokalisierung zu ermöglichen, kann der Titeltext auch aus einer Ressourcendatei stammen.

16. Speichern und erstellen Sie die Projektmappe.

###  <a name="sign-the-assembly-with-an-authenticode-signature"></a><a name="BKMK_SignAssembly"></a>Signieren der Assembly mit einer Authenticode-Signatur
 Sie müssen die Assembly mit Authenticode signieren, damit sie im Betriebssystem verwendet werden kann. Weitere Informationen zum Signieren der Assembly finden Sie unter [Signieren und Überprüfen von Code mit Authenticode](https://msdn.microsoft.com/library/ms537364\(VS.85\).aspx#SignCode).

###  <a name="install-the-assembly-on-the-reference-computer"></a><a name="BKMK_InstallAssembly"></a>Installieren der Assembly auf dem Referenz Computer
 Platzieren Sie nach der erfolgreichen Erstellung der Projektmappe eine Kopie der Datei "DashboardSettingsPage.dll" im folgenden Ordner auf dem Referenzcomputer:

 **%Programfiles%\Windows Server\Bin\OEM**

## <a name="see-also"></a>Weitere Informationen
 [Erstellen und Anpassen des Images](Creating-and-Customizing-the-Image.md) [weitere Anpassungen](Additional-Customizations.md) [Vorbereiten des Abbilds für die Bereitstellung](Preparing-the-Image-for-Deployment.md) [Testen der Kundenfreundlichkeit](Testing-the-Customer-Experience.md)