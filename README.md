# TheNextCar
Merupakan aplikasi dashboard electric car yang memiliki konsep MVC (Model View Controller).

MVC sendiri berfungsi untuk 
1. Model berfungsi untuk mengatur data, fungsi, dan aturan dari aplikasi
2. View berfungsi untuk mengatur tampilan/output yang tampil di layar
3. Controller berfungsi untuk mengatur / meneruma input dan mmenjalankan beberapa perintah untuk dijalankan.

## Scope & Functionalities
- User dapat menyalakan tombol power ON/OFF pada tampilan aplikasi
- User dapat membuka / menutup pintu(door)
- User dapat mengkunci / membuka security lock pada car
- User dapat menjalankan mesin ketika semuanya sudah benar/ready
- Memiliki keamanan berkendara karena terdapat pemberitahuan jika ada pintu atau mesin yang belum menyala

## How Does it Works ?
Diawali dengan method MainWindowpada class MainWindow.xaml.cs
```csharp

     public MainWindow()
        {
            InitializeComponent();
            AccubatteryController accubatteryController = new AccubatteryController(this);
            DoorController doorController = new DoorController(this);
            nextCar = new Car(doorController, accubatteryController, this);
        }
```

Cara kerjanya Mobil/Car hanya dapat menyala jika kita sudah menutup pintu , mengunci pintu, dan menyalakan tombol ON
maka secara otomatis akan bisa dihidupkan startengine nya

```csharp
 public void startEngine()
        {
            if (!doorIsClosed())
            {
                this.callback.onCarEngineStateChanged("STOPED", "Close the door");
                return;
            }
            if (!doorIsLocked())
            {
                this.callback.onCarEngineStateChanged("STOPED", "Lock th door");
                return;
            }
