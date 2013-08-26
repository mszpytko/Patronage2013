Patronage2013
=============
Projekt CRUDRESTPlayer jest projektem NetBeans 7 aplikacji PlayersService 
realizującej usługę REST-ową przeznaczoną do   zarządzanie obiektem gracza 
w pewnej grze (obiekt: Player). 

Usługa ta pozwala na:

	•	stworzenie nowego gracza,
	•	edycję istniejącego gracza,
	•	zwrócenie wybranego gracza na podstawie jego ID,
	•	zwrócenie wybranego gracza na podstawie jego nazwiska (lastname),
	•	zwrócenie listy istniejących graczy (wszystkich bądź ze wskazanego zakresu ID),
	•	usunąć istniejącego gracza na podstawie jego ID.

Obiekt gracza przechowuje następujące informacje (dane):
ID - oryginalny identyfikator gracza (Integer),
FIRSTNAME - imię gracza (String),
LASTNAME - nazwisko gracza (String),
TEAMNAME - nazwa zespołu / klubu / drużyny  (String)

Aplikacja pracuje w środowisku serwera GlassFish 3.0 (lub wyżej).
Obiekty graczy są przechowywane w lokalnej bazie danych Java DB Derby  
(dostępna m.in. wraz z serwerem GlassFish) - dołączono skrypt umożliwiający założenie bazy 
danych - plik create-playersdb-derby.sql. 
Aktualna konfiguracja bazy danych (m.in. databaseName, User, Password) są zawarte w pliku 
sun-resources.xml projektu.

Projekt zawiera również testową klasę pomocniczą wykonującą predefiniowane operacje typu: 
pobierz i pokaż wszystkich graczy, pobierz i pokaż graczy z zadanego zakresu ID, pobierz i pokaż 
gracza o wskazanym ID lub wskazanym nazwisku, usuń gracza o wskazanym ID, modyfikuj/edytuj 
gracza o wskazanym ID oraz dodaj nowego gracza. Klasa ta przechwytuje wyjątki związane z próbą 
edycji gracza o nieistniejacym ID oraz z próbą dodania gracza w sytuacji, gdy już istnieje inny gracz 
o takim ID.

webResource=http://localhost:8080/PlayersService/api/players

Zasoby:
players/count  - operacja metody GET zwracająca liczbę graczy,
players/{id} - operacje metod: GET, PUT i DELETE dla gracza o wskazanym id,
players/player/{lastname} - j.w. dla gracza o wskazanym nazwisku,
players/{from}/{to} - operacje metod: GET, PUT i DELETE dla graczy z wskazanego zakresu id,
players - operacja metody GET zwracająca listę wszystkich graczy oraz operacja metody POST 
polegająca na dodaniu nowego gracza.

Przykłady:
1. http://localhost:8080/PlayersService/api/players
2. http://localhost:8080/PlayersService/api/players/count
3. http://localhost:8080/PlayersService/api/players/2
4. http://localhost:8080/PlayersService/api/players/2-4
5. http://localhost:8080/PlayersService/api/players/player/Chrobry

Ponadto aplikacja umożliwia prezentację strony startowej http://localhost:8080/PlayersService/index.jsp 
(m.in. lista graczy) oraz standardowej strony Test RESTful Web Services projektu/aplikacji 
http://localhost:8080/PlayersService/test-resbeans.html.

Testy możemy również przeprowadzić z poziomu command-line przy pomocy programu curl - np.
curl  -i http://localhost:8080/PlayersService/api/players -X POST -H "Accept:application/json" 
-H "Content-Type:application/json"  --data @samplepost.json
gdzie: plik samplepost.json zawiera dane opisujace dodawanego gracza -np. 
{"id":"104","firstname":"Robert","lastname":"Plant","teamname":"Celtic"} 

