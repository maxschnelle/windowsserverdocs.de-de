---
title: Grundlegendes (fehlende) Sperren von verteilten Dateien in DFSR
description: In diesem Artikel wird das Fehlen eines verteilungssperrmechanismus für mehrere Hosts in Windows und insbesondere in Ordnern erläutert, die von DFSR repliziert wurden.
ms.prod: windows-server
ms.technology: server-general
ms.date: 06/10/2020
author: Deland-Han
ms.author: delhan
ms.openlocfilehash: 739bcd1127877d4c9b1339b64270262d9d48634f
ms.sourcegitcommit: fa9a8badf4eb366aeeca7d2905e2cad711ee8dae
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/11/2020
ms.locfileid: "84714974"
---
# <a name="understanding-the-lack-of-distributed-file-locking-in-dfsr"></a>Grundlegendes (fehlende) Sperren von verteilten Dateien in DFSR

In diesem Artikel wird das Fehlen eines verteilungssperrmechanismus für mehrere Hosts in Windows und insbesondere in Ordnern erläutert, die von DFSR repliziert wurden.
  
## <a name="some-background"></a>Hintergrund

  - Sperren verteilter Dateien – bezieht sich auf das Konzept der Verwendung mehrerer Kopien einer Datei auf mehreren Computern, und wenn eine Datei zum Schreiben geöffnet wird, werden alle anderen Kopien gesperrt. Dadurch wird verhindert, dass eine Datei auf mehreren Servern gleichzeitig von mehreren Benutzern geändert wird.
  - Verteiltes Dateisystem Replikation – [DFSR](/previous-versions/windows/desktop/dfsr/distributed-file-system-replication--dfsr-) arbeitet in einem Zustands basierten Entwurf mit mehreren Mastern. Bei der Zustands basierten Replikation wendet jeder Server im multimastersystem Updates auf das zugehörige Replikat an, ohne Protokolldateien auszutauschen (Stattdessen werden Versions Vektoren verwendet, um "Aktualitäts Informationen" beizubehalten). Nach der anfänglichen Synchronisierung ist kein Server mehr beliebig autorisierend, daher ist er für verschiedene Netzwerktopologien hoch verfügbar und sehr flexibel.
  - Server Message Block: [SMB](/openspecs/windows_protocols/ms-smb/f210069c-7086-4dc2-885e-861d837df688) ist das gängige Protokoll, das in Windows für den Zugriff auf Dateien über das Netzwerk verwendet wird. Vereinfacht ausgedrückt, ist es ein Client/Server-Protokoll, das einen Redirector verwendet, damit Remote Dateisysteme als lokale Dateisysteme angezeigt werden. Er ist nicht spezifisch für Windows und ist recht häufig – ein bekanntes nicht-Microsoft-Beispiel ist Samba, mit dem Linux, Mac und andere Betriebssysteme als SMB-Clients/-Server fungieren und an Windows-Netzwerken teilnehmen können.

  
Es ist wichtig, dass Sie eine klare Abgrenzung definieren, wo DFSR und SMB in ihrer replizierten Daten Umgebung leben. SMB ermöglicht Benutzern den Zugriff auf Ihre Dateien, und Sie hat keine Kenntnis von DFSR. Ebenso hält DFSR (über das RPC-Protokoll) Dateien zwischen Servern synchron und hat keinerlei Kenntnis von SMB. Verwechseln Sie die verteilte Sperre nicht, wie Sie in diesem Beitrag definiert ist, und die [opportunistische Sperre](/windows/win32/fileio/opportunistic-locks)  
  
An dieser Stelle können die Dinge wie die Brits in Birnen geformt werden.  
  
Da Benutzerdaten auf mehreren Servern ändern können, und da jeder Windows-Server nur über eine Datei Sperre auf sich selbst weiß, *und* da [DFSR nichts über diese Sperren auf anderen Servern weiß](/previous-versions/windows/it-pro/windows-server-2003/cc773238(v=ws.10)), ist es für Benutzer möglich, die Änderungen gegenseitig zu überschreiben. DFSR verwendet einen "Last Writer WINS"-Konflikt Algorithmus, sodass jemand verlieren muss und die Person, die zuletzt gespeichert werden muss, Ihre Änderungen behält. Der Verlust der Dateikopie wird in den Ordner *ConflictandDeleted* eingecheckt.  
  
