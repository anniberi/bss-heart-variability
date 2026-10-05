# Heart Rate Variability: Pathology Analysis from Poincaré Plots

Seminar paper on heart rate variability (HRV) and how the shape of a Poincaré plot shows the difference between healthy and pathological cardiac rhythms. Beyond reviewing Poincaré and Bland-Altman plots, the paper proposes and implements an OpenCV-based C++ algorithm that extracts contours from Poincaré plots. These contours could serve as a first step toward classifying the plots automatically.

> **Note:** Apart from this summary, everything in this project is written in Bosnian: the rest of this README, the source code, the comments and the technical documentation.

> **Napomena:** Izvorni kod, komentari i tehnička dokumentacija za ovaj projekat su napisani na bosanskom jeziku.

## O projektu

Seminarski rad iz predmeta **Biomedicinski signali i sistemi** na Elektrotehničkom fakultetu Univerziteta u Sarajevu. Rad obrađuje srčanu varijabilnost, odnosno fiziološku varijaciju vremenskih intervala između uzastopnih otkucaja srca. Analizira i načine njenog grafičkog predstavljanja, s posebnim naglaskom na Poincaré dijagram kao alat za uočavanje patoloških stanja.

## Sadržaj rada

1. **Tipovi dijagrama za grafičko predstavljanje srčane varijabilnosti**
   - Srčana varijabilnost i podjela snimaka prema trajanju (veoma dugi, kratki i ultrakratki snimci).
   - Poincaré dijagram, s primjerima iz MIT-BIH baze podataka.
   - Bland-Altman dijagram.
2. **Detekcija patologije na osnovu Poincaré dijagrama**
   - Zdravi pacijenti imaju karakterističan oblik „komete".
   - Kod pacijenata sa srčanom insuficijencijom javljaju se oblici „torpeda", „lepeze" i složeni oblici.
3. **Algoritam za detektovanje jedinstvenih oblika Poincaré dijagrama**
   - Implementacija u C++ uz biblioteku OpenCV.
   - Prijedlog daljeg razvoja kroz klasifikaciju izdvojenih kontura metodama mašinskog učenja.

## Metodologija

Algoritam opisan u radu obrađuje Poincaré dijagram kao sliku:

1. Dijagram se priprema tako da se uklone ose i mreža, a tačke se popune.
2. Slika se učitava u nijansama sive (`cv::imread` sa `cv::IMREAD_GRAYSCALE`).
3. Slika se pretvara u binarnu primjenom Otsuove metode praga (`cv::threshold`).
4. Primjenjuje se morfološka dilatacija s eliptičnim strukturnim elementom kako bi se razdvojene tačke spojile u cjelinu.
5. Konture se izdvajaju funkcijom `cv::findContours` i iscrtavaju funkcijom `cv::drawContours` na bijeloj podlozi.
6. Rezultat se snima na disk.

Algoritam ne daje samo vizuelni prikaz konture, nego i njen matematički opis (skup tačaka). Taj opis se može koristiti kao ulaz za dalju automatsku klasifikaciju dijagrama.

## Struktura repozitorija

| Datoteka | Opis |
|---|---|
| `BSS_Seminarski_Berina_Biberovic.pdf` | Seminarski rad s kompletnim izvornim kodom algoritma |

## Pokretanje koda iz rada

Izvorni kod algoritma nalazi se u samom radu. Za njegovo prevođenje potrebni su C++ kompajler s podrškom za C++11 ili noviji standard i instalirana biblioteka OpenCV 4. Na primjer:

```bash
g++ main.cpp -o konture $(pkg-config --cflags --libs opencv4)
./konture
```

Program očekuje ulaznu sliku `../19140.png` (pripremljeni Poincaré dijagram) i rezultat snima u `../rezultat_19140.png`.

## Autor

- **Student:** Berina Biberović
- **Predmetni profesor:** prof. dr Dušanka Bošković
- **Asistent:** Mr. dipl. ing. Amina Tihak
- **Ustanova:** Elektrotehnički fakultet, Univerzitet u Sarajevu
