# Potyczki - Finały

### Zadanie 1

- Na klastrze "potyczki" utwórz projekt "web-server" a w nim namespace "nginx". W tym namespace uruchom kontener “nginx” w najnowszej wersji. **5pkt**
    1. Tutaj dodać projekt + namespace
    
    ![Untitled](Potyczki%20-%20Fina%C5%82y%20cc9a00c0aa9c475a8f42391188f15249/Untitled.png)
    
    1. Dodać nowy deployment z nginxem i 3 replikami
    
    ![Untitled](Potyczki%20-%20Fina%C5%82y%20cc9a00c0aa9c475a8f42391188f15249/Untitled%201.png)
    
- - Utwórz usługę dzieki której można się odwołać do naszego nginx z całego klastra **5pkt**
    
    zrobić nowy ClusterIP
    
    ![Untitled](Potyczki%20-%20Fina%C5%82y%20cc9a00c0aa9c475a8f42391188f15249/Untitled%202.png)
    
- - Zapewnij dostępność usługi na internet. Nie masz czasu czekać aż administratorzy sieci udostępnią ci firmowy DNS, a potrzebujesz szybko przetestować dostępność, więc wymyśl jak zapewnić rozwiązywalny url wskazujący na IP hosta, na którym jest twój klaster "potyczki". **25pkt** (pełnym rozwiązaniem jest podanie adresu typu nginx.xxxx.xxxx.xx rozwiązywalnego przy pomocy DNS z internetu, pod którym zgłosi się działająca usługa);
- zrobić nowy ingress, ustawić request host na [nginx.193.187.69.137.sslip.io](http://nginx.193.187.69.137.sslip.io/) i default backend na naszą appkę
    
    ![Untitled](Potyczki%20-%20Fina%C5%82y%20cc9a00c0aa9c475a8f42391188f15249/Untitled%203.png)
    
    # Zadanie 2
    
    1. Sprawdzanie wymagań:
    
    ![Untitled](Potyczki%20-%20Fina%C5%82y%20cc9a00c0aa9c475a8f42391188f15249/Untitled%204.png)
    
    1. doinstalowanie open-iscsi i zenablowanie iscsid, oraz instalacja nfs client
    2. instalacja longhorna przez ranchera z odpowiednia konfiguracja
    3. sprawdzenie statusu podów longhorna przez `kubectl -n longhorn-system get all` oraz ui longhorna

### Zadanie 3

- Dodaj nowe repozytorium do katalogu aplikacji Ranchera. URL repo: [https://rancher.github.io/rodeo](https://rancher.github.io/rodeo) **5pkt**
    1. Dodać nowe repozytorium
    
    ![Untitled](Potyczki%20-%20Fina%C5%82y%20cc9a00c0aa9c475a8f42391188f15249/Untitled%205.png)
    
- Zainstaluj aplikację Tetris z nowo dodanego repo. **5 pkt**
    1. instalacja tetrisa z chartów:
    
    ![Untitled](Potyczki%20-%20Fina%C5%82y%20cc9a00c0aa9c475a8f42391188f15249/Untitled%206.png)
    
    2. Widoczny z: [https://rancher.193.187.69.86.sslip.io/k8s/clusters/c-m-f5btps2c/api/v1/namespaces/tetris/services/http:tetris:80/proxy/](https://rancher.193.187.69.86.sslip.io/k8s/clusters/c-m-f5btps2c/api/v1/namespaces/tetris/services/http:tetris:80/proxy/) (nie robiliśmy ingressu, ponieważ nigdzie nie pisało, że mamy ją wystawić na internet :/)
    
    ![Untitled](Potyczki%20-%20Fina%C5%82y%20cc9a00c0aa9c475a8f42391188f15249/Untitled%207.png)
    

### Zadanie 4

- Z katalogu aplikacji zainstaluj NeuVector w najnowszej stabilnej wersji. **10pkt**
    1. ustawić wersję 5.3.0 (jako najnowsza stabilna)
        
        ![Untitled](Potyczki%20-%20Fina%C5%82y%20cc9a00c0aa9c475a8f42391188f15249/Untitled%208.png)
        
    2. ustawić containerd jako enabled (cluster jest postawiony na RKE2)
        
        ![Untitled](Potyczki%20-%20Fina%C5%82y%20cc9a00c0aa9c475a8f42391188f15249/Untitled%209.png)
        
    3. opcjonalnie: ustawić mniej replik (z 3 na jednym node’dzie było strasznie duże zużycie CPU)
    4. NeuVector dostępny pod: [https://rancher.193.187.69.86.sslip.io/k8s/clusters/c-m-f5btps2c/api/v1/namespaces/cattle-neuvector-system/services/https:neuvector-service-webui:8443/proxy](https://rancher.193.187.69.86.sslip.io/k8s/clusters/c-m-f5btps2c/api/v1/namespaces/cattle-neuvector-system/services/https:neuvector-service-webui:8443/proxy)
- Włącz funkcję Auto-scan **5 pkt**
    1. włączenie auto-scannowania (nodes, platforms i containers)
    
    ![Untitled](Potyczki%20-%20Fina%C5%82y%20cc9a00c0aa9c475a8f42391188f15249/Untitled%2010.png)
    

### Zadanie 5

- Nasi deweloperzy chcą korzystać z publicznie dostępnych obrazów, ale mogą one zawierać groźne podatności. Dlatego chcemy najperw przeskanować rejestr, zanim zaczniemy z niego korzystać. Użyj NeuVector, żeby przeskanować sekcję nvbeta/* w rejestrze [https://registry.hub.docker.com](https://registry.hub.docker.com/) ; jako rozwiązanie podaj nazwę image z największą ilością podatności. **7pkt**
    1. dodać nowe registry
    
    ![Untitled](Potyczki%20-%20Fina%C5%82y%20cc9a00c0aa9c475a8f42391188f15249/Untitled%2011.png)
    
    1. lista przeskanowanych image’y:
    
    ![Untitled](Potyczki%20-%20Fina%C5%82y%20cc9a00c0aa9c475a8f42391188f15249/Untitled%2012.png)
    
    Najwięcej vulnów jest w: `nvbeta/node:latest`
    

# Zadanie 6

1. Zmiana nie-usuwa.yaml z deploymentu na statefulset
2. zdeployowanie nie-usuwaj.yaml do namespace’u `stateful` przez komende `kubectl -n stateful apply -f nie-usuwaj.yaml`
3. sprawdzenie działania:

![Untitled](Potyczki%20-%20Fina%C5%82y%20cc9a00c0aa9c475a8f42391188f15249/Untitled%2013.png)

![Untitled](Potyczki%20-%20Fina%C5%82y%20cc9a00c0aa9c475a8f42391188f15249/Untitled%2014.png)

![Untitled](Potyczki%20-%20Fina%C5%82y%20cc9a00c0aa9c475a8f42391188f15249/Untitled%2015.png)

### Zadanie 7

- Twój niezbyt rozgarnięty kolega z pracy, Adrian, prosi cię o poradę: w klastrze mam pewien resource, ale nie wiem jak znaleźć yaml tego zasobu? Jak go podejrzeć?
**5pkt**, +**7pkt** za dodatkową metodę
1. metoda pierwsza: `kubectl -n <namespace> get <resource_path> -o yaml` 
przykład: `kubectl -n nginx get deployments.apps/nginx -o yaml`
2. druga metoda: wejść w resource przez Ranchera i kliknąć `download YAML` 

![Untitled](Potyczki%20-%20Fina%C5%82y%20cc9a00c0aa9c475a8f42391188f15249/Untitled%2016.png)

### Zadanie 7.5

- Adrian uruchomił aplikację składającą się z front-endu i bazy danych MySQL. Widzisz, że jego kontener MySQL jest uruchomiony na najprostszych domyślnych ustawieniach. Czy jest to zalecany sposób? Uzasadnij w kilku zdaniach (min. 20 słów dla pełnej punktacji).
**5pkt**, +**5pkt** jeśli uzasadnienie zawiera za i przeciw oraz sugestię poprawy
1. Nie, domyślne ustawienia posiadają proste do zgadnięcia hasło `secretpass` i użytkownika `root, który ma uprawnienia do wszystkich baz danych. Hackierzy` potem będą mogli się dostać do danych klientów/serwisu. Pomidor.
    
    Za:
    
    - prosty deployment
    
    Przeciw:
    
    - Domyślne ustawienia nie są zoptymalizowane dla wydajności
    - brak serwisu dla bazy danych
    - Korzystanie z `MYSQL_USER` i `MYSQL_PASSWORD` , a nie usera `root` dla lepszego bezpieczeństwa
    - Zmienienie hasła dla roota (na coś trudniejszego niż `secretpass`)

**Zadanie 8**

- Wytłumacz Adrianowi w kilku prostych zdaniach czym jest resource o nazwie Gateway w Kubernetes? (min. 20 słów dla pełnej punktacji) **7pkt**
    1. Gateway to tak naprawdę Ingress, tylko ma więcej funkcji + jest successorem dla Ingressów. Może matchować skomplikowane pathy łatwo i tworzyć HTTPRoute’y które są podobne do tych z Traefika. Dodatkowo, zwiększają bezpieczeństwo i umożliwiają zarządzenie i monitorowaniem ruchu.

### Zadanie 9

- Adrian jest bardzo skonfundowany dlaczego są dwa różne resource w Kubernetes, które "robią to samo" czyli zarządzają zestawem identycznych podów: Deployment i ReplicaSet. Wyjaśnij mu na czym polega różnica między tymi resource'ami. (min. 20 słów dla pełnej punktacji) **7pkt**
1. Deployment jest abstrakcją wyższego poziomu, która tworzy i zarządza ReplicaSet’ami. Posiada więcej funkcji jak np. Rolling updates, rollbacks, skalowanie itp. ReplicaSet jest abstrakcją niższego poziomu i zapewnia tylko podstawowe funkcje jak trzymanie liczby podów, zastępowanie podów itp.

### Zadanie 10

- Dokonaj aktualizacji klastra "potyczki" to nowszej wersji Kubernetes tak, żeby zminimalizować jej wpływ na dostępność uruchomionych workloadów. **10pkt**
    1. Cluster management → Edit config → zmiana wersji na najnowszą (podczas upgrade’u web-server z zadania 1 cały czas działał)
    
    ![Untitled](Potyczki%20-%20Fina%C5%82y%20cc9a00c0aa9c475a8f42391188f15249/Untitled%2017.png)
    
    1. zupgradeowany cluster
    
    ![Untitled](Potyczki%20-%20Fina%C5%82y%20cc9a00c0aa9c475a8f42391188f15249/Untitled%2018.png)
    

### Zadanie 11

Firma zatrudniła właśnie dwóch nowych pracowników, jako administrator środowiska Kubernetes twoim zadaniem jest utworzyć dla nich konta użytkowników o nazwach w formacie imie.nazwisko i poprawnie przypisać im uprawnienia:

- Nowym dyrektorem IT został Muhammed Yassuff i nalega, żeby mieć podgląd na działanie całego środowiska (uprawnienia get, list, watch).
- Przyjęliśmy także świeżego praktykanta, któremu na razie powierzyliśmy tylko utrzymanie (tj. pełna kontrola) projektu "web-server". Nazywa się on Muhhamad Yussuff.

**5 pkt** za utworzenie dwóch lokalnych użytkowników, po **7 pkt** za poprawne przypisanie uprawnień do każdego z nich (**+5** dodatkowych punktów za rozwiązanie bez żadnej pomyłki i nie nadanie dyrektorowi prawa do podglądu sekretów)

- muhammed.yassuff:VMhnjkbXSVrPYoOV
- muhhamad.yussuff:iBXyswlPVd0vh1l1

1. Stworzenie nowej roli dla dyrektora z get, list, watch i danie tylko list na secrets

![Untitled](Potyczki%20-%20Fina%C5%82y%20cc9a00c0aa9c475a8f42391188f15249/Untitled%2019.png)

1. dodanie dyrektora do clustra:

![Untitled](Potyczki%20-%20Fina%C5%82y%20cc9a00c0aa9c475a8f42391188f15249/Untitled%2020.png)

1. sprawdzenie: dyrektor nie ma zakładki secrets

![Untitled](Potyczki%20-%20Fina%C5%82y%20cc9a00c0aa9c475a8f42391188f15249/Untitled%2021.png)

1. dodanie praktykanta do projektu:

![Untitled](Potyczki%20-%20Fina%C5%82y%20cc9a00c0aa9c475a8f42391188f15249/Untitled%2022.png)

### Zadanie 12

- Jeden z workloadów na klastrze "potyczki", Deployment o nazwie "mysql", nie działa poprawnie. Deweloperzy napisali yaml, ale winią Adriana bo on go zdeployował na klastrze i na pewno coś popsuł bo yaml przecież był ok. Znajdź przyczynę błędu i napraw go. **30 pkt**
1. w rancherze: mysql ma przydzielone za mało ramu, rozwiązanie to: zbumpowanie limitu ramu do 512Mi

![Untitled](Potyczki%20-%20Fina%C5%82y%20cc9a00c0aa9c475a8f42391188f15249/Untitled%2023.png)

1. po tych zmianach, deployment mysql’a działa

![Untitled](Potyczki%20-%20Fina%C5%82y%20cc9a00c0aa9c475a8f42391188f15249/Untitled%2024.png)

### Zadanie 13

- Nasz workload "nginx" z projektu "web-server" (Zadanie 1) jest prawdopodobnie atakowany z internetu! Użyj NeuVector, żeby zwizualizować wszystkie połączenia sieciowe w klastrze i zapisz zrzut ekranu do dokumentacji (**5 pkt**), oraz przechwyć i zapisz pakiety z ruchu przychodzącego do "nginx" (**10 pkt**). Jeśli Zadanie 1 jest niewykonane, możesz przechwycić pakiety innego poda (udokumentuj który). Możesz sztucznie wygenerować zapytania, żeby mieć co przechwycić. +**7 pkt** za opis na czym polega analiza pakietów i podanie przykładowego narzędzia do takiej analizy (min. 20 słów dla pełnej punktacji)
1. Network Activity → prawym na nginx → packet capture → download

![Untitled](Potyczki%20-%20Fina%C5%82y%20cc9a00c0aa9c475a8f42391188f15249/Untitled%2025.png)

1. Dodajemy plik .pcap (czyli dump pakietów do Wiresharka), pakiety te to pakiety TCP, które przychodziły z ingressu (który load balancuje traffic pomiędzy 3 repliki tego nginx’a). Pakiety te to tak naprawdę requesty HTTP, które możemy podejrzeć dzięki Wiresharkowi. Po prawej widać HTML’a którym serwer responduje.

![Untitled](Potyczki%20-%20Fina%C5%82y%20cc9a00c0aa9c475a8f42391188f15249/Untitled%2026.png)

### Zadanie 14

- Adrian próbuje zdeployować nowy workload i chyba tym razem rzeczywiście coś zepsuł bo za nic nie chce się to uruchomić. Napraw i uruchom adrian-nginx.yaml w nowym namespace o nazwie "adrian". **40 pkt**
1. Ustawienie poprawnych health checków: readiness miał zły port (8080), a liveness wysyłał request na nieistniejący path.

![Untitled](Potyczki%20-%20Fina%C5%82y%20cc9a00c0aa9c475a8f42391188f15249/Untitled%2027.png)

1. Kubernetes teraz poprawnie wyświetla health-status dla nginxa. (nie dodawaliśmy serwisu, ponieważ nie było w poleceniu :()

![Untitled](Potyczki%20-%20Fina%C5%82y%20cc9a00c0aa9c475a8f42391188f15249/Untitled%2028.png)

### Zadanie 15

- Przy pomocy NeuVector utwórz regułę blokującą połączenia wychodzące z nginx (Zadanie 3) na zewnątrz klastra i przełącz w tryb aktywnej ochrony (Protect). (**10 pkt**) Wyeksportuj regułę jako CRD w trybie Protect i załącz do dokumentacji (**5 pkt**). Potwierdź działanie reguły logując się do shella poda nginx i wykonując polecenie curl [suse.com](http://suse.com/)  (**7 pkt**). Zablokuj również samo polecenie curl w tym podzie i potwierdź działanie reguły logując się do shella. (**10 pkt**). Dopuszczalne potwierdzenia to zrzuty ekranu lub skopiowane w całości komunikaty shella wraz z poleceniem, które je wyzwoliło - dołącz do dokumentacji.
1. Przełączenie grupy w tryb Protect

![Untitled](Potyczki%20-%20Fina%C5%82y%20cc9a00c0aa9c475a8f42391188f15249/Untitled%2029.png)

1. Dodanie network rule

![Untitled](Potyczki%20-%20Fina%C5%82y%20cc9a00c0aa9c475a8f42391188f15249/Untitled%2030.png)

1. Zablokowanie curla

![Untitled](Potyczki%20-%20Fina%C5%82y%20cc9a00c0aa9c475a8f42391188f15249/Untitled%2031.png)

![Untitled](Potyczki%20-%20Fina%C5%82y%20cc9a00c0aa9c475a8f42391188f15249/Untitled%2032.png)

### Zadanie 16

- Jedna z naszych Service nie może się połączyć ze wskazanym Deployment'em. Uruchom "serwis.yaml" w nowym namespace "serwis" i napraw przyczynę problemu. Rozwiązaniem jest Service wskazujący poprawnie na Pod'a nginx zdeployowanego przez "serwis.yaml". **35 pkt**
1. zmienić selector na `app`

![Untitled](Potyczki%20-%20Fina%C5%82y%20cc9a00c0aa9c475a8f42391188f15249/Untitled%2033.png)

### Zadanie 17

- Kolejna instancja mysql sprawia problemy, Adrian od trzech dni przez nią nie śpi bo trzyma klaster i przecież wszystko sprawdził. Uruchom baza.yaml w nowym namespace "baza" i doprowadź do poprawnego załadowania się bazy danych. **25 pkt**
    1. Literówka w environment variablu: powinno być `MYSQL_ROOT_PASSWORD` , a nie `MYSQL_ROT_PASSWORD`

![Untitled](Potyczki%20-%20Fina%C5%82y%20cc9a00c0aa9c475a8f42391188f15249/Untitled%2034.png)

### Zadanie 18

- Adrian chciał uruchomić aplikację "hello-world", ale nawet to mu nie działa. Znajdź przyczynę problemu i uruchom hello-world. **20 pkt**
1. Zmiana architektury CPU image’u na `amd64` : z `arm64v8/hello-world` na `amd64/hello-world`

![Untitled](Potyczki%20-%20Fina%C5%82y%20cc9a00c0aa9c475a8f42391188f15249/Untitled%2035.png)