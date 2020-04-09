---
title: Verwalten von virtuellen Desktops
description: Erfahren Sie, wie Sie virtuelle Desktops (VDI) in Multipoint Services verwalten.
ms.prod: windows-server
ms.technology: multipoint-services
ms.topic: article
ms.assetid: fa9ac0ed-47cb-4811-91ff-4fcb62d7858b
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 08/04/2016
ms.openlocfilehash: 114fde42ca36f9451680066056251bafbe944e56
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80853463"
---
# <a name="manage-virtual-desktops"></a>Verwalten von virtuellen Desktops
Mit einem VDI-Computer können Sie jede *lokale* Multipoint Services-Station so konfigurieren, dass eine Verbindung mit einem Windows 10 Enterprise-Gast Betriebssystem hergestellt wird, das auf einem virtuellen Hyper-V-Computer auf demselben Multipoint Services-Computer wie die Station ausgeführt wird. Diese Stationen für virtuelle Desktops können mit einer Anwendung angepasst werden, die nicht auf einer Windows Server-Version installiert werden kann.  
  
## <a name="enable-the-virtual-desktop-feature"></a>Aktivieren des virtuellen Desktop Features  
  
1.  Öffnen Sie MultiPoint-Manager, und klicken Sie anschließend auf die Registerkarte **Virtuelle Desktops**.  
  
2.  Klicken Sie unter **VDI-Aufgaben** auf **Create virtual desktop** (Virtuellen Desktop erstellen), und rufen Sie Ihre ISO- oder VHD-Datei von Windows 10 Enterprise auf.  
  
Das System wird neu gestartet, dies kann einige Minuten dauern.  
  
## <a name="create-a-virtual-desktop-template"></a>Erstellen einer Vorlage für virtuelle Desktops  
  
1.  Öffnen Sie MultiPoint-Manager, und klicken Sie anschließend auf die Registerkarte **Virtuelle Desktops**.  
  
2.  Klicken Sie unter **VDI Tasks** (VDI-Aufgaben) auf **Create virtual desktop** (Virtuellen Desktop erstellen), und rufen Sie Ihre ISO- oder VHD-Datei von Windows 10 Enterprise auf.  
  
    Wenn Sie die DVD verwenden, sucht das Programm automatisch die WIM-Datei von Windows 10 Enterprise. Klicken Sie andernfalls auf **Durchsuchen**, und navigieren Sie dann zur ISO- bzw. VHD-Datei von Windows 10 Enterprise.  
  
    Ändern Sie das Präfix bei Bedarf. Standardmäßig ist es der Name des Hostcomputers.  
  
    > [!NOTE]  
    > Das Präfix wird als Name der Vorlage und der virtuellen Desktopstationen verwendet. Die Vorlage erhält den Namen „Präfix“ \-t. Die virtuellen Desktopstationen erhalten den Namen „Präfix“ \-*n*, wobei *n* die Stations-ID ist.  
  
4.  Geben Sie einen Namen und ein Kennwort für das lokale Administratorkonto ein, das zum Anmelden bei allen virtuellen Desktopstationen verwendet wird, die auf Grundlage der Vorlage erstellt werden, und klicken Sie dann auf **OK**.  
  
    Es dauert einige Minuten, bis die Erstellung der Vorlage abgeschlossen ist.  
      
    Als Nächstes erfahren Sie, wie Sie die Vorlage für virtuelle Desktops anpassen.  
      
    > [!NOTE]  
    > Wenn der MultiPoint-Server in eine Domäne eingebunden ist, füllt das Dialogfeld ein zusätzliches Feld. Dadurch können Sie bestimmen, ob die von der Vorlage erstellten virtuellen Computer in eine Domäne eingebunden werden sollen.   
  
## <a name="import-a-virtual-desktop-template"></a>Importieren einer Vorlage für virtuelle Desktops  
Falls Sie eine Vorlage für virtuelle Desktops auf einem anderen MultiPoint-Server erstellt haben, können Sie diese Vorlage mithilfe der folgenden Schritte importieren.  

