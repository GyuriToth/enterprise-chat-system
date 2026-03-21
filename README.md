# Élő Chat és Bot Rendszer

Ez a projekt egy olyan csevegőalkalmazás, ahol az üzenetek frissítés nélkül, azonnal megjelennek minden résztvevőnél. A rendszer három különálló szolgáltatásból áll, amelyek hálózaton keresztül kommunikálnak egymással.

[Magyar](#magyar) | [English](#english)

---

<a name="magyar"></a>
## Hogyan működik?

1.  **Chat Szerver (Go):** Ez tartja a kapcsolatot a böngészőkkel. Amikor valaki ír egy üzenetet, ez a komponens kapja meg és küldi tovább a többieknek.
2.  **Üzenetközpont (Redis):** Ez a rendszer "postája". Ez felel azért, hogy az üzenetek eljussanak minden futó szerverpéldányhoz és a feldolgozó bothoz is.
3.  **Okos Bot (Python):** Ez a program folyamatosan figyeli az üzenetcsatornát. Ha felismer egy kulcsszót (pl. "segítség"), automatikusan választ küld a chatbe.

---

## Mikor tekinthető késznek? (Követelmények)

A projektet akkor tekintjük befejezettnek, ha az alábbi pontok stabilan működnek:

### Funkcionális elvárások
* **Azonnali szinkronizáció:** Ha két ablakban megnyitod a chatet, az egyikben elküldött üzenetnek azonnal látszódnia kell a másikban.
* **Csatlakozási jelzés:** A rendszer automatikusan kiírja, ha egy új felhasználó belép a beszélgetésbe.
* **Interaktív Bot:** Ha a felhasználó beírja a "status" szót, a Python bot válaszol a rendszer aktuális állapotáról.
* **Előzmények:** Az oldal frissítése után is látszódnak a legutóbbi üzenetek.

### Technikai követelmények
* **WebSocket kapcsolat:** A böngésző és a szerver között élő, kétirányú adatkapcsolat van (nem sima HTTP kérések).
* **Redis csatornák:** Az üzenetküldés a Redis Pub/Sub mechanizmusán keresztül történik, így a rendszer skálázható.
* **Konténerizáció:** Az egész környezet (Go, Python, Redis) elindul egyetlen `docker compose up` paranccsal.
* **Hibatűrés:** Ha a Bot szolgáltatás leáll, a felhasználók közötti üzenetváltásnak továbbra is működnie kell.

---

<a name="english"></a>
## 🇺🇸 Essentials

### Architecture
* **Server (Go):** Handles live browser connections.
* **Broker (Redis):** Distributes messages between services.
* **Bot (Python):** Monitors traffic and replies to specific keywords.

### When is it done?
* **Instant Sync:** Real-time message delivery across all clients.
* **Join Alerts:** System notifications for new participants.
* **Bot Interaction:** Automated replies for keywords (e.g., "help", "status").
* **Persistence:** Recent history remains visible after a page reload.
* **Deployment:** Fully managed via Docker Compose.
* **Resilience:** Core chat stays online even if the bot service fails.