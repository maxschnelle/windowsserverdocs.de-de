---
title: Systemanforderungen
description: Welche Mindestanforderungen gelten für Speicher, CPU, Netzwerk, Arbeitsspeicher und RAM bei einer Neuinstallation jeder Installationsoption?
ms.prod: windows-server
ms.date: 10/17/2017
ms.technology: server-general
ms.topic: article
ms.assetid: 4a8b42d7-9fe5-4efe-9ea1-ace2131fe068
author: jaimeo
ms.author: jaimeo
manager: dongill
ms.localizationpriority: medium
ms.openlocfilehash: cd4666f9ac0677ce8893041ae4e937cca41e8164
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2020
ms.locfileid: "80826493"
---
# <a name="system-requirements"></a>Systemanforderungen

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016 

Dieses Thema behandelt die Mindestsystemanforderungen zum Ausführen von Windows Server&reg; 2016 oder Windows Server, Version 1709.

> [!NOTE]  
> Bei diesem Release wird eine Neuinstallation empfohlen.  

> [!NOTE]  
> Wenn Sie bei der Installation die Server Core-Option wählen, sollten Sie berücksichtigen, dass keinerlei GUI-Komponenten installiert werden und diese nicht mit dem Server-Manager installiert oder deinstalliert werden können. Wenn Sie GUI-Features benötigen, müssen Sie bei der Installation von Windows Server 2016 die Option „Server mit Desktopdarstellung“ wählen. Weitere Informationen finden Sie unter [Installieren von Nano Server](Getting-Started-with-Nano-Server.md)  


## <a name="review-system-requirements"></a>Überprüfen der Systemanforderungen  
Nachfolgend sind die geschätzten Systemanforderungen für Windows Server 2016 aufgeführt. Wenn der Computer die Mindestanforderungen nicht erfüllt, kann das Produkt nicht ordnungsgemäß installiert werden. Die tatsächlichen Anforderungen sind von der Systemkonfiguration und den installierten Anwendungen und Features abhängig.

Sofern nicht anders angegeben gelten diese Mindestanforderungen für alle Installationsoptionen (Server Core, Server mit Desktopdarstellung und Nano Server) auf jeweils der Standard- und der Datacenter Edition.  

> [!IMPORTANT]  
> Aufgrund des beachtlichen Ausmaßes an potenziellen Bereitstellungen ist es unrealistisch, empfohlene Systemanforderungen anzugeben, die allgemein gültig sind. Ziehen Sie für jede Serverrolle, die Sie bereitstellen möchten, die Dokumentation zu Rate, um weitere Informationen über die Ressourcenanforderungen bestimmter Serverrollen zu erhalten. Die besten Ergebnisse erzielen Sie, indem Sie Testbereitstellungen durchführen, um die entsprechenden Systemanforderungen für bestimme Bereitstellungsszenarien zu ermitteln.  


## <a name="processor"></a>Prozessor  
Die Prozessorleistung ist nicht nur von der Taktfrequenz des Prozessors abhängig, sondern auch von der Anzahl der Prozessorkerne und der Größe des Prozessorcache. Nachfolgend sind die Prozessoranforderungen für dieses Produkt aufgeführt:  

**Minimum**:  
- 1,4-GHz-Prozessor mit 64 Bit  
- Kompatibel mit x64-Anweisungsset  
- Unterstützt NX und DEP  
- Unterstützt CMPXCHG16b, LAHF/SAHF und PrefetchW  
- Unterstützt SLAT (Second-Level Address Translation) (EPT oder NPT)  

