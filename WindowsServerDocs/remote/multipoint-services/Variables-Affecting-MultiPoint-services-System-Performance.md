---
title: Variablen mit Auswirkung auf die Leistung von MultiPoint Services-Systemen
description: Leistungsinformationen für MultiPoint Services
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0f3e8875-1b5e-4789-b16c-d06d6e31f38e
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: 7a06fcc763283114dc12ad106aa7ec146502dbd9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59867581"
---
# <a name="variables-affecting-multipoint-services-system-performance"></a>Variablen mit Auswirkung auf die Leistung von MultiPoint Services-Systemen
Es gibt viele Variablen, die die allgemeine Leistung Ihres MultiPoint Services-Systems beeinträchtigen können. Sie sollten dies berücksichtigen beim Entwerfen Ihres Systems.  
  
## <a name="usage"></a>Verwendung  
  
-   **Anwendungen** Art und Anzahl von Anwendungen, die zur gleichen Zeit, besonders grafische ausgeführt\-mit hohem schreibaufkommen oder Arbeitsspeicher-intensive Anwendungen wirken sich die gesamtleistung des Systems. Weitere Informationen finden Sie unter [Anwendungen und Internet Content](hardware-and-performance-recommendations.md#applications-and-internet-content).  
  
-   **Nutzung des Internets** überlegen, ob Ihre Benutzer angezeigt werden, multimedia-Inhalte oder Webseiten, Full Motion-Videos zu verwenden. Diese Art von Inhalt kann im System überladen werden, wenn zu viele Benutzer gleichzeitig anzeigen.  
  
    > [!NOTE]  
    > Die Projektion-Funktion in MultiPoint Services dadurch Lehrer, um ihren Bildschirmen in Monitore für Schüler und Studenten zu projizieren, dient nicht zum projizieren von Full Motion-Videos. Die Projektion-Funktion dient zur Veranschaulichung, wie z. B. eine Prozedur angezeigt.  
  
-   **Schnelle Geräte** Wenn zu viele Benutzer gleichzeitig ein Gerät mit hoher Geschwindigkeit wie z. B. eine Webkamera oder DVD-Player verwenden, sind dies die gesamtleistung des Systems auswirkt.  
  
## <a name="configuration"></a>Konfiguration  
  
-   **CPU, RAM und GPU** finden Sie unter [Leistung des MultiPoint Services-System optimieren](hardware-and-performance-recommendations.md#optimize-multipoint-services-system-performance) in diesem Handbuch für CPU, RAM und GPU-Empfehlungen.  
-   **Die Netzwerkbandbreite** für RDP-Over-LAN verbundene Stationen, die Netzwerkbandbreite und die Möglichkeit, den Client (z. B. eine thin Client, desktop-PC oder Laptop) ist wichtig, insbesondere, wenn Sie Videos in der Sitzung des Benutzers ausgeführt wird. Wenn Sie USB-Over-Ethernet-0 (null)-Clients verwenden, sollte die Netzwerkbandbreite auch berücksichtigt. Videodaten für alle Geräte werden über die gleichen Ethernet-Verbindung gesendet werden, daher Sie sollten zum Einrichten einer separaten Gigabit-Ethernet-Netzwerk zu berücksichtigen, wenn Sie diese Geräte verwenden.  
-   **RemoteFX** für RDP-Over-LAN verbundene Stationen, möglicherweise RemoteFX verwenden, um die Übermittlung von High Definition-Multimediainhalten erheblich zu verbessern.  
-   **Bildschirmauflösung** , wenn Sie Vollbild-video Auslastung haben, möchten Sie möglicherweise reduzieren Sie die Auflösung des Bildschirms auf die Leistung zu maximieren.  
-   **Anzahl von Clients, USB-0 (null)** die Gesamtanzahl der USB-0 (null)-Clients auf einem einzelnen Stamm-Hub auf dem Server wirkt sich direkt auf die video-Leistung. Weitere Informationen finden Sie unter [Layout für USB-0 (null) Client verbundene Stationen](MultiPoint-services-Site-Planning.md#layout-for-usb-zero-client-connected-stations). Die Anzahl der USB-Over-Ethernet-0 (null)-Client-Stationen, die unterstützt werden möglicherweise etwas kleiner als die Anzahl der Clients der USB-0 (null).  
-   **USB-Bandbreite** sollten Sie die USB-Bandbreite, wenn Sie Ihr System entwerfen.  Dies ist besonders wichtig für USB-0 (null)-Clients, die video-Daten über die USB-Verbindung senden. Minimieren Sie die Anzahl der Geräte, die mit einem einzelnen USB-Anschluss auf dem Server verbunden sind, um Bandbreite zu optimieren. Dies gilt für kaskadierenden Stationen und zwischen Hubs. Weitere Informationen finden Sie unter [Station Hubs](MultiPoint-services-Site-Planning.md#station-hubs) und [Hubs für fortgeschrittene](MultiPoint-services-Site-Planning.md#intermediate-hubs).  
  
-   **USB-Typ** mithilfe von USB-3.0 statt USB 2.0 wird die verfügbare Bandbreite zwischen dem Server und die zwischengeschalteter Hub erhöht, wenn Sie mehr als drei USB-0 (null)-Clients mit dem Hub herstellen, oder bei Verwendung von hoher Bandbreite USB-Geräte.  
  
-   **Stationen** die Gesamtzahl der Stationen wirkt sich auf die Leistung. Wenn Sie hohe Grafik, Verarbeitung oder video-Anforderungen verfügen, empfiehlt es sich um die Anzahl der Stationen zu beschränken. Weitere Informationen finden Sie unter [MultiPoint Services-Systems optimieren der Leistung](hardware-and-performance-recommendations.md#optimize-multipoint-services-system-performance).