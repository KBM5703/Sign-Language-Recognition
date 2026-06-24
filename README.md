# Sign Language Recognition

Project nhan dien chu cai ngon ngu ky hieu ASL (American Sign Language) qua camera. Ung dung dung MediaPipe Hands de trich xuat 21 diem landmark cua ban tay, dua 63 dac trung `(x, y, z)` vao model Keras da train va hien thi chu cai du doan truc tiep tren khung hinh webcam.

## Tinh nang

- Nhan dien 26 chu cai ASL tu `A` den `Z`.
- Chay real-time bang webcam trong `main.py`.
- Su dung model da train san: `sign_language_model.keras`.
- Co notebook `SLDetection.ipynb` de train/fine-tune lai model tu dataset anh.
- Dataset gom cac tap `train`, `test`, `valid`, moi lop duoc tach theo thu muc chu cai.

## Cau truc thu muc

```text
.
|-- main.py                         # Chuong trinh nhan dien qua webcam
|-- sign_language_model.keras       # Model Keras da train
|-- SLDetection.ipynb               # Notebook train/fine-tune model
|-- dataset/
|   |-- train/                      # Du lieu train theo tung lop A-Z
|   |-- test/                       # Du lieu test theo tung lop A-Z
|   |-- valid/                      # Du lieu validation theo tung lop A-Z
|   |-- accuracy_plot.png           # Bieu do accuracy sau train
|   |-- loss_plot.png               # Bieu do loss sau train
|   `-- README.roboflow.txt         # Thong tin dataset tu Roboflow
`-- README.md
```

## Yeu cau moi truong

- Python 3.10 hoac 3.11.
- Webcam hoat dong va duoc cap quyen truy cap.
- Nen dung virtual environment de tranh xung dot dependency.

Thu vien can cai:

```bash
pip install mediapipe==0.10.9 opencv-python numpy scikit-learn tensorflow matplotlib
```

Neu may ban dung Python 3.12 va cai `mediapipe` bi loi, hay tao moi truong Python 3.10/3.11 vi MediaPipe thuong ho tro on dinh hon tren cac phien ban nay.

## Cai dat

1. Mo terminal tai thu muc project:

```bash
cd Sign-Language-Recognition-main
```

Neu ban dang o thu muc cha vua giai nen, duong dan co the la:

```bash
cd Sign-Language-Recognition-main/Sign-Language-Recognition-main
```

2. Tao va kich hoat moi truong ao.

Tren Windows PowerShell:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

Tren macOS/Linux:

```bash
python -m venv .venv
source .venv/bin/activate
```

3. Cai dependencies:

```bash
python -m pip install --upgrade pip
pip install mediapipe==0.10.9 opencv-python numpy scikit-learn tensorflow matplotlib
```

## Chay nhan dien qua camera

Dam bao file `sign_language_model.keras` nam cung thu muc voi `main.py`, sau do chay:

```bash
python main.py
```

Khi cua so camera hien len:

- Dua ban tay vao khung hinh.
- Giu tay ro, du anh sang va nen it roi.
- Ket qua du doan se hien bang chu cai mau xanh tren man hinh.
- Nhan phim `q` de thoat chuong trinh.

## Train hoac fine-tune lai model

File `SLDetection.ipynb` chua pipeline train model:

1. Cai cac thu vien can thiet.
2. Doc anh trong `dataset/train` va `dataset/test`.
3. Dung MediaPipe Hands de trich xuat 63 keypoint tu moi anh.
4. Ma hoa label A-Z bang `LabelEncoder`.
5. Train mang neural network gom cac lop Dense/Dropout.
6. Luu model thanh `sign_language_model.keras`.

Cach thuc hien:

```bash
jupyter notebook SLDetection.ipynb
```

Hoac mo notebook bang Google Colab/JupyterLab va chay lan luot cac cell. Neu train tren may local, can sua cac duong dan dang `/content/dataset/train` trong notebook thanh duong dan local, vi `/content/...` la duong dan cua Google Colab.

Vi du khi train local:

```python
train_dir = 'dataset/train'
test_dir = 'dataset/test'
```

Sau khi train xong, notebook se luu model:

```python
model.save('sign_language_model.keras')
```

Copy/giu file model moi trong cung thu muc voi `main.py`, roi chay lai:

```bash
python main.py
```

## Dataset

Dataset trong project la bo American Sign Language Letters duoc export tu Roboflow, gom 26 lop tu `A` den `Z`. Anh da duoc resize ve `416x416` va co augmentation nhu flip, crop, rotate, shear, brightness va blur.

Cau truc label:

```text
dataset/train/A
dataset/train/B
...
dataset/train/Z
```

Ten thu muc con duoc dung truc tiep lam nhan lop khi train model.

## Luu y khi nhan dien

- Model hien tai nhan dien tung chu cai tinh, khong phai cau/tu dong theo chuoi thoi gian.
- Cac chu co chuyen dong trong ASL nhu `J` va `Z` co the kho nhan dien hon neu chi dung mot khung hinh.
- Ket qua phu thuoc vao anh sang, goc camera, khoang cach ban tay va do giong voi du lieu train.
- Neu muon nhan dien nhieu nguoi/nhieu tay, can sua `max_num_hands` trong `main.py`.

## Xu ly loi thuong gap

### Khong mo duoc camera

- Kiem tra webcam co dang bi ung dung khac su dung khong.
- Kiem tra quyen camera cua he dieu hanh.
- Neu co nhieu camera, doi index trong `main.py`:

```python
cap = cv2.VideoCapture(0)
```

thanh:

```python
cap = cv2.VideoCapture(1)
```

### Loi khong tim thay model

Dam bao file `sign_language_model.keras` nam cung thu muc voi `main.py` va ban dang chay lenh tu dung thu muc project.

### Loi cai MediaPipe

Dung Python 3.10 hoac 3.11, sau do cai lai:

```bash
pip install mediapipe==0.10.9
```

### Cua so camera bi dung hoac khong hien

Hay chay project tu terminal local thay vi mot moi truong khong ho tro GUI. `cv2.imshow()` can moi truong desktop de hien cua so camera.

## Tac gia

BTL_ML-APP_HK242_NHOM7
