# Traffic Sign Detection

Projekt për detektimin dhe klasifikimin e shenjave të trafikut duke përdorur datasuetin **GTSRB** (German Traffic Sign Recognition Benchmark). Notebook-u implementon dhe krahason metoda tradicionale të Machine Learning si dhe arkitektura CNN.

## Struktura e Projektit

```
traffic-sign-detection-ipynb/
├── data_preprocessing.ipynb   # Notebook kryesor
├── requirements.txt           # Bibliotekat e nevojshme
├── saved_models/              # Modelet e ruajtura pas trajnimit
└── traffic_sign/              # Dataseti
    ├── Train.csv
    ├── Test.csv
    ├── Meta.csv
    ├── Meta/                  # Imazhet e meta-të shenjave
    └── Test/                  # Imazhet e testimit
```

## Çfarë Bën Ky Projekt

1. **Para-procesimi i të dhënave** — ngarkon dhe analizon CSV-të, vizualizon shpërndarjen e klasave
2. **Ngarkimi i imazheve** — ndryshohen në madhësi 32×32 piksel dhe normalizohen
3. **Reduktimi i dimensionalitetit** — PCA me 100 komponente
4. **Klasifikuesit tradicionalë** — KNN, Random Forest, Logistic Regression, LinearSVC
5. **Rrjetet CNN** — dy arkitektura të ndryshme me Keras/TensorFlow
6. **Vlerësimi** — krahasim me F1-score, confusion matrix
7. **Grupimi (Clustering)** — KMeans mbi veçoritë e imazheve
8. **Ruajtja e modelit** — modeli më i mirë ruhet në `saved_models/`

## Kërkesat e Sistemit

- Python 3.8 ose më i ri
- pip

## Konfigurimi dhe Ekzekutimi

### 1. Klono ose shkarko projektin

```bash
git clone https://github.com/RijonZ/traffic-sign-detection-ipynb.git
cd traffic-sign-detection-ipynb
```

### 2. Krijo dhe aktivizo një mjedis virtual (opsionale por i rekomanduar)

```bash
python -m venv venv

# Windows
venv\Scripts\activate

# macOS / Linux
source venv/bin/activate
```

### 3. Instalo bibliotekat

```bash
pip install -r requirements.txt
```

### 4. Sigurohu që dataseti është i vendosur

Vendose dosjen `traffic_sign/` në rrënjë të projektit me këtë strukturë:

```
traffic_sign/
├── Train.csv
├── Test.csv
├── Meta.csv
├── Meta/        (imazhet meta të shenjave)
└── Test/        (imazhet e testimit)
```

### 5. Nis Jupyter Notebook

```bash
jupyter notebook
```

Hap `data_preprocessing.ipynb` dhe ekzekuto qelizat sipas radhës (**Kernel → Restart & Run All** ose `Shift+Enter` qelizë nga qeliza).

## Variablat Kryesore të Konfigurimit

Brenda notebook-ut, në fillim të ekzekutimit, mund të ndryshosh:

| Variabla | Vlera Default | Përshkrim |
|---|---|---|
| `IMG_SIZE` | `32` | Madhësia e imazheve (piksel) |
| `USE_SUBSET` | `True` | Përdor nëndataset më të vogël për shpejtësi |
| `RANDOM_STATE` | `42` | Seed për riprodhueshmëri |

Nëse `USE_SUBSET = False`, modelet trajnohen mbi të gjithë datasetin (trajnim më i gjatë).

## Rezultatet

Modelet krahasohen sipas F1-score. Modeli me performancën më të lartë ruhet automatikisht si:

- `saved_models/best_traffic_sign_model.keras` (CNN)
- `saved_models/*.pkl` (klasifikuesit tradicionalë me joblib)

## Kërkesat e Harduerit

Modelet CNN mund të trajnohen edhe pa GPU. Me GPU (CUDA), TensorFlow e shfrytëzon automatikisht për trajnim më të shpejtë.
