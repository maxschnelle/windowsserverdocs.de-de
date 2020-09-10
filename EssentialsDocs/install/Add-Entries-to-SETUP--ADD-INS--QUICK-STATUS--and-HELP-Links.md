---
title: Hinzufügen von Einträgen zu SETUP, ADD-INS und KURZE STATUSINFOS sowie von Links zu HILFE
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.topic: article
ms.assetid: c0a8f10d-fd85-4c8d-b9bb-176cb1db1f46
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: b8abf96a5d07d3bcda3cfc43c4e0e960a38e465b
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89624081"
---
# <a name="add-entries-to-setup-add-ins-quick-status-and-help-links"></a>Hinzufügen von Einträgen zu SETUP, ADD-INS und KURZE STATUSINFOS sowie von Links zu HILFE

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Sie können den Aufgabenlisten **SETUP**, **ADD-INS** und **KURZE STATUSINFOS** Aufgaben hinzufügen. Zudem können Sie dem Abschnitt "Community-Links" auf der Homepage im Dashboard Links hinzufügen. Aufgaben und Links werden diesen Listen und dem Abschnitt hinzugefügt, indem die XML-Datei "OEMHomePageContent.home" oder eine eingebettete Ressourcendatei namens "OEMHomePageContent.dll" in "%ProgramFiles%\Windows Server\Bin\Addins\Home" eingefügt wird. Mithilfe der eingebetteten Ressourcendatei kann der Text in den hinzugefügten Aufgaben und Links lokalisiert werden. Die HOME-Datei enthält die XML-Definitionen von Aufgaben und Links.

## <a name="adding-tasks-to-the-setup-add-ins-quick-status-task-lists-and-adding-links-to-help-task"></a>Hinzufügen von Aufgaben zu den Aufgabenlisten SETUP, ADD-INS, KURZE STATUSINFOS und Hinzufügen von Links zur Aufgabe HILFE
 Sie können den Aufgabenlisten **SETUP**, **ADD-INS** und **KURZE STATUSINFOS** Aufgaben hinzufügen, und Sie können der Aufgabe **HILFE** Links hinzufügen, indem Sie die Aufgaben und Links mit XML definieren, optional eine eingebettete Ressourcendatei erstellen und die Datei auf dem Server installieren. Wenn die XML-Datei ohne eine Ressourcendatei auf dem Server installiert wird, muss sie in "OEMHomePageContent.home" umbenannt werden. Wenn zum Installieren einer XML-Datei und einer Ressourcendatei eine Assembly verwendet wird, muss diese den Namen "OEMHomePageContent.dll" erhalten und mit Authenticode signiert werden.

### <a name="define-the-tasks-and-links"></a>Definieren von Aufgaben und Links
 Sie können einen Text-Editor wie Editor zum Erstellen der HOME-Datei verwenden. Wenn Sie zudem eine eingebettete Ressourcendatei erstellen, können Sie die Dateien auch mit Visual Studio 2010 oder höher definieren. Im folgenden Verfahren wird gezeigt, wie die Dateien mit Visual Studio 2010 oder höher erstellt werden.

##### <a name="to-define-the-tasks-and-links"></a>So definieren Sie die Aufgaben und Links

1. Öffnen Sie Visual Studio 2010 oder höher als Administrator, indem Sie im Menü "Start" auf das Programm klicken und **Als Administrator ausführen** auswählen.

2. Klicken Sie auf **Datei**, auf **Neu** und anschließend auf **Projekt**.

3. Klicken Sie im Bereich **Vorlagen** auf **Klassenbibliothek**, geben Sie **OEMHomePageContent** in das Feld **Name** ein, und klicken Sie dann auf **OK**.

4. Löschen Sie die Datei "Class1.cs".

5. Klicken Sie mit der rechten Maustaste auf das neue Projekt, klicken Sie auf **Hinzufügen**, und klicken Sie anschließend auf **Neues Element**.

6. Klicken Sie im Bereich **Vorlagen** auf **XML-Datei**, geben Sie **OEMHomePageContent.home** in das Feld **Name** ein, und klicken Sie dann auf **Hinzufügen**.

   > [!NOTE]
   >  Wenn die XML-Datei ohne eine Ressourcendatei installiert wird, muss sie in "OEMHomePageContent.home" umbenannt werden. Wenn sie in eine Assembly aufgenommen wird, kann sie einen beliebigen Namen bekommen, die Erweiterung muss aber HOME sein.

