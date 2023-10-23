-   **local k8s setup**  
	- Islamovic Almin (BEG/ENG13-IOT-Wi) fertigstellen und dokumentieren
	- Waismayer Fabian (BEG/ENG13-IOT-Wi) + Crepaz Martin (BEG/ENG13-IOT-Wi): lokales k8s setup seperat testen und bei Problemen mit Almin absprechen
	<mark style="background: #BBFABBA6;">Tested - Working</mark> 
-   **local docker-compose**    
    -   Waismayer Fabian (BEG/ENG13-IOT-Wi) fertigstellen und dokumentieren
    -   Islamovic Almin (BEG/ENG13-IOT-Wi) + Crepaz Martin (BEG/ENG13-IOT-Wi): lokales k8s setup seperat testen und bei Problemen mit Almin absprechen
  
-   **Gemeinsam besprechen, wie wir local am besten Entwicklungen testen können (welches Setup wir verwenden)**    
    -   local k8s + docker compose für Tests? Nur eins von beiden? Wann nehmen wir was und warum?

-   **Local Setup auf MVP anpassen**
    -   Komponenten entfernen: SBOD, SBFD, HCFE/BE, DOS, KTS, VS (ggf. doing in Code Base, siehe unten) 
    -   Erweiterte Frage: welche Komponenten brauchen wir dennoch, um gut lokale Test durchzuführen?
<mark style="background: #BBFABBA6;">	 JMeter tests fuer die componenten die wir brauchen funktionieren. Die componenten: TBE, Postgres, Keycloak, VOS, PGadmin4, laufen ohne probleme lokal und tests sind auch grun. Info: Man muss die URL aendern und port-forward machen.</mark>
    -   Erweiterte Frage: brauchen wir pgadmin4 oder ist es auch mit [https://learn.microsoft.com/en-us/sql/azure-data-studio/quickstart-postgres?view=sql-server-ver16](https://learn.microsoft.com/en-us/sql/azure-data-studio/quickstart-postgres?view=sql-server-ver16 "https://learn.microsoft.com/en-us/sql/azure-data-studio/quickstart-postgres?view=sql-server-ver16") möglich? Bitte testen und bewerten.

-   **Local environment semantisch testen, mit:**
    -   [https://github.boschdevcloud.com/PKL/loadtest](https://github.boschdevcloud.com/PKL/loadtest "https://github.boschdevcloud.com/PKL/loadtest") (JMeter)  
<mark style="background: #BBFABBA6;">    tested with Jmeter tests works fine, need to change some of the settings, like the URLS and creds. </mark>
    -   [https://github.boschdevcloud.com/PKL/regression](https://github.boschdevcloud.com/PKL/regression "https://github.boschdevcloud.com/PKL/regression") (Postman)  

-   **Code Weiterentwicklung:**
    -   [https://github.boschdevcloud.com/PKL/telematicsbackend](https://github.boschdevcloud.com/PKL/telematicsbackend "https://github.boschdevcloud.com/PKL/telematicsbackend") als neues Repo abforken (name: beg-pkl-tb) (der, der es tun möchte)  
    - ![[Pasted image 20221116131340.png]]
    -   Sind essentielle Stellen noch mit Loggin zu erweitern? Dann go.
    -   Dummy / Hardcoded values entfernen.
    -   [https://rb-tracker.bosch.com/tracker02/browse/PKMVP-706](https://rb-tracker.bosch.com/tracker02/browse/PKMVP-706 "https://rb-tracker.bosch.com/tracker02/browse/PKMVP-706") , das Thema mit der Erhöhten Speicherlast checken. ob es beim aufsetzen und testen zu dieser Problematik kommt und es dann via Implementierung lösen.          
    -   Durch das entfernen der nicht MVP relevanten Komponenten: kommt es beim Testen oder Aufsetzen zu Fehler, weil eine Abhängigkeit zu einer nicht verwendeten Komponente bestehen: umprogrammieren.
    
-   **E2E Demonstrator**
    -   Crepaz Martin (BEG/ENG13-IOT-Wi) nach einem aktuellen Stand fragen



**[[14-11-2022]]** Updates
- Tested endpoints with Martin and Jmeter tests. The smaller version of the app is working. 
- Write down the tasks that need to be done from me 