Dies ist weitaus *weniger* häufig als Benutzer, die glauben. Normalerweise werden echte freigegebene Dateien in einer lokalen Umgebung geändert. in der Zweigstelle oder in derselben Zeile von kubischen. Sie werden in der Regel von Mitarbeitern desselben Teams bearbeitet, sodass die Benutzer im allgemeinen wissen, dass Sie Daten ändern. Da Sie sich in der Regel am gleichen Standort befinden, sind die Chancen deutlich höher, dass alle Benutzer, die an einem freigegebenen Dokument arbeiten, denselben Server verwenden. Die Situation wird von Windows SMB behandelt. Wenn ein Benutzer eine Datei für Änderungen gesperrt hat und er versucht, die Datei zu bearbeiten, erhält der andere Benutzer eine Fehlermeldung wie die folgende:  
  
![Datei wird verwendet](./media/understanding-the-lack-of-distributed-file-locking-in-dfsr/1.jpg)
  
Wenn die Anwendung, die die Datei öffnet, sehr clever ist, wie z. b. Word 2007, erhalten Sie möglicherweise Folgendes:  
  
![Datei wird verwendet](./media/understanding-the-lack-of-distributed-file-locking-in-dfsr/2.jpg) 
  
DFSR verfügt über einen Mechanismus für gesperrte Dateien, befindet sich jedoch nur im Kontext des Servers. DFSR repliziert eine Datei nicht in oder, wenn die lokale Kopie eine exklusive Sperre aufweist. Dadurch wird jedoch nicht verhindert, dass jemand auf einem anderen Server die Datei ändert.  
  
Zurück zum Thema ist das Problem, dass freigegebene Daten geografisch geändert werden, und für einige Leute *ist es ziemlich* leicht. Wir werden gelegentlich gefragt, warum DFSR diese Sperre nicht behandelt und alles mit einer Welle der magischen Wand übernimmt. Es stellt sich heraus, dass dies ein interessantes und schwieriges Szenario ist, das für ein multimasterreplikations System gelöst werden muss. Sehen wir uns dies einmal genauer an.  
  
## <a name="third-party-solutions"></a>Lösungen von Drittanbietern
  
Es gibt einige Anbieter Lösungen, bei denen dieses Problem auftritt, das Sie in der Regel durch eine oder mehrere der folgenden Methoden lösen \* :  

  - Verwendung eines Broker Mechanismus

> Eine zentrale "Verkehrs-Cop" ermöglicht einem Server, alle anderen Server und die von Benutzern gesperrten Dateien zu kennen. Dies bedeutet leider auch, dass es häufig einen Single Point of Failure im verteilten Sperrsystem gibt.

![Topologie](./media/understanding-the-lack-of-distributed-file-locking-in-dfsr/3.png) 

  - Anforderung für ein vollständig geroutetes Netzwerk

> Da ein zentraler Broker in der Lage sein muss, mit allen Servern zu kommunizieren, die an der Datei Replikation teilnehmen, ist dadurch die Möglichkeit, komplexe Netzwerktopologien zu verarbeiten. Ringtopologien und Multihub-und-geclustertopologien sind in der Regel nicht möglich. In einem nicht vollständig gerouteten Netzwerk sind einige Server möglicherweise nicht in der Lage, sich gegenseitig oder einen Broker direkt zu kontaktieren, und können nur mit einem Partner sprechen, der selbst mit einem anderen Server kommunizieren kann – usw. Dies ist in einer Umgebung mit mehreren Mastern, aber nicht mit einem Broker Mechanismus gut.

![Topologie](./media/understanding-the-lack-of-distributed-file-locking-in-dfsr/4.png)

  - Sind auf ein paar von Servern beschränkt

> Einige Lösungen schränken die Topologie auf ein Server Paar ein, um ihren verteilten Sperrmechanismus zu vereinfachen. Bei größeren Umgebungen ist dies möglicherweise nicht möglich.

  - Verwenden von Agents auf Clients und Servern
  - Verwenden Sie die Multimasterreplikation nicht.
  - Verwenden Sie MS Clustering nicht.
  - Verwenden von speziellen Geräten

  
***\*** Beachten Sie, dass ich in der Regel \! keine Bedrohungs Bedrohungen bereitstelle, weil eine Lösung vorhanden ist, die mindestens eine dieser Methoden nicht implementiert.\!*  
  
## <a name="deeper-thoughts"></a>Tiefere Gedanken  
  