7. Fügen Sie den folgenden XML-Code in die Datei "OEMHomePageContent.home" ein:

   ```

   <Tasks version=?2.0? xmlns=?https://schemas.microsoft.com/WindowsServerSolutions/2010/01/Dashboard>
      <SetupMyServerTasks>
         <Task name="MyTask"
            description="MyTaskDescription"
            id="GUID">
                 <Action
                 name=?MyAction1Name?
                 image=?IconForAction1?
                 type=?TaskType?
                 exelocation=?ActionExeLocation? />
                 <Action
                 name=?MyAction2Name?
                 image=?IconForAction2?
                 type=?TaskType?
                 exelocation=?ActionExeLocation? />
                  ¦
          </Task>
                  ¦
       </SetupMyServerTasks>
   <MailServiceTasks>
        <!-- Same schema as in œSetupMyServerTasks? but the tasks are shown in œConnect to Email Service? category. -->
   </MailServiceTasks>
   <LineOfBusinessTasks>
        <!-- Same schema as in œSetupMyServerTasks? but the tasks are shown in œAdd-ins? category. -->

   <GetQuickStatusTasks>
         <Task name="MyQuickStatusTask1"
            description="MyQuickStatusTask1Desc   "
            id="GUID"
            assembly="AssemblyName of quick status query implementation"
            class="ClassName of quick status query implementation"
            replaceid="GUID"/>
              <!--  Same schema as Actions in œSetupMyServerTasks? -->
            </Task>
   </GetQuickStatusTasks>
      <Links>
         <Link
            ID=?GUID?
            Title="Displayed text of the link"
            Description="A very short description"
            ShellExecPath="Path to the application or URL"/>
      </Links>
   </Tasks>
   ```

    Hierbei gilt:

   |attribute|BESCHREIBUNG|
   |---------------|-----------------|
   |Name (Aufgabe)|Der Name, der für die Aufgabe in der Liste angezeigt wird. Wenn Sie eine eingebettete Ressourcendatei erstellen, ist der Wert dieses Attributs eine Zeichenfolgenressource.|
   |Beschreibung (Aufgabe)|Die Beschreibung des Tasks. Wenn Sie eine eingebettete Ressourcendatei erstellen, ist der Wert dieses Attributs eine Zeichenfolgenressource.|
   |ID (Aufgabe)|Der Bezeichner des Tasks. Dieser Bezeichner muss eine GUID sein. Sie erstellen eine neue GUID für eine **exe** -Aufgabe, aber für eine **globale** Aufgabe verwenden Sie die GUID, die Sie beim Definieren der Aufgabe für den Aufgabenbereich der unter Registerkarte erstellt haben. Weitere Informationen zum Erstellen einer GUID finden Sie unter [Create GUID (guidgen.exe)](https://go.microsoft.com/fwlink/?LinkId=116098).|
   |image|Dieses Feld wird ignoriert.|
   |Name (Aktion)|Gibt den Namen der Aufgabe an.|
   |Typ (Aktion)|Beschreibt den Typ der Aufgabe. Die Aufgabe kann eine der folgenden sein: - **globale** Aufgabe, **exe** oder eine URL-Aufgabe. Eine **globale** Aufgabe ist dieselbe globale Aufgabe, die Sie beim Definieren der Aufgaben für den Aufgabenbereich auf der unter Registerkarte erstellt haben. Weitere Informationen zum Erstellen einer globalen Aufgabe, die im Aufgabenbereich der unter Registerkarte und in den Listen mit den ersten Schritten oder allgemeinen Aufgaben der Startseite verwendet werden kann, finden Sie unter "Erstellen der Unterstützungs Klassen". in "œgewusst wie: Erstellen einer unter Registerkarte" des [SDK für Windows Server-Lösungen](https://go.microsoft.com/fwlink/?LinkID=248648). Mit einer Aufgabe vom Typ **exe** können Anwendungen in den Listen mit Aufgaben unter "Erste Schritte" und mit allgemeinen Aufgaben ausgeführt werden.|
   |exelocation|Der Pfad der Anwendung, die der Aufgabe zugeordnet ist. Dieses Attribut wird nur für Aufgaben vom Typ **exe** verwendet.|
   |replaceid|Der Bezeichner der Aufgabe, die mit dieser Aufgabe ersetzt wird.|
   |Assembly|Der Assemblyname der Assembly, die die Klasse zum Implementieren der Abfrage des kurzen Status angibt. Die Assembly muss sich im Ordner "Program Files \ Windows Server\bin" befinden \\ .|
   |class|Der Name der Abfrage der kurzen Statusinfos der Klassenimplementierungen. Die Klasse muss die Schnittstelle **ITaskStatusQuery** implementieren.|
   |Titel (Link)|Der Text, der für den Link angezeigt wird. Wenn Sie eine eingebettete Ressourcendatei erstellen, ist der Wert dieses Attributs eine Zeichenfolgenressource.|
   |Beschreibung (Link)|Die Beschreibung des Linkziels. Wenn Sie eine eingebettete Ressourcendatei erstellen, ist der Wert dieses Attributs eine Zeichenfolgenressource.|
   |ShellExecPath|Der Pfad der Anwendung oder die URL.<br /><br /> **Hinweis:** Umgebungsvariablen werden im shellexecpath-Attribut unterstützt.|

    Im folgenden Codebeispiel wird die Definition eines Links zu einer Anwendung veranschaulicht:

   ```
   <Links>
      <Link Title="Calc" Description="Launches Calc" ShellExecPath="%windir%\system32\calc.exe" />
   </Links>
   ```

    Im folgenden Codebeispiel wird die Definition eines Links zu einer Webseite veranschaulicht:

   ```
   <Links>
      <Link Title="Browser" Description="Open browser" ShellExecPath="http://www.adventureworks.com/" />
   </Links>
   ```

8. Ändern Sie die Attributwerte, um die Aufgabe oder den Link darzustellen.

9. Klicken Sie im **Projektmappen-Explorer** mit der rechten Maustaste auf **OEMHomePageContent.home** und anschließend auf **Eigenschaften**.  Wählen Sie im Bereich **Eigenschaften** (unter **Buildvorgang**) die Option **Eingebettete Ressource** aus.

10. Speichern Sie die Datei "OEMHomePageContent.home".

    Informationen dazu, wie Sie eine Abfrage des Kurzstatus implementieren, finden Sie in den Dokumenten und Beispielen des [SDK für Windows Server-Lösungen](https://go.microsoft.com/fwlink/?LinkID=248648).

#### <a name="change-the-status-of-a-setupadd-ins-task"></a>Ändern des Status einer Aufgabe unter SETUP/ADD-INS
 Die Aufgaben unter SETUP und ADD-INS können zwischen den Statusangaben "Abgeschlossen" (konfiguriert für Add-Ins) und "Nicht abgeschlossen" (nicht konfiguriert für Add-Ins) umgeschaltet werden.

 Wenn Sie die Anwendung definieren, die der neuen Aufgabe zugeordnet ist, können Sie mithilfe der SetTaskStatus-Methode des Microsoft.WindowsServerSolutions.Administration.ObjectModel.TaskStatusHelper-Namespace (enthalten, aber im SDK für Windows Server-Lösungen nicht dokumentiert) den Status der Aufgabe ändern. Sie können beispielsweise das Häkchen von grau in grün ändern, indem Sie die SetTaskStatus-Methode mit dem TaskStatus.Complete-Enumerationswert aufrufen ("SetTaskStatus(id, TaskStatus.Complete)", wobei **id** die ID der Aufgabe ist). Die folgenden Enumerationswerte können verwendet werden: "TaskStatus.Complete", "TaskStatus.Incomplete" oder "TaskStatus.Hidden".

##### <a name="replace-tasks"></a>Ersetzen von Aufgaben
 Sie können die Aufgaben ersetzen, die in den Listen mit Aufgaben unter "Erste Schritte" und mit allgemeinen Aufgaben vordefiniert sind, indem Sie die GUID für die Aufgabe dem replaceid-Attribut in der Aufgabendefinition hinzufügen. In der folgenden Tabelle werden die Aufgaben und die entsprechenden Bezeichner aufgeführt, die im Dashboard ersetzt werden können:

|Aufgabenname|Bezeichner|
|---------------|----------------|
|Updates für weitere Microsoft-Produkte abrufen|8412D35A-13EE-4112-AE0B-F7DBC83EA83D|
|Serversicherung einrichten|F68B3F3F-19DE-499D-9ACB-4BB41B8FF420|
|Zugriff überall|8991302D-676A-4A7C-B244-D1E08AE0EFEA|
|E-Mail-Benachrichtigungen für Warnungen einrichten|DE6F2B36-F19C-4FAF-998B-9772300E3530|
|Benutzerkonten hinzufügen|6D5B5D5F-2EC7-4B1F-9580-4DB084B278B1|
|Serverordner hinzufügen|03F1F438-D94E-439B-A9F7-0C817C37D625|
|Zugriff überall - Kurze Statusinfos|6093B462-1F04-4212-8804-9BC823070FAD|
|Serversicherung - Kurze Statusinfos|156947D8-21DC-45FE-A9A8-2F80AE304191|
|Serverordner - Kurze Statusinfos|C657E8AB-AC1F-4AA1-8E80-5AF6BB27C314|
|Aktive Benutzerkonten - Kurze Statusinfos|68BCB125-CE8F-467F-B65B-56AD45A614B5|
|E-Mail-Benachrichtigungen für Warnungen - Kurze Statusinfos|75AB06E7-A679-4D62-A5EC-65362FE4F9DB|
|Computer - Kurze Statusinfos|7966A974-D52D-4F5D-B37F-05C1B73CEEF3|

##### <a name="optional-create-the-resource-file"></a>(Optional) Ressourcendatei erstellen
 Wenn Sie den Text in den Aufgaben, die Sie den Aufgaben unter "Erste Schritte", den allgemeinen Aufgaben und den Community-Links hinzufügen, lokalisieren möchten, müssen Sie eine Assembly mit der HOME-Datei und einer HOME.RESX-Datei erstellen, um die Textzeichenfolgen zu definieren.

###### <a name="to-create-the-resource-file"></a>So erstellen Sie die Ressourcendatei

1.  Klicken Sie mit der rechten Maustaste auf das für die Aufgaben erstellte Projekt, klicken Sie auf **Hinzufügen**, und klicken Sie anschließend auf **Neues Element**.

2.  Klicken Sie im Bereich **Vorlagen** auf **Ressourcendatei**, geben Sie **OEMHomePageContent.home.resx** in das Feld **Name** ein, und klicken Sie dann auf **Hinzufügen**.

    > [!NOTE]
    >  Die Ressourcendatei kann einen beliebigen Namen bekommen, er muss aber die Erweiterung HOME.RESX aufweisen.

3.  Für alle hinzugefügten Aufgaben oder Links müssen Sie der Datei "OEMHomePageContent.home.resx" Zeichenfolgen und Werte hinzufügen, die den Aufgaben- und Linkelementen entsprechen, die in der Datei "OEMHomePageContent.home" definiert sind. Im folgenden Codebeispiel wird eine Datei "Tasks.xml" veranschaulicht, die für die Ressourcendatei strukturiert ist:

    ```

    <Tasks version=?2.0? xmlns=?https://schemas.microsoft.com/WindowsServerSolutions/2010/01/Dashboard>
       <SetupMyServerTasks>
          <Task name="MyTask"
             description="MyDescription"
             id="GUID">
             <Action
             name="MyActionname"
             image="IconForAction"
             type="TaskType"
             exelocation="ActionExeLocation" />
          </Task>
       </SetupMyServerTasks>
    </Tasks>

    ```

    > [!NOTE]
    >  Bezeichner in den Attributen für die Lokalisierung dürfen keine Leerzeichen enthalten.

4.  Fügen Sie der RESX-Datei die Ressourcennamen "MyTask", "MyTaskDescription", "MyActionName" und "IconForAction" mit den entsprechenden Werten hinzu.

5.  Speichern Sie die Datei "OEMHomePageContent.home.resx", und erstellen Sie die Projektmappe.

#####  <a name="sign-the-assembly-with-an-authenticode-signature"></a><a name="BKMK_SignAssembly"></a> Signieren der Assembly mit einer Authenticode-Signatur
 Sie müssen die Assembly mit Authenticode signieren, damit sie im Betriebssystem verwendet werden kann. Weitere Informationen zum Signieren der Assembly finden Sie unter [Signieren und Überprüfen von Code mit Authenticode](https://msdn.microsoft.com/library/ms537364\(VS.85\).aspx#SignCode).

##### <a name="install-the-task-files"></a>Installieren der Aufgabendateien
 Nachdem Sie die HOME- und HOME.RESX-Dateien erstellt haben, müssen Sie sie auf dem Server installieren.

###### <a name="to-install-the-task-files"></a>So installieren Sie die Aufgabendateien

1.  Stellen Sie sicher, dass die Projektmappe ohne Fehler erstellt wird.

2.  Wenn Sie keine eingebettete Ressourcendatei erstellt haben, kopieren Sie die Datei "OEMHomePageContent.home" nach **%ProgramFiles%\Windows Server\Bin\Addins\Home** auf dem Server. Wenn Sie eine eingebettete Ressourcendatei erstellt haben, kopieren Sie die Datei "OEMHomePageContent.dll" nach **%ProgramFiles%\Windows Server\Bin\Addins\Home** auf dem Server.

## <a name="see-also"></a>Weitere Informationen
 [Erstellen und Anpassen des Images](Creating-and-Customizing-the-Image.md) [weitere Anpassungen](Additional-Customizations.md) [Vorbereiten des Abbilds für die Bereitstellung](Preparing-the-Image-for-Deployment.md) [Testen der Kundenfreundlichkeit](Testing-the-Customer-Experience.md)