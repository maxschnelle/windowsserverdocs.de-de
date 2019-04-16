---
title: "Hinzufügen einer Registerkarte zu Einstellungen"
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aac6b7f3-9020-46c3-a83f-b81542300385
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 9eaa1aa5a9c5e8d4c2e36f2000e0adecc83245d9
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="add-a-tab-to-settings"></a>Hinzufügen einer Registerkarte zu Einstellungen

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

Sie können eine Registerkarte Einstellungen auf dem Dashboard hinzufügen, indem erstellen und installieren Sie eine Codeassembly, die vom Einstellungs-Manager im Betriebssystem verwendet wird.  
  
## <a name="add-a-tab-to-settings"></a>Hinzufügen einer Registerkarte zu Einstellungen  
 Hinzufügen einer Registerkarte Einstellungen durch Ausführen der folgenden Aufgaben:  
  
-   [Hinzufügen einer Implementierung der ISettingsData-Schnittstelle zur Assembly](Add-a-Tab-to-Settings.md#BKMK_ISettingsData).  
  
-   [Signieren der Assembly mit Authenticode-Signatur](Add-a-Tab-to-Settings.md#BKMK_SignAssembly).  
  
-   [Installieren Sie die Assembly auf dem Referenzcomputer](Add-a-Tab-to-Settings.md#BKMK_InstallAssembly).  
  
###  <a name="BKMK_ISettingsData"></a>Hinzufügen einer Implementierung der ISettingsData-Schnittstelle zur assembly  
 Die ISettingsData-Schnittstelle ist im Namespace "Microsoft.WindowsServerSolutions.Settings" der Assembly AdminCommon.dll enthalten \Programme\Windows Server\Bin befindet.  
  
##### <a name="to-add-the-isettingsdata-code-to-the-assembly"></a>Die ISettingsData-Code auf die Assembly hinzufügen  
  
1.  Öffnen Sie Visual Studio2010 als Administrator mit der rechten Maustaste in das Programm in die **starten** Menü und Auswählen von **als Administrator ausführen**.  
  
2.  Klicken Sie auf **Datei**, klicken Sie auf **neu**, und klicken Sie dann auf **Projekt**.  
  
3.  In der **neues Projekt** Dialogfeld, klicken Sie auf **Visual C#-**, klicken Sie auf **Klassenbibliothek**, geben Sie **DashboardSettingsPage** für den Namen für die Projektmappe, und klicken Sie dann auf **OK**.  
  
    > [!IMPORTANT]
    >  Die Assembly, die auf dem Server installiert ist, muss den Namen DashboardSettingsPage.dll und kopieren Sie die DLL in %ProgramFiles%\Windows Server\Bin\OEM.  
  
4.  Erstellen Sie das Steuerelement, das Sie auf der Registerkarte verwendet werden sollen. In diesem Beispiel wird das Steuerelement für Einstellungen MySettingsControl bezeichnet.  
  
5.  Benennen Sie die Datei Class1.cs. Beispielsweise MySettingTab.cs.  
  
6.  Fügen Sie einen Verweis auf die Datei AdminCommon.dll.  
  
7.  Fügen Sie die folgenden using-Anweisung:  
  
    ```c#  
    using Microsoft.WindowsServerSolutions.Settings;  
    ```  
  
8.  Ändern Sie den Namespace und den klassenheader entsprechend dem folgenden Beispiel:  
  
    ```  
  
    namespace DashboardSettingsPage  
    {  
        public class MySettingTab : ISettingsData  
        {  
        }  
    }  
  
    ```  
  
9. Instanziieren Sie eine Instanz des Steuerelements, das Sie für die Registerkarte erstellt haben. Zum Beispiel:  
  
    ```c#  
    private MySettingsControl tab;  
    ```  
  
10. Fügen Sie den Konstruktor für die Klasse. Im folgenden Codebeispiel wird der Konstruktor veranschaulicht:  
  
    ```  
  
    public MySettingTab()  
    {  
       tab = new MySettingsControl();  
    }  
    ```  
  
11. Fügen Sie die Commit-Methode, die die Änderungen an Einstellungen übermittelt. Das folgende Codebeispiel zeigt die Commit-Methode:  
  
    ```  
  
    void ISettingsData.Commit(bool dismissed)  
    {  
       // Implement the code that is required to submit your setting changes  
    }  
    ```  
  
12. Fügen Sie die TabControl-Methode, die das Steuerelement für die Registerkarte identifiziert. Das folgende Codebeispiel zeigt die TabControl-Methode:  
  
    ```  
  
    System.Windows.Forms.Control ISettingsData.TabControl  
    {  
       get { return tab; }  
    }  
    ```  
  
13. Fügen Sie die TabId-Methode, die einen eindeutigen Bezeichner für die Registerkarte bereitstellt. Das folgende Codebeispiel zeigt die TabId-Methode:  
  
    ```  
  
    private Guid id = Guid.NewGuid();  
  
    Guid ISettingsData.TabId  
    {  
       get { return id; }  
    }  
    ```  
  
14. Fügen Sie die TabOrder-Methode, die die Reihenfolge der Registerkarten zurückgibt. Das folgende Codebeispiel zeigt die TabOrder-Methode:  
  
    ```  
  
    int ISettingsData.TabOrder  
    {  
       get { return 0; }  
    }  
    ```  
  
    > [!NOTE]
    >  Die Reihenfolge der Registerkarten wird mithilfe von Zahlen, beginnend mit 0 definiert. Die Microsoft-Registerkarten integrierten Einstellungen angezeigt werden, und klicken Sie dann Ihren Registerkarten werden angezeigt, basierend auf der Reihenfolge, die Sie definieren. Wenn beispielsweise Sie über drei Registerkarten mit Einstellungen verfügen, geben Sie die Reihenfolge der Registerkarten als 0, 1 und 2 basierend auf der Reihenfolge der Registerkarten angezeigt werden soll.  
  
15. Fügen Sie die TabTitle-Methode, die den Titel der Registerkarte bereitstellt. Das folgende Codebeispiel zeigt die TabTitle-Methode:  
  
    ```  
  
    string ISettingsData.TabTitle  
    {  
      get { return "My Settings Tab"; }  
    }  
    ```  
  
    > [!NOTE]
    >  Der Titeltext kommen auch aus einer Ressourcendatei, um die Lokalisierung zu ermöglichen.  
  
16. Speichern Sie und erstellen Sie die Projektmappe.  
  
###  <a name="BKMK_SignAssembly"></a>Signieren der Assembly mit Authenticode-Signatur  
 Sie müssen mit Authenticode Signieren der Assembly für sie in das Betriebssystem verwendet werden. Weitere Informationen zum Signieren der Assembly finden Sie unter [signieren und Überprüfen von Code mit Authenticode](https://msdn.microsoft.com/library/ms537364\(VS.85\).aspx#SignCode).  
  
###  <a name="BKMK_InstallAssembly"></a>Installieren Sie die Assembly auf dem Referenzcomputer  
 Nachdem Sie die Projektmappe erfolgreich erstellt haben, platzieren Sie eine Kopie der Datei DashboardSettingsPage.dll im folgenden Ordner auf dem Referenzcomputer:  
  
 **%Programfiles%\Windows Server\Bin\OEM**  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen und Anpassen des Abbilds](Creating-and-Customizing-the-Image.md)   
 [Weitere Anpassungen](Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](Testing-the-Customer-Experience.md)