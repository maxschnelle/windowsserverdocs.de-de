---
title: Problembehandlung bei ADBA-Clients
description: Exemplarische Vorgehensweise für einen Problembehandlungsprozess bei Problemen mit der Windows-Aktivierung
ms.topic: troubleshooting
ms.date: 09/24/2019
ms.technology: server-general
author: Teresa-Motiv
ms.author: v-tea
manager: dcscontentpm
ms.localizationpriority: medium
ms.openlocfilehash: d56b2d002b0403971dc50fab639f77bddf1f8809
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86959882"
---
# <a name="example-troubleshooting-active-directory-based-activation-adba-clients-that-do-not-activate"></a>Beispiel: Problembehandlung bei ADBA-Clients (Active Directory Based Activation), die sich nicht aktivieren lassen

> [!NOTE]
> Dieser Artikel wurde ursprünglich als TechNet-Blog am 26. März 2018 veröffentlicht.

Hallo an alle! Mein Name ist Mike Kammer, und ich bin jetzt seit etwas über zwei Jahren Plattform-PFE bei Microsoft. Ich leistete kürzlich Support für einen Kunden bei der Bereitstellung von Windows Server 2016 in seiner Umgebung. Wir nutzen die Gelegenheit, um zugleich die Aktivierungsmethode von einem KMS-Server auf [Aktivierung über Active Directory](/previous-versions/windows/hh852637(v=win.10)) umzustellen.