Wenn Sie mehr über dieses Problem nachzudenken, beginnen einige grundlegende Probleme. Wenn z. b. vier Server mit Daten vorhanden sind, die von Benutzern an vier Standorten geändert werden können, und die WAN-Verbindung zu einem der Anwendungen offline geschaltet wird, was tun wir? Die Benutzer können weiterhin auf ihre einzelnen Server zugreifen – aber sollten Sie Sie zulassen? Wir möchten nicht, dass Sie Änderungen vornehmen, die in Konflikt stehen, aber wir möchten sicher sein, dass Sie weiterhin arbeiten und unser Unternehmen Geld verdienen. Wenn Änderungen an diesem Punkt willkürlich blockiert werden, können keine Benutzer arbeiten, auch wenn keine Konflikte auftreten.\! Es gibt keine Möglichkeit, den anderen Servern mitzuteilen, dass die Datei verwendet wird und Sie sich wieder auf Quadrat eins befinden.  
  
![Topologie](./media/understanding-the-lack-of-distributed-file-locking-in-dfsr/5.png)
  
Dann gibt es SMB selbst und die Fehlerbehandlung von Berichterstattungs sperren. Wir können die Art und Weise, wie SMB-Berichte freigegeben werden, nicht ändern, da wir eine Menge von Anwendungen unterbrechen und Clients die neuen erweiterten Fehlermeldungen trotzdem nicht verstehen Anwendungen wie Word 2007 führen einige unter Deckung aus, um herauszufinden, wer Dateien sperrt, aber die meisten Anwendungen wissen nicht, wer über eine Datei verwendet wird (oder sogar, dass SMB vorhanden ist). Tatsächlich.). Wenn ein Benutzer also die Meldung "diese Datei wird verwendet" erhält, ist er nicht besonders handlungsfähig – sollte er den Helpdesk anrufen? Hat der Helpdesk Zugriff auf alle Dateiserver, um zu sehen, welche Benutzer auf Dateien zugreifen? Unübersichtlich.  
  
Da wir multimasterunterstützung für hohe Verfügbarkeit benötigen, ist ein Broker System weniger erwünscht. möglicherweise muss auf allen Servern etwas ausgeführt werden, das Ihnen die Kommunikation mit nicht vollständig gerouteten Netzwerken ermöglicht. Dies erfordert sehr komplexe Synchronisierungs Techniken. Dies führt zu einem gewissen Verwaltungsaufwand (obwohl wahrscheinlich nicht viel), und es muss sich um einen blitzschnell handeln, um sicherzustellen, dass wir den Benutzer nicht in der Arbeit halten. Es muss die Datei Replikation selbst überstehen. tatsächlich muss Sie tatsächlich an die Replikation gebunden werden. Außerdem müssen Serverausfälle berücksichtigt werden, bei denen es sich um Netzwerk-und nicht um Serverabstürze handelt.  

![Topologie](./media/understanding-the-lack-of-distributed-file-locking-in-dfsr/6.png)
  
Und dann kommen wir zur speziellen Client Software für dieses Szenario zurück, die die Sperren besser versteht und dem Benutzer einige nützliche Informationen geben kann ("anrufen Sie sich bei der Buchhaltung an, und teilen Sie dem Dokument mit, dass die Datei Sperr Topologie beschädigt ist, und Ihr Administrator hindert Sie daran, diese Datei zu öffnen, bis Sie korrigiert wird" usw.). Es ist definitiv interessant, dies mit den Millionen von Anwendungen zu erreichen, die unter Windows ausgeführt werden. Es gibt viele Betriebssysteme, die nicht unterstützt werden oder die Software erhalten – Windows 2000 ist von grundlegender Unterstützung und XP bald. Linux-und Mac-Clients hätten diese Software erst dann, wenn Sie es als wichtig empfunden hätte, damit der Kunde hoffen muss, dass seine Hersteller etwas ähnliches gemacht haben.  
  
## <a name="more-inforamtion"></a>Weitere Informationen
  
Die einfachste Möglichkeit, diese Situation in DFSR zu steuern, besteht darin, dass Sie DFS-Namespaces verwenden, um Benutzer zu vorhersagbaren Orten mit einem konsistenten Namespace zu leiten. Durch die ordnungsgemäße Konfiguration der DFSN-Standort Topologie und der Server Verknüpfungen erzwingen Sie, dass Benutzer denselben lokalen Server freigeben und nur den Zugriff auf Remote Computer gestatten, wenn der Server "Main" nicht mehr zur Verfügung steht. In den meisten Umgebungen funktioniert dies ziemlich gut. Alternative zu DFSR, SharePoint ist eine Option, da es sich um ein Auschecken-/Eincheck System handelt. BranchCache (in Windows Server 2008 R2 und Windows 7) ist möglicherweise eine Option für Sie, da Sie für das Lesen von Dateien in einem branchszenario konzipiert ist, aber letztendlich bleiben die autorisierenden Daten immer noch auf einem Server, – [hier](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj127252(v=ws.11))mehr. Und auch hier haben diese Anbieter ihre Lösungen.

