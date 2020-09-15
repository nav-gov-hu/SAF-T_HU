# SAF-T_HU XSD változtatásai (2020.09.15.)

## 1) Partneradatok változása
A Definitions.xsd-be kerültek át a partneradatokkal kapcsolatos adatstrukturák: SAFTHUCustomerInfoStructure, SAFTHUSupplierInfoStructure, SAFTHUPartnerInfoStructure. A TaxNumber elem mindegyik definícióban opcionálisan szerepel. A séma lehetőséget ad arra, hogy egy partner több tagországban rendelkezik adóregisztrációval, akkor a megfelelő adószámot lehet behivatkozni. A törzsadatok között a közösségi adószámot végtelenítettük (ahogy a Header-ben is), így egy vállalkozáshoz törzsadat szintjén több közösségi adószám megadható. A séma megteremti annak a lehetőségét is, hogy ha egy partner nem szerepel a törzsadatok között, akkor a teljes SAF-T struktúrában lehetséges a név és cím megadása ID adat nélkül.
Azzal, hogy a partneradatok a Definitions.xsd-be kerültek bele, egységes szerkezetet kapnak a teljes SAF-T struktúrában.

## 2) Összegek megadása
Az összegek megadását egységesen megváltoztattuk a teljes sémában. Mindenhol bevezettük a DebitAmount/CreditAmount párost, így megszűntek a korábbi verzióban az összeg struktúrájának az eltérései, valamint az előjelek hiányát is megszűntettük.

## 3) Stockmovement változások
A ProductInformation elemet opcionálissá tettük, majd üzleti validációt dolgozunk ki, hogy az értéknek vagy mennyiségnek, vagy mindkettőnek szerepelnie kell.
Bevezettünk egy PhysicalStockDetails részt egyes komplexebb készletnyilvántartási rendszerek egyszerűbb és átláthatóbb riportolási lehetőségének biztosítása miatt. A változtatások okát, valamint a PhysicalStockDetails kezelését a dokumentációban részletesen kifejtettük.

## 4) Kintlevőségek
Újrastruktúráltok az XSD ezen részét. Szétválasztottuk a partner és a bizonylati adatokat.

## 5) Tárgyi eszköz változások
A MasterData részben az AccountID-t kötelezővé tettük. Ez azt is jelenti, hogy minden eszközanalitikához kapcsolódóan szerepelnie kell a törzsadatok között, hogy a vállalkozás az adott eszközt mely főkönyvi számlán tartja nyilván. Ez a főkönyvi számlaszám lehet dedikáltan egy tárgyi eszközé is, de nyilvántarthat a vállalkozás több tárgyi eszközt is. 

## 6) GroupingLedgerIndicator
Bevezettünk egy új elemet a csoportos könyvelés jelzésére, mely három elemű enum listávával rendelkezik:
- Nem csoportos feladás
- Csoportos feladás, de nincs hozzá tartozó GroupingLedger riport állomány (pl. bérszámfejtés)
- Csoportos feladás és tartozik hozzá GroupingLedger riport állomány

## 7) Period elemek használata
Több helyen megjelent a Period elem a korábbiakhoz képest:
- GL Header
- Payment Header
- Purchase Invoice
- Sales Invoice

## 8) Taxation elemek 
A Proportional elemcsoportnak hiányzott az annotációja, ezt a hibát javítottuk.
A MasterData részben lévő TaxDeclarationInfo csomópontot végtelenítettük, hogy jobban illeszkedjen az áfa bevallás készítéshez.

## 9) Idegen készlet kezelése
A MasterData Warehouse részben megszűntettük az OwnForeignStock elemet. Az idegen készlet kezelését a MasterData Product részhez illesztettük hozzá. Amennyiben egy készletnek más a tulajdonosa, akkor az Owner struktúrában szükséges a Product alatt leírni. A dokumentációban is megváltoztattuk a Warehouse fogalmát, kivezettük az idegen készlet miatti virtuális raktár fogalmat.

## 10) Árfolyam
Az árfolyamot kötelezővé tettük az adatstruktúrában. 

## 11) TransactionID megjelenése több részben
A TransactionID lehetőséget ad arra, hogy a SAF-T adatstruktúra több részét hozzá lehet illeszteni a G/L-hez. Ezért opcionálisan a következő helyeken meg lehet adni: Purchase Invoice, Sales Invoice, StockMovement, SupplierAnalytics, CustomerAnalytics

## 12) GroupIndicator
Bevezettünk egy új elemet a cikkcsoport jelölésére a MasterData Pruduct részben. Adott cikkszámhoz vagy mennyiségi egység, vagy cikkcsoport jelölő tartozik.

## 13) TaxBase típusának változása
A TaxBase elem típusát megváltoztattuk, eddig csak a bizonylat pénznemében lehetett megadni az értéket. A változtatást követően meg lehet adni a könyvelés és a bizonylat pénznemében is.

## 14) Szállítási adatok struktúrájának változása
Módosítottunk a SAFTHUShippingPointStructure szerkezetén, vagy a WarehouseID, vagy pedig a raktár címének megadására van opcionális lehetőség. 


