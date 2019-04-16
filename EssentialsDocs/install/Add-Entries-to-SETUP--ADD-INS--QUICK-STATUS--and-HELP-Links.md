---
title: "Hinzufügen von Einträgen zu einrichten, ADD-INS, kurze STATUSINFOS und Links zu HILFETHEMEN"
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c0a8f10d-fd85-4c8d-b9bb-176cb1db1f46
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 6d3303f2c6d84932ad9d5dee8a547cd478447732
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="add-entries-to-setup-add-ins-quick-status-and-help-links"></a>Hinzufügen von Einträgen zu einrichten, ADD-INS, kurze STATUSINFOS und Links zu HILFETHEMEN

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

Können Sie Aufgaben zum Hinzufügen der **SETUP**, **ADD-INS**, **kurze STATUSINFOS** Aufgabenlisten, und Sie können im Abschnitt "Community-Links" auf der Startseite des Dashboards Links hinzu. Aufgaben und Links werden diesen Listen und dem Abschnitthinzugefügt, indem Sie eine XML-Datei mit dem Namen OEMHomePageContent.home Datei oder eine eingebettete Ressourcendatei mit dem Namen "OEMHomePageContent.dll", in %ProgramFiles%\Windows Server\Bin\Addins\Home. Die eingebettete Ressourcendatei kann verwendet werden, zum Lokalisieren von Text in den Aufgaben und Links, die Sie hinzufügen. Die Home-Datei enthält die XML-Definitionen der Aufgaben und Links.  
  
## <a name="adding-tasks-to-the-setup-add-ins-quick-status-task-lists-and-adding-links-to-help-task"></a>Hinzufügen von Aufgaben zu SETUP, ADD-INS und kurze STATUSINFOS Aufgabenlisten und Hinzufügen von Links zur Aufgabe Hilfe  
 Können Sie Aufgaben hinzufügen der **SETUP**, **ADD-INS**, **kurze STATUSINFOS** Listen sowie Links zu den **Hilfe** Aufgabe durch die Aufgaben und Links mit XML definieren optional die eingebettete Ressourcendatei erstellen und installieren die Datei auf dem Server. Wenn die XML-Datei auf dem Server ohne eine Ressourcendatei installiert wird, müssen sie OEMHomePageContent.home benannt werden. Wenn eine Assembly So installieren Sie eine XML-Datei und eine Ressourcendatei verwendet wird, muss diese den Namen OEMHomePageContent.dll und es muss mit Authenticode signiert werden.  
  
### <a name="define-the-tasks-and-links"></a>Definieren Sie die Aufgaben und links  
 Können einen Texteditor wie Editor zum Erstellen der Home-Datei, oder wenn Sie auch eine eingebettete Ressourcendatei erstellen können Sie Visual Studio2010 oder höher verwenden, definieren Sie die Dateien. Das folgende Verfahren zeigt, wie Sie Visual Studio2010 oder höher verwenden, um die Dateien zu erstellen.  
  
##### <a name="to-define-the-tasks-and-links"></a>Um die Aufgaben und Links zu definieren.  
  
1.  Öffnen Sie Visual Studio2010 oder höher als Administrator, indem das Programm im Menü "Start" und wählen Sie **als Administrator ausführen**.  
  
2.  Klicken Sie auf **Datei**, klicken Sie auf **neu**, und klicken Sie dann auf **Projekt**.  
  
3.  In der **Vorlagen** Bereich, klicken Sie auf **Klassenbibliothek**, Typ **OEMHomePageContent** in den **Namen** ein, und klicken Sie dann auf **OK**.  
  
4.  Löschen Sie die Datei Class1.cs.  
  
5.  Mit der rechten Maustaste in des neuen Projekts, klicken Sie auf **hinzufügen**, und klicken Sie dann auf **neues Element**.  
  