[Coreinfo](https://technet.microsoft.com/sysinternals/cc835722.aspx) ist ein Tool, mit dem du überprüfen kannst, über welche dieser Funktionen die CPU verfügt.

## <a name="ram"></a>RAM  
Nachfolgend sind die geschätzten RAM-Anforderungen für dieses Produkt aufgeführt:  

**Minimum**:  
- 512 MB (2 GB für Server mit der Installationsoption „Desktopdarstellung“)
- ECC-Typ (Error Correcting Code) oder ähnliche Technologie  

> [!IMPORTANT]  
> Wenn Sie einen virtuellen Computer, der in Bezug auf die Hardware nur die Mindestanforderungen (1 Prozessorkern und 512 MB RAM) unterstützt, erstellen und dann versuchen, diese Version auf dem virtuellen Computer zu installieren, tritt ein Fehler beim Setup auf.  
>   
> Führen Sie zur Vermeidung dieses Problems eine der folgenden Aktionen aus:  
>   
> -   Ordnen Sie dem virtuellen Computer, auf dem diese Version installiert werden soll, mehr als 800 MB RAM zu. Nach dem Setup können Sie die Zuordnung abhängig von der tatsächlichen Serverkonfiguration in 512 MB RAM ändern.  
> -   Unterbrechen Sie den Startprozess dieser Version auf dem virtuellen Computer mit UMSCHALTTASTE+F10. Erstellen Sie in der geöffneten Eingabeaufforderung mithilfe von %%amp;quot;Diskpart.exe%%amp;quot; eine Installationspartition, und formatieren Sie sie. Führen Sie **Wpeutil createpagefile /path=C:\pf.sys** aus (vorausgesetzt, Sie haben die Installationspartition %%amp;quot;C:%%amp;quot; erstellt). Schließen Sie die Eingabeaufforderung, und setzen Sie das Setup fort.  

## <a name="storage-controller-and-disk-space-requirements"></a>Speichercontroller- und Speicherplatzanforderungen  
Computer mit Windows Server 2016 müssen über einen Speicheradapter verfügen, der mit der PCI Express-Architekturspezifikation konform ist. Bei beständigen Speichergeräten auf Servern, die als Festplattenlaufwerke klassifiziert sind, darf es sich nicht um PATA handeln. Bei Windows Server 2016 ist ATA/PATA/IDE/EIDE nicht für Start-, Auslagerungs- oder Datenlaufwerke zulässig.  

Nachfolgend sind die geschätzten **minimalen** Speicherplatzanforderungen für die Systempartition aufgeführt.  

**Minimum**: 32 GB  

> [!NOTE]
> Beachten Sie, dass der *absolute Mindestwert* für eine erfolgreiche Installation 32 GB beträgt. Dieser Mindestwert ermöglicht Ihnen die Installation von Windows Server 2016 im Server Core-Modus mit der Serverrolle für Webdienste (IIS). Ein Server im Server Core-Modus ist ca. 4 GB kleiner als der gleiche Server im Modus %%amp;quot;Server mit grafischer Benutzeroberfläche%%amp;quot;. 
> 
> In den folgenden Fällen ist zusätzlicher Speicherplatz für die Systempartition erforderlich:  
> 
> -   Wenn Sie das System über ein Netzwerk installieren.  
> -   Computer mit mehr als 16 GB RAM erfordern einen größeren Speicherplatz für Auslagerungen, Ruhezustand und Sicherungsdateien.  

## <a name="network-adapter-requirements"></a>Netzwerkkartenanforderungen  

Netzwerkkarten, die mit diesem Release verwendet werden, sollten folgende Features umfassen:  

**Minimum**:  
- Ein Ethernet-Adapter mit einem Mindestdurchsatz im Gigabit-Bereich  
- Konformität mit der PCI Express-Architekturspezifikation  
- Unterstützung für PXE (Pre-Boot eXecution Environment)  

Eine Netzwerkkarte, die das Netzwerkdebugging (KDNet) unterstützt, ist sinnvoll, jedoch keine Mindestanforderung.   

## <a name="other-requirements"></a>Sonstige Anforderungen  
Computer, auf denen dieses Release ausgeführt wird, müssen außerdem über folgende Elemente verfügen:  


-   DVD-Laufwerk (wenn Sie das Betriebssystem über DVD-Medien installieren möchten)  

Die folgenden Elemente sind nicht unbedingt erforderlich, werden jedoch für bestimme Features benötigt:  

- UEFI 2.3.1c-basiertes System und Firmware mit Unterstützung eines sicheren Starts  
- Trusted Platform Module  

-   Grafikgerät und Monitor mit Unterstützung für Super-VGA (1024 x 768) oder eine höhere Auflösung  

-   Tastatur und Microsoft&reg;-Maus (oder anderes kompatibles Zeigegerät)  

-   Internetzugang (möglicherweise kostenpflichtig)  

> [!NOTE]  
> Ein TPM-Chip (Trusted Platform Module) ist nicht unbedingt für die Installation dieses Release erforderlich. Für die Verwendung bestimmter Features wie z.B. der BitLocker-Laufwerkverschlüsselung wird jedoch ein solcher Chip benötigt. Wenn Ihr Computer TPM verwendet, müssen die folgenden Anforderungen erfüllt sein:  
>  
> - Bei hardwarebasierten TPMs muss Version 2.0 der TPM-Spezifikation implementiert sein.  
> - TPMs, die Version 2.0 implementieren, müssen über ein EK-Zertifikat verfügen, das entweder vorab vom Hardwarehersteller für das TPM bereitgestellt wird, oder beim ersten Start vom Gerät abgerufen werden kann.  
> - TPMs, die Version 2.0 implementieren, müssen über SHA-256 PCR-Bänke verfügen und PCRs 0 bis 23 für SHA-256 implementieren. Es ist akzeptabel, TPMs mit einer einzigen wechselbaren PCR-Bank auszuliefern, die sowohl für SHA-1 als auch für SHA-256 verwendet werden kann.  
> - Eine UEFI-Option zum Deaktivieren des TPMs ist nicht erforderlich.  

## <a name="installation-of-nano-server"></a>Installation von Nano Server  
Detaillierte Schritte zum Installieren von Windows Server 2016 als Nano Server-Version finden Sie unter [Installieren von Nano Server](Getting-Started-with-Nano-Server.md).

## <a name="additional-resources"></a>Weitere Ressourcen
- [Windows-Prozessoranforderungen](https://docs.microsoft.com/windows-hardware/design/minimum/windows-processor-requirements)
- [Vergleich der Standard- und Datacenter-Editionen von Windows Server 2016](https://docs.microsoft.com/windows-server/get-started/2016-edition-comparison)
- [Windows 10-Systemanforderungen](https://www.microsoft.com/windows/windows-10-specifications#system-specifications)
- [Herunterladen des Windows Server 2016 Lizenzierungsdatenblatts](https://download.microsoft.com/download/7/2/9/7290EA05-DC56-4BED-9400-138C5701F174/WS2016LicensingDatasheet.pdf)