Als ordnungsgemäßes Verfahren zum Vornahmen aller Änderungen begannen wir unsere Migration in der Testumgebung des Kunden. Wir begannen unsere Bereitstellung, indem wir die Anweisungen in dem hervorragenden Blogbeitrag von Charity Shelbourne befolgten, [Active Directory-Based Activation vs. Key Management Services](https://techcommunity.microsoft.com/t5/Core-Infrastructure-and-Security/Active-Directory-Based-Activation-vs-Key-Management-Services/ba-p/256016) (Aktivierung über Active Directory im Vergleich mit Schlüsselverwaltungsdiensten). Sämtliche Domänencontroller in unserer Testumgebung führten Windows Server 2012 R2 aus, daher brauchten wir keine Vorbereitung der Gesamtstruktur durchzuführen. Wir installierten die Rolle auf einem Windows Server 2012 R2-Domänencontroller und wählten Aktivierung über Active Directory als Volumenaktivierungsmethode aus. Wir installierten unseren KMS-Schlüssel und gaben ihm den Namen „KMS AD Activation ( ** LAB)“. Wir folgten dem Blogbeitrag weitgehend Schritt für Schritt.

Zunächst erstellten wir vier virtuelle Computer, zwei mit Windows 2016 Standard und zwei mit Windows 2016 Datacenter. An diesem Punkt sah alles gut aus, und alle waren zufrieden. Wir erstellten einen physischen Server, der Windows 2016 Standard ausführte, und der Computer wurde ordnungsgemäß aktiviert. Und hier endet unsere Geschichte.

Hahaha! Reingelegt! So leicht geht es wirklich nie. Ja, es stimmt schon, das Setup und die Konfiguration waren superleicht, dieser Teil war wirklich einfach und geradlinig. Ich kehrte am Montag ins Büro zurück, und alle virtuellen Computer, die ich in der Woche zuvor aufgebaut hatte, zeigten an, dass sie nicht aktiviert waren. Komm schon! So geht‘s aber nicht! Ich kehrte zum physischen Computer zurück, und der war in Ordnung. Ich setzte mich mit dem Kunden in Verbindung, um zu erörtern, was passiert war. Natürlich lautete die erste Frage: „Was hat sich am Wochenende geändert?“ Und wie üblich war die Antwort: „Nichts“. Aber diesmal hatte sich tatsächlich nichts Nennenswertes geändert, und wir mussten herausfinden, was los war.

Ich begab mich zu einem meiner problematischen Server, öffnete eine Eingabeaufforderung und überprüfte die Ausgabe des Befehls **slmgr /ao-list**. Mit dem Schalter **/ao-list** werden alle Aktivierungsobjekte in Active Directory angezeigt.

![Abbildung des Befehls „slmgr“](./media/032618_1700_Troubleshoo1.png)

![Abbildung der Ausgabe des Befehls „slmgr“](./media/032618_1700_Troubleshoo2.png)

Die Ergebnisse zeigen, dass wir über zwei Aktivierungsobjekte verfügen: eins für Server 2012 R2 und eins für unsere neu erstellte „KMS AD Activation (** LAB)“, dabei handelt es sich um unsere Windows Server 2016-Lizenz. Dies bestätigt, dass unser Active Directory ordnungsgemäß für die Aktivierung von Windows KMS-Clients konfiguriert ist.

Im Bewusstsein, dass der **slmgr**-Befehl mein Freund und Helfer bei der Lizenzaktivierung ist, fuhr ich mit verschiedenen Optionen fort. Ich probierte es mit dem Schalter **/dlv**, mit dem detaillierte Lizenzinformationen angezeigt werden. Für mich sahen die in Ordnung aus, ich führte die Standardversion von Windows Server 2016 aus, es gab eine Aktivierungs-ID, eine Installations-ID, eine Validierungs-URL und sogar den Teil eines Product Keys.

![Abbildung der Ausgabe von „slmgr /dlv“](./media/ActivationTroubleshoot2b.jpg)

Fällt jemandem auf, was mir an dieser Stelle entgangen ist? Wir kommen nach den weiteren Schritten zur Problembehandlung darauf zurück, für den Moment soll so viel genügen: Der Screenshot enthält die Antwort.

Meine Gedanken an diesem Punkt waren, dass aus irgendeinem Grund der Schlüssel defekt war, also verwendete ich den Schalter **/upk**, der den aktuellen Schlüssel deinstalliert. Das war zwar erfolgreich beim Entfernen des Schlüssels, es ist aber im Allgemeinen nicht die beste Vorgehensweise. Sollte der Server neu gestartet werden, bevor er einen neuen Schlüssel erhalten hat, kann das den Server in einen unbrauchbaren Zustand versetzen. Ich fand dann heraus, dass bei Verwendung des Schalters **/ipk** (den ich später in der Problembehandlung noch einsetze) der vorhandene Schlüssel überschrieben wird, und das ist ein viel sichereres Verfahren. Lernen Sie aus meinen Fehlern!

![Abbildung des Befehls „slmgr /upk“ und seiner Ausgabe](./media/032618_1700_Troubleshoo3.png)

Ich führte den Schalter **/dlv** erneut aus, um die detaillierten Lizenzinformationen anzuzeigen. Leider erhielt ich dadurch keine nützlichen Informationen, nur einen Fehler „Product Key nicht gefunden“. Natürlich gibt es keinen Schlüssel, den habe ich ja gerade deinstalliert!

![Abbildung des Befehls „slmgr /dlv“ und seiner Ausgabe](./media/032618_1700_Troubleshoo4.png)

Das war also nichts, aber ich probierte den Schalter **/ato** aus, der Windows mithilfe der bekannten KMS-Server (oder Active Directory in diesem Fall) aktivieren sollte. Wieder nur ein Produkt nicht gefunden-Fehler.

![Abbildung des Befehls „slmgr /ato“ und seiner Ausgabe](./media/032618_1700_Troubleshoo5.png)

Mein nächster Gedanke war, dass das Problem sich manchmal durch Beenden und erneutes Starten eines Diensts beheben lässt, also probierte ich das als nächstes. Ich musste den SPPSvc-Dienst (Microsoft Software Protection Platform Service) beenden und neu starten. An einer Administratoreingabeaufforderung verwendete ich die vertrauten Befehle **net stop** und **net start**. Zunächst fiel mir auf, dass der Dienst nicht ausgeführt wurde, also dachte ich, das muss es sein!

![Abbildung der Ausgaben der Befehle „net stop“ und „net start“](./media/032618_1700_Troubleshoo6.png)

Falsch gedacht. Nach dem Starten des Diensts und dem erneuten Versuch, Windows zu aktivieren, erhalte ich immer noch den Produkt nicht gefunden-Fehler.

Anschließend sah ich mir das Anwendungsereignisprotokoll auf einem der Problemserver an. Ich fand einen Fehler im Zusammenhang mit der Lizenzaktivierung, Ereignis-ID 8198 mit dem Code 0x8007007b.

![Abbildung mit den Details von Ereignis-ID 8198](./media/032618_1700_Troubleshoo7.png)

Beim Nachschlagen dieses Codes fand ich einen Artikel, der besagte, dass die Syntax für den Dateinamen, Verzeichnisnamen oder die Volumebezeichnung falsch sei. Beim Durchlesen der im Artikel beschriebenen Methoden hatte ich nicht den Eindruck, dass sie irgendwie auf meine Situation passten. Als ich den Befehl **nslookup -type=all _vlmcs._tcp** ausführte, fand ich den vorhandenen KMS-Server (es gab in der Umgebung noch viele Windows 7- und Server 2008-Computer, also wurde der noch benötigt) und außerdem die fünf Domänencontroller. Dies wies darauf hin, dass es sich nicht um ein DNS-Problem handelte und meine Schwierigkeiten eine andere Ursache hatten.

![Abbildung der Ausgabe des Befehls „nslookup“](./media/032618_1700_Troubleshoo8.png)

Also ist klar, dass DNS in Ordnung ist. Active Directory ist ordnungsgemäß als KMS-Aktivierungsquelle konfiguriert. Mein physischer Server wurde ordnungsgemäß aktiviert. Konnte dies ein Problem sein, das nur virtuelle Computer betrifft? Als interessanten Aspekt am Rande teilte mit mein Kunde mit, dass jemand in einer anderen Abteilung sich entschieden hatte, ebenfalls virtuelle Windows Server 2016-Computer aufzubauen, gleich mehr als ein Dutzend. Also ging ich davon aus, mich um ein weiteres Dutzend Server kümmern zu müssen, die sich nicht aktivieren ließen. Weit gefehlt. Diese Server wurden problemlos aktiviert.

Mich verschlug es also wieder zurück zu meinem **slmgr**-Befehl, um herauszufinden, wie sich diese Monster aktivieren ließen. Diesmal verwendete ich den Schalter **/ipk**, der die Installation eines Product Keys ermöglicht. Ich begab mich zu [dieser Website](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj612867(v=ws.11)), um die passenden Schlüssel für meine Standardversion von Windows Server 2016 abzurufen. Bei einigen meiner Server handelt es sich um die Datacenter-Edition, aber diesen muss ich zuerst reparieren.

![Abbildung der Liste der KMS-Clientsetupschlüssel](./media/032618_1700_Troubleshoo9.png)

Ich verwendete den Schalter **/ipk**, um einen Product Key zu installieren, und wählte den Schlüssel für Windows Server 2016 Standard aus.

![Abbildung des Befehls „slmgr /ipk“ und seiner Ausgabe](./media/032618_1700_Troubleshoo10.png)

Von hier an habe ich nur noch Ergebnisse für die Datacenter-Server erfasst (es waren die gleichen). Ich verwendete den Schalter **/ato**, um die Aktivierung zu erzwingen. Und erhalte die umwerfende Nachricht, dass das Produkt erfolgreich aktiviert wurde!

![Abbildung des Befehls „slmgr /ato“ und seiner Ausgabe](./media/032618_1700_Troubleshoo11.png)

Bei nochmaligem Verwenden des **/dlv**-Schalters war zu sehen, dass wir von Active Directory aktiviert wurden.

![Abbildung des Befehls „slmgr /dlv“ und seiner Ausgabe](./media/032618_1700_Troubleshoo12.png)

Tja, aber was war eigentlich schief gelaufen? Warum musste ich den installierten Schlüssel entfernen und diese generischen Schlüssel hinzufügen, um eine ordnungsgemäße Aktivierung dieser Computer zu erreichen? Warum ließ sich das andere Dutzend (oder so) Computer problemlos aktivieren? Wie ich bereits erwähnt habe, war mir in der Frühphase meiner Auseinandersetzung mit dem Problem etwas entgangen. Ich war gründlich verwirrt, also setzte ich mich mit Charity, der Verfasserin des zitierten Blogbeitrags, in Verbindung, um zu erfahren, ob sie mir helfen konnte. Sie erkannte das Problem sofort und half mir, zu verstehen, was ich anfangs übersehen hatte.

Bei der ersten Ausführung des **/dlv**-Schalters enthielt die Beschreibung den Schlüssel. Die Beschreibung lautete „Windows® Operating System, RETAIL Channel“. Ich hatte mir das angesehen und gedacht, „RETAIL Channel“ bedeute, dass der Schlüssel erworben worden war und also einen gültigen Schlüssel darstellte.

![Abbildung der Ausgabe von „slmgr /dlv“ mit hervorgehobener Distributionskanalinformation](./media/032618_1700_Troubleshoo13.png)

Wenn wir die Ausgabe des Schalters **/dlv** eines der ordnungsgemäß aktivierten Server betrachten, achten Sie darauf, dass die Beschreibung jetzt „VOLUME_KMSCLIENT channel“ besagt. Dadurch wissen wir, dass es sich tatsächlich um eine Volumenlizenz handelt.

![Abbildung der Ausgabe von „slmgr /dlv“ mit hervorgehobener Distributionskanalinformation](./media/032618_1700_Troubleshoo14.png)

Also was bedeutet dann „RETAIL channel“? Nun, in diesem Fall bedeutet es, dass das zur Installation des Betriebssystems verwendete Medium ein MSDN-ISO-Image war. Ich wandte mich also wieder an meinen Kunden und fragte ihn, ob möglicherweise ein zweites Windows Server 2016-ISO-Image im Netzwerk vorhanden war. Und es stellte sich heraus: Ja, es gab ein weiteres ISO-Image im Netzwerk, und das war verwendet worden, um das andere Dutzend Computer zu erstellen. Die beiden ISO-Images wurden verglichen, und das, welches ich erhalten hatte, um die virtuellen Server zu erstellen, war ein MSDN-ISO-Image. Sie entfernten das MSDN-ISO-Image aus ihrem Netzwerk, und jetzt sind alle vorhandenen Server aktiviert und die Sorgen wegen Aktivierungsfehlern bei zukünftigen Installationen ausgeräumt.

Ich hoffe, diese Informationen waren nützlich für Sie und sparen Ihnen in Zukunft Zeit!

Mike