6.  In der **Vorlagen** Bereich, klicken Sie auf **XML-Datei**, Typ **"oemhomepagecontent.Home"** in den **Namen** ein, und klicken Sie dann auf **hinzufügen**.  
  
    > [!NOTE]
    >  Wenn die XML-Datei ohne eine Ressourcendatei installiert wird, müssen sie OEMHomePageContent.home benannt werden. Wenn sie in einer Assembly enthalten ist, kann einen beliebigen Namen zugewiesen werden, solange es die Erweiterung Home aufweist.  
  
7.  Fügen Sie den folgenden XML-Code in die Datei OEMHomePageContent.home hinzu:  
  
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
  
     Dabei gilt:  
  
    |Attribut|Beschreibung|  
    |---------------|-----------------|  
    |Name (Vorgang)|Der Name, der für die Aufgabe in der Liste angezeigt wird. Wenn Sie eine eingebettete Ressourcendatei erstellen, wird der Wert dieses Attributs Zeichenfolgenressource.|  
    |Beschreibung (Vorgang)|Die Beschreibung der Aufgabe. Wenn Sie eine eingebettete Ressourcendatei erstellen, wird der Wert dieses Attributs Zeichenfolgenressource.|  
    |ID (Vorgang)|Der Bezeichner der Aufgabe. Dieser Bezeichner muss eine GUID sein. Sie erstellen eine neue GUID für eine **Exe** Aufgabe, aber für eine **globale** Aufgabe, Sie verwenden die GUID, die Sie erstellt haben, wenn Sie die Aufgabe für den Aufgabenbereich der Unterregisterkarte definiert. Weitere Informationen zum Erstellen einer GUID finden Sie unter [GUID erstellen (guidgen.exe)](https://go.microsoft.com/fwlink/?LinkId=116098).|  
    |Bild|Dieses Feld wird ignoriert.|  
    |(Aktion)|Zeigt den Namen der Aufgabe.|  
    |Typ (Info)|Beschreibt den Typ der Aufgabe. Die Aufgabe kann eine der folgenden Optionen:- **globale** Aufgabe **Exe**, oder eine Url-Aufgabe. Ein **globale** Aufgabe ist die gleiche globale Aufgabe, die Sie beim Definieren der Aufgaben für den Aufgabenbereich der Unterregisterkarte erstellt haben. Weitere Informationen zum Erstellen einer globalen Aufgabe, die verwendet werden kann in beiden Aufgabenbereich der Unterregisterkarte und die erste Schritteund allgemeine Aufgaben Listen der Startseite finden Sie unter œCreating der Unterstützungsklassen? in œHow zu: Erstellen einer Unterregisterkarte? von der [SDK für Windows Server-Lösungen](https://go.microsoft.com/fwlink/?LinkID=248648). Ein **Exe** Task zum Ausführen von Anwendungen aus der erste Schritte-Aufgaben verwendet werden kann oder allgemeine Aufgaben aufgelistet sind.|  
    |exelocation|Der Pfad der Anwendung, die der Aufgabe zugeordnet ist. Dieses Attribut wird nur zum **Exe** Aufgaben.|  
    |replaceid|Der Bezeichner der Aufgabe, die mit dieser Aufgabe ersetzt wird.|  
    |Assembly|Der AssemblyName der Assembly die Klasse enthält, um die Abfrage des kurzen Status implementieren. Die Assembly muss sich im Programm c:\programme\ Windows Server\bin\\ befinden.|  
    |Klasse|Der Name der Klasse implementiert die Abfrage des kurzen Status. Die Klasse muss implementieren **ITaskStatusQuery** Schnittstelle.|  
    |Titel (Link)|Der Text, der für den Link angezeigt wird. Wenn Sie eine eingebettete Ressourcendatei erstellen, wird der Wert dieses Attributs Zeichenfolgenressource.|  
    |Beschreibung (Link)|Die Beschreibung des Linkziels. Wenn Sie eine eingebettete Ressourcendatei erstellen, wird der Wert dieses Attributs Zeichenfolgenressource.|  
    |ShellExecPath|Der Pfad der Anwendung oder die URL.<br /><br /> **Hinweis:** Umgebungsvariablen werden im ShellExecPath-Attribut unterstützt.|  
  
     Im folgenden Codebeispiel wird veranschaulicht, wie einen Link zu einer Anwendung zu definieren:  
  
    ```  
    <Links>  
       <Link Title="Calc" Description="Launches Calc" ShellExecPath="%windir%\system32\calc.exe" />  
    </Links>  
    ```  
  
     Im folgenden Codebeispiel wird veranschaulicht, wie einen Link zu einer Webseite zu definieren:  
  
    ```  
    <Links>  
       <Link Title="Browser" Description="Open browser" ShellExecPath="http://www.adventureworks.com/" />  
    </Links>  
    ```  
  
8.  Ändern Sie die Attributwerte, um die Aufgabe oder den Link darzustellen.  
  
9. In **Projektmappen-Explorer**, mit der rechten Maustaste **"oemhomepagecontent.Home"**, und klicken Sie dann auf **Eigenschaften**.  In der **Eigenschaften** Bereich unter **Buildvorgang**Option **eingebettete Ressource**.  
  
10. Speichern Sie die Datei OEMHomePageContent.home.  
  
 Zum Implementieren einer kurzstatusabfrage, Dokumenten und Beispielen finden Sie unter der [SDK für Windows Server-Lösungen](https://go.microsoft.com/fwlink/?LinkID=248648).  
  
#### <a name="change-the-status-of-a-setupadd-ins-task"></a>Ändern Sie den Status einer Aufgabe SETUP/ADD-INS  
 Die Aufgaben, die in SETUP und ADD-INS aufgeführten Statusangaben ausgeschaltet werden abgeschlossen (konfiguriert für Add-Ins) und nicht abgeschlossen (nicht konfiguriert für Add-Ins).  
  
 Wenn Sie die Anwendung, die der neuen Aufgabe zugeordnet ist definieren, können Sie die SetTaskStatus-Methode des Microsoft.WindowsServerSolutions.Administration.ObjectModel.TaskStatusHelper-Namespace (enthalten, aber im SDK für Windows Server-Lösungen nicht dokumentiert) den Status der Aufgabe ändern. Angenommen, Sie konnte ändern das Häkchen von Grau in Grün durch Aufrufen der SetTaskStatus-Methode, mit dem TaskStatus.Complete-Enumerationswert (SetTaskStatus (ID, TaskStatus.Complete), wobei **ID** ist der Bezeichner der Aufgabe). Enumerationswerte, die verwendet werden können, sind TaskStatus.Complete, TaskStatus.Incomplete oder "TaskStatus.Hidden".  
  
##### <a name="replace-tasks"></a>Ersetzen von Aufgaben  
 Sie können die Aufgaben ersetzen, die in der Checkliste oder die Listen der allgemeinen Aufgaben vordefiniert sind, indem Sie die GUID für die Aufgabe dem Replaceid-Attribut der Aufgabendefinition hinzufügen. Die folgende Tabelle enthält die Aufgaben und die entsprechenden Bezeichner, die im Dashboard ersetzt werden kann:  
  
|Den Namen der Aufgabe|Bezeichner|  
|---------------|----------------|  
|Abrufen von Updates für andere Microsoft-Produkte|8412D35A-13EE-4112-AE0B-F7DBC83EA83D|  
|Richten Sie Server-Sicherung|F68B3F3F-19DE-499D-9ACB-4BB41B8FF420|  
|Einrichten von "Zugriff überall"|8991302D-676A-4A7C-B244-D1E08AE0EFEA|  
|Einrichten von E-Mail-Benachrichtigung|DE6F2B36-F19C-4FAF-998B-9772300E3530|  
|Hinzufügen von Benutzerkonten|6D5B5D5F-2EC7-4B1F-9580-4DB084B278B1|  
|Serverordner hinzufügen|03F1F438-D94E-439B-A9F7-0C817C37D625|  
|Zugriff überall - kurze Statusinfos|6093B462-1F04-4212-8804-9BC823070FAD|  
|Serversicherung - kurze Statusinfos|156947D8-21DC-45FE-A9A8-2F80AE304191|  
|Serverordner - kurze Statusinfos|C657E8AB-AC1F-4AA1-8E80-5AF6BB27C314|  
|Aktive Benutzerkonten - kurze Statusinfos|68BCB125-CE8F-467F-B65B-56AD45A614B5|  
|E-Mail-Benachrichtigungen für Warnungen - kurze Statusinfos|75AB06E7-A679-4D62-A5EC-65362FE4F9DB|  
|Computer - kurze Statusinfos|7966A974-D52D-4F5D-B37F-05C1B73CEEF3|  
  
##### <a name="optional-create-the-resource-file"></a>(Optional) Die Ressourcendatei erstellen  
 Wenn Sie den Text in den Aufgaben, die Sie Checkliste, Aufgaben und Community-Links hinzufügen, lokalisieren möchten müssen Sie eine Assembly, die die Home-Datei erstellen und eine. Home.resx-Datei, die die Textzeichenfolgen definiert.  
  
###### <a name="to-create-the-resource-file"></a>Die Ressourcendatei erstellen  
  
1.  Mit der rechten Maustaste in des Projekts, das Sie für Ihre Aufgaben erstellt haben, klicken Sie auf **hinzufügen**, und klicken Sie dann auf **neues Element**.  
  
2.  In der **Vorlagen** Bereich, klicken Sie auf **Ressourcendatei**, Typ **OEMHomePageContent.home.resx** in den **Namen** ein, und klicken Sie dann auf **hinzufügen**.  
  
    > [!NOTE]
    >  Die Ressourcendatei kann beliebiger Name zugewiesen, solange es verfügt über eine. die Erweiterung Home.resx.  
  
3.  Für jeden Vorgang oder die Verknüpfung, die Sie hinzufügen, müssen Sie Zeichenfolgen und Werte hinzufügen, auf die OEMHomePageContent.home.resx-Datei, die den Aufgaben- und linkelementen entsprechen, die in der Datei OEMHomePageContent.home definiert sind. Das folgende Codebeispiel zeigt ein Beispiel für eine Tasks.xml-Datei, die strukturiert ist für die Ressourcendatei:  
  
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
    >  Bezeichner in den Attributen, die für die Lokalisierung verwendet werden darf keine Leerzeichen enthalten.  
  
4.  Fügen Sie die Ressourcennamen "MyTask", "MyTaskDescription", "MyActionName, und" iconforaction "auf die RESX-Datei mit den entsprechenden Werten hinzu.  
  
5.  Speichern Sie die Datei OEMHomePageContent.home.resx, und erstellen Sie die Projektmappe.  
  
#####  <a name="BKMK_SignAssembly"></a>Signieren der Assembly mit Authenticode-Signatur  
 Sie müssen mit Authenticode Signieren der Assembly für sie in das Betriebssystem verwendet werden. Weitere Informationen zum Signieren der Assembly finden Sie unter [signieren und Überprüfen von Code mit Authenticode](https://msdn.microsoft.com/library/ms537364\(VS.85\).aspx#SignCode).  
  
##### <a name="install-the-task-files"></a>Installieren der Aufgabendateien  
 Nach dem Erstellen der Home und. Home.resx-Dateien, Sie müssen diese auf dem Server installieren.  
  
###### <a name="to-install-the-task-files"></a>So installieren Sie die Aufgabendateien  
  
1.  Stellen Sie sicher, dass die Projektmappe ohne Fehler erstellt.  
  
2.  Wenn Sie keine eingebettete Ressourcendatei erstellt haben, kopieren Sie die Datei OEMHomePageContent.home **%ProgramFiles%\Windows Server\Bin\Addins\Home** auf dem Server. Wenn Sie eine eingebettete Ressourcendatei erstellt haben, kopieren Sie die Datei OEMHomePageContent.dll **%ProgramFiles%\Windows Server\Bin\Addins\Home** auf dem Server.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen und Anpassen des Abbilds](Creating-and-Customizing-the-Image.md)   
 [Weitere Anpassungen](Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](Testing-the-Customer-Experience.md)