---
title: Windows Server 2019-Systemanforderungen
description: Mindestanforderungen für Speicher, CPU, Netzwerk, Arbeitsspeicher und RAM bei einer Neuinstallation von Windows Server 2019.
ms.prod: windows-server-threshold
ms.technology: server-general
ms.topic: article
ms.assetid: 4a8b42d7-9fe5-4efe-9ea1-ace2131f860e
author: jasongerend
ms.author: jgerend
manager: jasgroce
ms.localizationpriority: medium
ms.openlocfilehash: 70ebf445515fd227d0f35b0c267f4fe34b2b83a9
ms.sourcegitcommit: 081661f50d6dafb77180149956a02e679270c710
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/17/2019
ms.locfileid: "71037579"
---
# <a name="system-requirements"></a>Systemanforderungen

> Gilt für: Windows Server 2019

Dieses Thema erläutert die Mindestsystemanforderungen zum Ausführen von Windows Server&reg; 2019.

## <a name="review-system-requirements"></a>Überprüfen der Systemanforderungen  

Nachfolgend sind die geschätzten Systemanforderungen für Windows Server 2019 aufgeführt. Erfüllt der Computer diese Mindestanforderungen nicht, kann das Produkt nicht ordnungsgemäß installiert werden. Die tatsächlichen Anforderungen sind von der Systemkonfiguration und den installierten Anwendungen und Features abhängig.

Sofern nicht anders angegeben gelten diese Mindestanforderungen für alle Installationsoptionen (Server Core, Server mit Desktopdarstellung und Nano Server) auf jeweils der Standard- und der Datacenter Edition.  

> [!IMPORTANT]  
> Aufgrund des beachtlichen Ausmaßes an potenziellen Bereitstellungen ist es unrealistisch, „empfohlene“ Systemanforderungen anzugeben, die allgemein gültig sind. Ziehen Sie für jede Serverrolle, die Sie bereitstellen möchten, die Dokumentation zu Rate, um weitere Informationen über die Ressourcenanforderungen bestimmter Serverrollen zu erhalten. Die besten Ergebnisse erzielen Sie, indem Sie Testbereitstellungen durchführen, um die entsprechenden Systemanforderungen für bestimme Bereitstellungsszenarien zu ermitteln.  

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
- ECC-Typ (Error Correcting Code) oder ähnliche Technologie, für physische Hostbereitstellungen

> [!IMPORTANT]  
> Wenn Sie einen virtuellen Computer, der in Bezug auf die Hardware nur die Mindestanforderungen (1 Prozessorkern und 512 MB RAM) unterstützt, erstellen und dann versuchen, diese Version auf dem virtuellen Computer zu installieren, tritt ein Fehler beim Setup auf.  
>   
> Führen Sie zur Vermeidung dieses Problems eine der folgenden Aktionen aus:  
>   
> -   Ordnen Sie dem virtuellen Computer, auf dem diese Version installiert werden soll, mehr als 800 MB RAM zu. Nach dem Setup können Sie die Zuordnung abhängig von der tatsächlichen Serverkonfiguration in 512 MB RAM ändern. Wenn Sie das Startimage (Startabbild) mit zusätzlichen Sprachen und Updates geändert haben, müssen Sie möglicherweise mehr als 800 MB RAM zuordnen, um die Installation abzuschließen.  
> -   Unterbrechen Sie den Startprozess dieser Version auf dem virtuellen Computer mit SHIFT+F10. Erstellen Sie in der geöffneten Eingabeaufforderung mithilfe von %%amp;quot;Diskpart.exe%%amp;quot; eine Installationspartition, und formatieren Sie sie. Führen Sie **Wpeutil createpagefile /path=C:\pf.sys** aus (vorausgesetzt, Sie haben die Installationspartition %%amp;quot;C:%%amp;quot; erstellt). Schließen Sie die Eingabeaufforderung, und setzen Sie das Setup fort.  

## <a name="storage-controller-and-disk-space-requirements"></a>Speichercontroller- und Speicherplatzanforderungen  
Computer mit Windows Server 2019 müssen über einen Speicheradapter verfügen, der mit der PCI Express-Architekturspezifikation konform ist. Bei beständigen Speichergeräten auf Servern, die als Festplattenlaufwerke klassifiziert sind, darf es sich nicht um PATA handeln. Bei Windows Server 2019 ist ATA/PATA/IDE/EIDE nicht für Start-, Auslagerungs- oder Datenlaufwerke zulässig.  

Nachfolgend sind die geschätzten **minimalen** Speicherplatzanforderungen für die Systempartition aufgeführt.  

**Minimum**: 32 GB  

> [!NOTE]
> Beachten Sie, dass der *absolute Mindestwert* für eine erfolgreiche Installation 32 GB beträgt. Dieser Mindestwert ermöglicht die Installation von Windows Server 2019 im Server Core-Modus mit der Serverrolle „Webdienste (IIS)“. Ein Server im Server Core-Modus ist ca. 4 GB kleiner als der gleiche Server im Modus %%amp;quot;Server mit grafischer Benutzeroberfläche%%amp;quot;. 
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

Eine Netzwerkkarte, die das Netzwerkdebugging (KDNet) unterstützt, ist sinnvoll, jedoch keine Mindestanforderung.   

Ein Netzwerkadapter, der die PXE (Pre-boot Execution Environment) unterstützt, ist sinnvoll, aber keine Mindestanforderung.

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
