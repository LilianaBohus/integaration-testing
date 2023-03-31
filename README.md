# Integrációs tesztelés

A tesztelési tevékenység információt biztosít az alkalmazás aktuális állapotáról.

Tesztelési szintek (tesztelési piramis)
- Unit
- Integration
- Acceptance/E2E
- Manual

Ami alsóbb szinteken tesztelünk, azt fentebb nem feltétlenül szükséges, viszont a magasabb szintű tesztek sokkal nagyobb magabiztosságot adnak a alkalmazásban.

Backend fejlesztőknek a felelősségi kör nagym értékben az Integrációs teszten van, kis kitekintéssel a UNIT és az Acceptance tesztelés irányába.
Jó esetben ezek az tesztek lokálisan futtathatóak és nem szükséges hozzájuk developmnet (kitelepített) környezet.
Ezek a tesztek automatizált tesztek, hiszen bár kézzel implementáljuk őket, nem szükséges emberi tevékenység a futtatásukhoz.

Unit teszteléshez az elterjedt eszköz a Mockito és a JUnit, amely még nem építi fel futási időben az egész SpringBoot Context-et, csak "körbemockolja" a tesztelendő komponenst (Unitot).
Fontos észbentartani, hogy Unit tesztelésről addig beszélünk "tisztán", ameddig a tesztesetünk működése/ellenőrzésének logikája nem mutat ki az adott komponensből.
(Például egy DTO Transzformációt szeretnénk ellenőrizni kézben tartható bemenettel és kimenettel, ObjectMapper-t vagy konfigurációt mockolva Mockito-val).
SpringBoot tulajdonságokat ebben nem tudunk ellenőrizni, például Resource felolvasás. Illetve több Service vagy Component osztály együttes működését sem (megfelelően jön létre egy transzformációs flow).

Integration Testing ezzel szemben felépít egy Spring Context-et a @SpringBootTest annotáció segítségével (és SpringExtension-el) és képes a komponensek/resource-ok/service-ek/database-ek közös működését ellenőrizni.
Abban térHET (cég és projekt válogatja a megnevezéseket) az Acceptance teszteléstől, hogy az integrációs tesztelésnél van lehetőség MOCK-olásra szintén mockito használatával, viszont a Unit teszteléssel ellenéátétben nem metódusokat hívunk meg, hanem a szerverünk végpontjait MockMVC használatával.