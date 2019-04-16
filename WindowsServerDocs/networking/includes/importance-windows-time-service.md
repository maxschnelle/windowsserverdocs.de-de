## <a name="importance-of-time-protocols"></a>Bedeutung der Zeit Protokolle
Zeit Protokolle Kommunikation zwischen zwei Computern zum Austausch von Informationen, und klicken Sie dann diese Informationen verwenden, um ihre Uhren synchronisieren. Mit dem Windows-Zeitdienst Service Time-Protokoll ein Client fordert Informationen von einem Server und synchronisiert die Uhr auf Basis der Informationen, die empfangen werden.
  
Windows-Zeitdienst verwendet NTP, um die Zeit in einem Netzwerk zu synchronisieren. NTP ist ein Internet-Zeit-Protokoll, das die Disziplin Algorithmen für die Synchronisierung von Uhren erforderlichen enthält. NTP ist eine genauere NTP als SNTP Simple Network Time Protocol (), die in einigen Versionen von Windows verwendet wird. Allerdings unterstützt auch weiterhin W32Time SNTP um Abwärtskompatibilität mit Zeit SNTP-basierte Dienste wie z. B. Windows 2000-Computern zu aktivieren.

Es gibt viele verschiedene Gründe dafür, dass Sie genaue Zeit benötigen.  Der häufigste Fall für Windows ist Kerberos, das 5Minuten Genauigkeit zwischen Client und Server erforderlich ist.  Es gibt jedoch viele andere Bereiche, die Zeit Genauigkeit einschließlich betroffen sein können:


- Gesetzlichen Vorschriften wie folgt:
    - 50 ms Genauigkeit für FINRA in den USA
    - 1 ms ESMA (MiFID II) in der EU.
- Kryptografische Algorithmen
- Verteilte Systeme wie Cluster/SQL/Exchange und Dokument-DBs
- Blockchain-Framework für Bitcoin-Transaktionen
- Verteilte Protokolle und Analyse 
- Active Directory-Replikation
- PCI (Payment Card Industry) derzeit 1Sekunde Genauigkeit