1.    Öffnen Sie MultiPoint-Manager, und klicken Sie anschließend auf die Registerkarte **Virtuelle Desktops**.  
  
2.    Klicken Sie unter VDI-Tasks (VDI-Aufgaben) auf **Import Virtual desktop template** (Vorlage für virtuelle Desktops importieren).  
  
3.    Suchen Sie die Vorlage und definieren Sie den Pfad und das Präfix für die importierte Vorlage.  
  
## <a name="customize-the-virtual-desktop-template"></a>Anpassen der Vorlage für virtuelle Desktops  
Nachdem Sie die Vorlage für virtuelle Desktops erstellt haben, können Sie sie mit Anwendungen und Softwareupdates anpassen und Systemeinstellungen konfigurieren.   

1. Öffnen Sie MultiPoint-Manager, und klicken Sie anschließend auf die Registerkarte **Virtuelle Desktops**.  
2. Wählen Sie die Vorlage für virtuelle Desktops aus, und klicken Sie anschließend auf **Customize virtual desktop template** (Vorlage für virtuelle Desktops anpassen).  
Die Vorlage wird in einem separaten Fenster geöffnet, und es werden zusätzliche Anweisungen dargestellt, die die wichtigsten Schritte zum Anpassen der Vorlage für virtuelle Desktops hervorheben. Lesen Sie diese Anweisungen sorgfältig.  
  
## <a name="create-virtual-desktop-stations"></a>Erstellen virtueller Desktop Stationen  
  
1.  Öffnen Sie den MultiPoint-Manager im Stationsmodus, und klicken Sie anschließend auf die Registerkarte **Virtuelle Desktops**.  
  
    > [!NOTE]  
    > Wenn das MultiPoint Services-System nicht im Stationsmodus ausgeführt wird, starten Sie es neu, bevor Sie diese Prozedur abschließen.  
  
2.  Wählen Sie im linken\-Bereich die Vorlage für virtuelle Desktops aus. Sie trägt den Namen <Präfix –t>.  
  
3.  Klicken Sie unter Vorlagenaufgaben auf **Virtuelle Desktopstationen erstellen**, und klicken Sie anschließend auf **OK**.  
  
    Die Erstellung der virtuellen Desktopstation kann einige Minuten dauern.  
  
    > [!NOTE]  
    > Wenn lokale Stationen gegenwärtig mit einem sitzungsbasierten virtuellen Desktop verbunden sind, müssen Sie diese Stationen abmelden, damit sie eine Verbindung mit einer der neu erstellten virtuellen Desktopstationen herstellen können.  
  
### <a name="validate-the-newly-created-customized-virtual-station-desktops"></a>Überprüfen der neu erstellten angepassten virtuellen Desktopstationen  
  
Sie können Ihre benutzerdefinierten virtuellen Desktopstationen überprüfen, indem Sie sich mit einem lokalen Administratorkonto oder einem Domänenkonto bei mindestens einer virtuellen Desktopstation anmelden und anschließend sicherstellen, dass die neuen VM\-basierten virtuellen Desktops ordnungsgemäß funktionieren.  
  
## <a name="disable-virtual-desktops"></a>Deaktivieren von virtuellen Desktops  
  
Wenn Sie virtuelle Desktops deaktivieren, wird auch die Hyper-V-Funktion deaktiviert. Alle Benutzer werden abgemeldet, und das System wird neu gestartet. Alle virtuellen Stationen werden nach dem Neustart des Systems lokalen MultiPoint-Sitzungen zugewiesen.  

1. Öffnen Sie den MultiPoint-Manager im Stationsmodus, und klicken Sie anschließend auf die Registerkarte **Virtuelle Desktops**.  
  
2. Klicken Sie unter VDI-Tasks (VDI-Aufgaben) auf **Disable virtual desktops** (Virtuelle Desktops deaktivieren). 