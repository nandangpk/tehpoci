# Teh Poci
Menggunakan Laravel versi 9.19 dan PHP versi 8.0.2

## DAFTAR ISI
[DAFTAR ISI](https://github.com/nandangpk/tehpoci/blob/main/README.md#daftar-isi)

[CONTROLLER](https://github.com/nandangpk/tehpoci/blob/main/README.md#terdapat-5-controller)

[MODEL](https://github.com/nandangpk/tehpoci/edit/blob/README.md#terdapat-4-model)

[#1. MENU ORDER](https://github.com/nandangpk/tehpoci/blob/main/README.md#1-menu-order-ordercontroller)
* [ROUTING](https://github.com/nandangpk/tehpoci/blob/main/README.md#routing)
* [GET DATA DARI CONTROLLER + RETURN VIEW](https://github.com/nandangpk/tehpoci/blob/main/README.md#get-data-dari-controller--return-view-dengan-data)
* [MENAMPILKAN DATA ORDER DARI CONTROLLER PADA BLADE](https://github.com/nandangpk/tehpoci/blob/main/README.md#menampilkan-data-dari-controller)
* [MEMASUKKAN DATA ORDER](https://github.com/nandangpk/tehpoci/blob/main/README.md#menampilkan-data-dari-controller)

[#2. MENU DATA PENJUALAN](https://github.com/nandangpk/tehpoci/blob/main/README.md#2-menu-data-penjualan-datapenjualancontroller)
* [ROUTING](https://github.com/nandangpk/tehpoci/blob/main/README.md#routing-1)
* [GET DATA DARI CONTROLLER + RETURN VIEW](https://github.com/nandangpk/tehpoci/blob/main/README.md#get-data-dari-controller--return-view-dengan-data-1)
* [MENAMPILKAN DATA PENJUALAN DARI CONTROLLER PADA BLADE](https://github.com/nandangpk/tehpoci/blob/main/README.md#menampilkan-data-penjualan-dari-controller-pada-blade)
* [MENAMPILKAN DATA 'DETAIL' PENJUALAN DARI CONTROLLER PADA BLADE](https://github.com/nandangpk/tehpoci/blob/main/README.md#menampilkan-data-detail-penjualan-dari-controller-pada-blade)

[#3. MENU DATA BELANJA](https://github.com/nandangpk/tehpoci/blob/main/README.md#3-menu-data-belanja-databelanjacontroller)
* [ROUTING](https://github.com/nandangpk/tehpoci/blob/main/README.md#routing-2)
* [GET DATA DARI CONTROLLER + RETURN VIEW](https://github.com/nandangpk/tehpoci/blob/main/README.md#get-data-dari-controller--return-view-dengan-data-2)
* [MENAMPILKAN DATA BELANJA DARI CONTROLLER PADA BLADE](https://github.com/nandangpk/tehpoci/blob/main/README.md#menampilkan-data-belanja-dari-controller-pada-blade)

[#4. MENU KELOLA MINUMAN](https://github.com/nandangpk/tehpoci/blob/main/README.md#4-menu-kelolaminuman-minumancontroller)
* [ROUTING](https://github.com/nandangpk/tehpoci/blob/main/README.md#routing-3)
* [GET DATA DARI CONTROLLER + RETURN VIEW](https://github.com/nandangpk/tehpoci/blob/main/README.md#get-data-dari-controller--return-view-dengan-data-3)
* [MENAMPILKAN DATA MINUMAN DARI CONTROLLER PADA BLADE](https://github.com/nandangpk/tehpoci/blob/main/README.md#menampilkan-data-minuman-dari-controller-pada-blade)
* [TAMBAH DATA MINUMAN](https://github.com/nandangpk/tehpoci/blob/main/README.md#menambahkan-data-minuman)
* [EDIT DATA MINUMAN](https://github.com/nandangpk/tehpoci/blob/main/README.md#edit-data-minuman)
* [HAPUS DATA MINUMAN](https://github.com/nandangpk/tehpoci/blob/main/README.md#hapus-data-minuman)

[#5. MENU BELANJA](https://github.com/nandangpk/tehpoci/blob/main/README.md#4-menu-belanja-minuman-belanjaminumancontroller)
* [ROUTING](https://github.com/nandangpk/tehpoci/blob/main/README.md#routing-4)
* [GET DATA DARI CONTROLLER + RETURN VIEW](https://github.com/nandangpk/tehpoci/blob/main/README.md#get-data-dari-controller--return-view-dengan-data-4)
* [MENAMPILKAN DATA MINUMAN DARI CONTROLLER PADA BLADE](https://github.com/nandangpk/tehpoci/blob/main/README.md#menampilkan-data-minuman-dari-controller-pada-blade)
* [EKSEKUSI BELANJA](https://github.com/nandangpk/tehpoci/blob/main/README.md#eksekusi-belanja-minuman)

##### Terdapat 5 Controller:
1. OrderController
    - route: /order
    - berinteraksi dengan 3 Model (Minuman, Order, OrderDetail)

2. DataPenjualanController
    - route: /data-penjualan
    - berinteraksi dengan 2 Model (Order, OrderDetail)
 
3. DataBelanjaController
    - route: /data-belanja
    - berinteraksi dengan 1 Model (Belanja)
 
4. MinumanController
    - route: /minuman
    - berinteraksi dengan 1 Model (Minuman)
    
5. BelanjaMinumanController
    - route: /belanja
    - berinteraksi dengan 2 Model (Minuman, Belanja)
		
---------------------

##### Terdapat 4 Model:
1. Minuman

    |name|type|
    |---|---|
    |idMinuman (PK)|int|
    |varian|varchar(32)|
    |modal|int|
    |harga|int|
    |stok|int|


2. Belanja

    |name|type|
    |---|---|
    |idBelanja (PK)|int|
    |varian|varchar(32)|
    |tanggalBelanja|date|
    |kuantitas|int|
    |totalBelanja|int|
 
3. Order

    |name|type|
    |---|---|
    |idOrder (PK)|int|
    |tanggalOrder|date|
    |totalOrder|int|

4. OrderDetail

    |name|type|
    |---|---|
    |idOrder|int|
    |varian|varchar(32)|
    |kuantitas|int|

---------------------

## #1 Menu Order (OrderController)

---------------------
##### ROUTING
app\routes\web.php
```php
...
Route::resource('order', OrderController::class);
...
```
melakukan routing pada agar bisa di akses melalui /order

##### GET DATA DARI CONTROLLER + RETURN VIEW DENGAN DATA
app\Http\Controller\OrderController.php
```php
...
public function index()
{
  $minuman = Minuman::All();
  return view('order.index', ['minuman' => $minuman]);
}
...
```

mengambil seluruh data Minuman pada function index OrderController sekaligus me-return view beserta data-nya ($minuman)

---------------------
##### MENAMPILKAN DATA DARI CONTROLLER
app\resources\views\order\index.blade.php
```html
...
<form action="{{route('order.store')}}" method="POST">
  @csrf
  <table class="table">
    <tr>
      <th>Varian</th>
      <th>Harga</th>
      <th style="width: 200px">Qty</th>
    </tr>
    @foreach($minuman as $min)
    <tr>
      <td>{{$min->varian}}</td>
      <td><input readonly="true" type="number" class="form-control border-0 bg-light" name="harga[]" value="{{$min->harga}}"></td>
      <td>
        <input class="form-control" min="0" type="number" name="kuantitas[]" id="" required>
        <input type="hidden" value="{{$min->varian}}" name="varian[]">
      </td>
    </tr>
    @endforeach
  </table>
  <input type="submit" class="btn btn-primary w-100" value="Order">
</form>
...
```

menampilkan data yang di passing dari Controller ($minuman) dengan menggunakan _@foreach_ sekaligus membuat form order yang akan di handle pada function store OrderController 

>pada setiap _name_ input diberikan '[]' karena jenis minumannya lebih dari satu dengan hanya 1 tipe form (akan di handle secara array)

---------------------

##### MEMASUKKAN DATA ORDER
app\Http\Controller\OrderController.php
```php
...
public function store(Request $request)
{
  $counter = count($request->get('varian'));

  $totalOrder = 0;
  for($i = 0; $i < $counter; $i++){
    $totalOrder += ($request->get('harga')[$i] * $request->get('kuantitas')[$i]);
  }

  $order = new Order;
  $order->tanggalOrder = Carbon::now()->toDateString();
  $order->totalOrder = $totalOrder;
  $order->save();

  $idOrder = Order::max('idOrder');
  for($i = 0; $i < $counter; $i++){
    if($request->get('kuantitas')[$i] > 0){
      $orderDetail = new OrderDetail;
      $orderDetail->idOrder = $idOrder;
      $orderDetail->kuantitas = $request->get('kuantitas')[$i];
      $orderDetail->varian = $request->get('varian')[$i];
      $orderDetail->save();
    }
  }
  return redirect()->route('order.index');
}
...
```

mengambil, mengolah serta menyimpan data yang dikirim oleh form pada _app\resources\views\order\index.blade.php_

---------------------

## #2 Menu Data Penjualan (DataPenjualanController)

---------------------

##### ROUTING
app\routes\web.php
```php
...
Route::resource('data-penjualan', DataPenjualanController::class);
...
```
melakukan routing pada agar bisa di akses melalui /data-penjualan

---------------------

##### GET DATA DARI CONTROLLER + RETURN VIEW DENGAN DATA
app\Http\Controller\DataPenjualanController.php
```php
...
public function index(Request $request)
{
  if ($request->get('dari') == '' && $request->get('sampai') == '') {
    $order = Order::All();
    return view('data-penjualan.index', ["order" => $order]);
  }else{
    $dari = $request->get('dari');
    $sampai = $request->get('sampai');
    $order = Order::whereBetween('tanggalOrder', [$dari, $sampai])->get();
    return view('data-penjualan.index', ["order" => $order]);
  }
}
...
```
```
route: /data-penjualan
target: data-penjualan/index.blade.php
```

mengambil seluruh / sebagian (tergantung pada request, defaultnya mengambil seluruh) data penjualan pada function index DataPenjualanController sekaligus me-return view beserta data-nya ($order)
> CATATAN: melakukan pengecekan terlebih dahulu, jika tidak terdapat request parameter 'dari' dan 'sampai' maka akan mengambil semua data penjualan

---------------------

app\Http\Controller\DataPenjualanController.php
```php
...
public function show($idOrder)
{
  $orderDetail = OrderDetail::where("idOrder", $idOrder)->get();
  return view('data-penjualan.detail', ["idOrder" => $idOrder, "orderDetail" => $orderDetail]);
}
...
```
```
route: /data-penjualan/{$id}
target: data-penjualan/detail.blade.php
```

mengambil seluruh data dari OrderDetail berdasarkan idOrder sekaligus me-return view beserta datanya ($orderDetail, $idOrder)

---------------------

##### MENAMPILKAN DATA PENJUALAN DARI CONTROLLER PADA BLADE
app\resources\views\data-penjualan\index.blade.php
```html
...

<form action="{{route('data-penjualan.index')}}" method="GET">
  <table class="table table-borderless">
    <tr>
      <td>Dari</td>
      <td class="w-100"><input type="date" name="dari" required></td>
    </tr>
    <tr>
      <td>Sampai</td>
      <td class="w-100"><input type="date" name="sampai" required></td>
    </tr>
    <tr>
      <td>
        <a href="/data-belanja">
          <button type="button" class="btn btn-danger">Reset</button>
        </a>
      </td>
      <td>
        <button type="submit" class="btn btn-primary">Cari</button>
      </td>
    </tr>
  </table>
</form>
<table class="table">
  <tr>
    <th>Tanggal</th>
    <th>No. Order</th>
    <th>Total Order</th>
    <th>Aksi</th>
  </tr>
  @php $total = 0 @endphp
  @foreach ($order as $orderr)
  @php $total = $total + $orderr->totalOrder @endphp
  <tr>
    <td>{{$orderr->tanggalOrder}}</td>
    <td>{{$orderr->idOrder}}</td>
    <td>{{$orderr->totalOrder}}</td>
    <td>
      <a href="{{ route('data-penjualan.show', [$orderr->idOrder]) }}">
        <button type="button" class="btn btn-sm btn-primary">Lihat Detail</button>
      </a>
    </td>
  </tr>
  @endforeach
  <tr>
    <td colspan="3" class="text-end"><b>Total (Rp.)</b></td>
    <td><b>{{$total}}</b></td>
  </tr>
</table>
...
```
menampilkan data yang di passing dari Controller ($order) dengan menggunakan _@foreach_ sekaligus membuat clickable button yang akan me-redirect ke '/data-penjualan/{$id}' (halaman detail data penjualan) yang di handle pada function show DataPenjualanController juga menghitung total belanja menggunakan variabel $total yang di looping didalam _@foreach_

juga terdapat form untuk menampilkan data berdasarkan tanggal yang dipilih ('dari' dan 'sammpai')

---------------------

##### MENAMPILKAN DATA DETAIL PENJUALAN DARI CONTROLLER PADA BLADE
app\resources\views\data-penjualan\detail.blade.php
```html
...
<h5 class="text-center mb-0">ID Order : {{$idOrder}}</h5>
<hr>

<table class="table">
  <tr>
    <th>Varian</th>
    <th>Kuantitas</th>
  </tr>
  @foreach ($orderDetail as $od)
  <tr>
    <td>{{$od->varian}}</td>
    <td>{{$od->kuantitas}}</td>
  </tr>
  @endforeach
</table>

<a href="{{ route('data-penjualan.index') }}">
  <button type="button" class="btn w-100 btn-secondary">< Kembali</button>
</a>
...
```
menampilkan data yang di passing dari Controller ($idOrder, $orderDetail) dengan menggunakan _@foreach_ untuk $orderDetail, juga terdapat button untuk kembali ke menu utama data penjualan 

---------------------

## #3 Menu Data Belanja (DataBelanjaController)

---------------------

##### ROUTING
app\routes\web.php
```php
...
Route::resource('data-belanja', DataBelanjaController::class);
...
```
melakukan routing pada agar bisa di akses melalui /data-belanja

---------------------

##### GET DATA DARI CONTROLLER + RETURN VIEW DENGAN DATA
app\Http\Controller\DataBelanjaController.php
```php
...
public function index(Request $request)
{
  if ($request->get('dari') == '' && $request->get('sampai') == '') {
    $belanja = Belanja::All();
    return view( 'data-belanja.index', ['belanja' => $belanja]);
  }else{
    $dari = $request->get('dari');
    $sampai = $request->get('sampai');
    $belanja = Belanja::whereBetween('tanggalBelanja', [$dari, $sampai])->get();
    return view( 'data-belanja.index', ['belanja' => $belanja]);
  }
}
...
```
```
route: /data-belanja
target: data-belanja/index.blade.php
```

mengambil seluruh / sebagian (tergantung pada request, defaultnya mengambil seluruh) data belanja pada function index DataBelanjaController sekaligus me-return view beserta data-nya ($belanja)
> CATATAN: melakukan pengecekan terlebih dahulu, jika tidak terdapat request parameter 'dari' dan 'sampai' maka akan mengambil semua data belanja

---------------------

##### MENAMPILKAN DATA BELANJA DARI CONTROLLER PADA BLADE
app\resources\views\data-penjualan\index.blade.php
```html
...

<form action="{{route('data-belanja.index')}}" method="GET">
  <table class="table table-borderless">
    <tr>
      <td>Dari</td>
      <td class="w-100"><input type="date" name="dari" required></td>
    </tr>
    <tr>
      <td>Sampai</td>
      <td class="w-100"><input type="date" name="sampai" required></td>
    </tr>
    <tr>
      <td>
        <a href="/data-belanja">
          <button type="button" class="btn btn-danger">Reset</button>
        </a>
      </td>
      <td>
        <button type="submit" class="btn btn-primary">Cari</button>
      </td>
    </tr>
  </table>
</form>
<table class="table">
  <tr>
    <th>Tanggal Belanja</th>
    <th>Varian</th>
    <th>Kuantitas</th>
    <th>Rp.</th>
  </tr>
    @php $total = 0 @endphp
    @foreach ($belanja as $blj)
    @php $total = $total + $blj->totalBelanja @endphp
  <tr>
    <td>{{$blj->tanggalBelanja}}</td>
    <td>{{$blj->varian}}</td>
    <td>{{$blj->kuantitas}}</td>
    <td>{{$blj->totalBelanja}}</td>
  </tr>
  @endforeach
  <tr>
    <td colspan="3" class="text-end"><b>Total (Rp.)</b></td>
    <td><b>{{$total}}</b></td>
  </tr>
</table>
...
```
menampilkan data yang di passing dari Controller ($belanja) dengan menggunakan _@foreach_, menghitung total belanja menggunakan variabel $total yang di looping didalam _@foreach_

juga terdapat form untuk menampilkan data berdasarkan tanggal yang dipilih ('dari' dan 'sammpai')

---------------------

## #4 Menu KelolaMinuman (MinumanController)

---------------------

##### ROUTING
app\routes\web.php
```php
...
Route::resource('minuman', MinumanController::class);
Route::get('/minuman/hapus/{idMinuman}', 'App\Http\Controllers\MinumanController@destroy');
...
```
melakukan routing pada agar bisa di akses melalui /minuman

---------------------

##### GET DATA DARI CONTROLLER + RETURN VIEW DENGAN DATA
app\Http\Controller\MinumanController.php
```php
...
public function index()
{
  $minuman = Minuman::All();
  return view( 'minuman.index', ['minuman' => $minuman]);
}
...
```
```
route: /minuman
target: minuman/index.blade.php
```

mengambil seluruh data minuman pada function index MinumanController sekaligus me-return view beserta data-nya ($minuman)

---------------------

##### MENAMPILKAN DATA MINUMAN DARI CONTROLLER PADA BLADE
app\resources\views\minuman\index.blade.php
```html
...
<figure class="text-end">
  <a href="{{route('minuman.create')}}">
    <button type="button" class="btn btn-sm btn-primary" id="btn-tambah-minuman">Tambah Minuman</button>
  </a>
</figure>
<table class="table mt-3">
  <tr class="text-start">
    <th>Varian</th>
    <th>Modal</th>
    <th>Harga</th>
    <th>Stok</th>
    <th>Aksi</th>
  </tr>
  @foreach ($minuman as $min)
  <tr>
    <td>{{$min->varian}}</td>
    <td>{{$min->modal}}</td>
    <td>{{$min->harga}}</td>
    <td>{{$min->stok}}</td>
    <td>
      <a href="{{ route('minuman.edit', [$min->idMinuman]) }}">
        <button type="button" class="btn btn-sm btn-success">Edit</button>
      </a>
      <a href="/minuman/hapus/{{ $min->idMinuman }}" onclick="return confirm('Yakin Ingin menghapus data?')">
        <button type="button" class="btn btn-sm btn-danger">Hapus</button>
      </a>
    </td>
  </tr>
  @endforeach
</table>
...
```
menampilkan data yang di passing dari Controller ($minuman) dengan menggunakan _@foreach_, sekaligus membuat clickable button edit dan hapus yang dibuat didalam _@foreach_ yang akan me-redirect ke '/minuman/{$idMinuman}' (button edit -> halaman edit minuman) yang di handle pada function edit MinumanController dan button hapus berfungsi untuk menghapus minuman yang akan me-redirect ke (/minuman/hapus/{$idMinuman}) yang di handle pada function destroy MinumanController.

terdapat button di atas untuk menuju ke '/minuman/create' (halaman tambah minuman) yang akan di handle pada function create MinumanController. 

---------------------

##### MENAMBAHKAN DATA MINUMAN
app\Http\Controller\MinumanController.php
```php
...
public function create()
{
  return view('minuman.tambah');
}
...
```

```
route: /minuman/create
target: minuman/tambah.blade.php
```

app\resources\views\minuman\tambah.blade.php

```html
...
<form action="{{route('minuman.store')}}" method="post">
@csrf
  <div class="form-floating mb-3">
    <input type="text" class="form-control" id="varian" name="varian" required>
    <label for="varian">Varian</label>
  </div>
  <div class="form-floating mb-3">
    <input type="number" class="form-control" id="modal" name="modal" required>
    <label for="harga">Modal</label>
  </div>
  <div class="form-floating mb-3">
    <input type="number" class="form-control" id="harga" name="harga" required>
    <label for="harga">Harga</label>
  </div>
  <div class="form-floating mb-3">
    <input type="number" class="form-control" id="stok" name="stok" required>
    <label for="stok">Stok</label>
  </div>
  <input type="submit" class="btn btn-primary w-100" value="Tambah Minuman">
</form>
...
```

terdapat form untuk membuat data minuman (varian, modal, harga, stok) dengan method POST yang akan di handle pada function store MinumanController (disertakan dibawah)

app\Http\Controller\MinumanController.php
```php
...
public function store(Request $request)
{
  $minuman = new Minuman;

  $minuman->varian    = $request->get('varian');
  $minuman->modal    = $request->get('modal');
  $minuman->harga     = $request->get('harga');
  $minuman->stok      = $request->get('stok');
  $minuman->save();

  return redirect()->route('minuman.index');
}
...
```

---------------------

##### EDIT DATA MINUMAN
app\Http\Controller\MinumanController.php
```php
...
public function edit($id)
{
  $minuman = Minuman::findOrFail($id);
  return view( 'minuman.edit', ['minuman' => $minuman]);
}
...
```

```
route: /minuman/edit/{$idMinuman}
target: minuman/edit.blade.php
note: mencari data minuman berdasarkan idMinuman, kemudian di return dengan view 'minuman.edit' beserta data-nya ($minuman)
```

app\resources\views\minuman\edit.blade.php

```html
...
<form enctype="multipart/form-data" action="{{route('minuman.update', [$minuman->idMinuman])}}" method="post">
  @csrf
  <input type="hidden" value="PUT" name="_method">
  <div class="form-floating mb-3">
    <input type="text" class="form-control" id="varian" name="varian" value="{{$minuman->varian}}" required>
    <label for="varian">Varian</label>
  </div>
  <div class="form-floating mb-3">
    <input type="number" class="form-control" id="modal" name="modal" value="{{$minuman->modal}}" required>
    <label for="harga">Modal</label>
  </div>
  <div class="form-floating mb-3">
    <input type="number" class="form-control" id="harga" name="harga" value="{{$minuman->harga}}" required>
    <label for="harga">Harga</label>
  </div>
  <div class="form-floating mb-3">
    <input type="number" class="form-control" id="stok" name="stok" value="{{$minuman->stok}}" required>
    <label for="stok">Stok</label>
    </div>
  <input type="submit" class="btn btn-primary w-100" value="Edit data">
</form>
...
```
data yang di return dari function edit MinumanController kemudian dimasukkan kedalam value masing-masing form

terdapat form untuk merubah data minuman (varian, modal, harga, stok) dengan method POST yang akan di handle pada function update MinumanController (disertakan dibawah)

app\Http\Controller\MinumanController.php
```php
...
public function update(Request $request, $idMinuman)
{
  $minuman = Minuman::findOrFail($idMinuman);

    $minuman->varian    = $request->get('varian');
    $minuman->modal    = $request->get('modal');
    $minuman->harga     = $request->get('harga');
    $minuman->stok      = $request->get('stok');
    $minuman->save();

    return redirect()->route('minuman.index');
}
...
```

---------------------

##### HAPUS DATA MINUMAN
app\Http\Controller\MinumanController.php
```php
...
public function destroy($idMinuman)
{
  $minuman = Minuman::findOrFail($idMinuman);
  $minuman->delete();
  return redirect()->route('minuman.index');
}
...
```

```
route: /minuman/hapus/{$idMinuman}
redirect-to: /minuman
note: mencari data minuman berdasarkan idMinuman, jika ditemukan maka data minuman akan dihapus menggunakan method delete(), kemudian akan me-redirect kembali ke halaman '/minuman' (index)
```
---------------------

## #5 Menu Belanja Minuman (BelanjaMinumanController)

---------------------

##### ROUTING
app\routes\web.php
```php
...
Route::resource('belanja', BelanjaMinumanController::class);
...
```
melakukan routing pada agar bisa di akses melalui /belanja

---------------------

##### GET DATA DARI CONTROLLER + RETURN VIEW DENGAN DATA
app\Http\Controller\BelanjaMinumanController.php
```php
...
public function index()
{
  $minuman = Minuman::All();
  return view( 'belanja.index', ['minuman' => $minuman]);
}
...
```
```
route: /belanja
target: belanja/index.blade.php
```

mengambil seluruh data minuman pada function index BelanjaMinumanController sekaligus me-return view beserta data-nya ($minuman)

---------------------

##### MENAMPILKAN DATA MINUMAN DARI CONTROLLER PADA BLADE
app\resources\views\belanja\index.blade.php
```html
...
<table class="table mt-3">
  <tr class="text-start">
    <th>Varian</th>
    <th>Modal</th>
    <th>Harga</th>
    <th>Stok</th>
    <th>Aksi</th>
  </tr>
  @foreach ($minuman as $min)
  <tr>
    <td>{{$min->varian}}</td>
    <td>{{$min->modal}}</td>
    <td>{{$min->harga}}</td>
    <td>{{$min->stok}}</td>
    <td>
      <a href="{{ route('belanja.show', [$min->idMinuman]) }}">
        <button type="button" class="btn btn-sm btn-primary">Belanja</button>
      </a>
    </td>
  </tr>
  @endforeach
</table>
...
```
menampilkan data yang di passing dari Controller ($minuman) dengan menggunakan _@foreach_, sekaligus membuat clickable button belanja yang dibuat didalam _@foreach_ yang akan me-redirect ke '/belanja/{$idMinuman}' yang di handle pada function show BelanjaMinumanController.

---------------------

##### EKSEKUSI BELANJA MINUMAN
app\Http\Controller\BelanjaMinumanController.php
```php
...
public function show($idMinuman)
{
  $minuman = Minuman::findOrFail($idMinuman);
  return view( 'belanja.belanja', ['minuman' => $minuman]);
}
...
```

```
route: /belanja/{$idMinuman}
target: belanja/belanja.blade.php
note: mencari data minuman berdasarkan idMinuman, kemudian di return dengan view 'belanja.belanja' beserta data-nya ($minuman)
```

app\resources\views\belanja\belanja.blade.php
```html
...
<h3 class="text-center mb-0">Belanja {{ $minuman-> varian }}</h3>

<table class="table mt-3">
  <tr>
    <th>Modal</th>
    <th>Harga</th>
    <th>Stok</th>
  </tr>
  <tr>
    <td>{{$minuman->modal}}</td>
    <td>{{$minuman->harga}}</td>
    <td>{{$minuman->stok}}</td>
  </tr>
</table>

<form enctype="multipart/form-data" action="{{route('belanja.update', [$minuman->idMinuman])}}" method="post">
  @csrf
  <input type="hidden" value="PUT" name="_method">
  <input type="hidden" name="varian" value="{{ $minuman-> varian }}" required>
  <input type="hidden" name="modal" value="{{ $minuman-> modal }}" required>
  <div class="form-floating mb-3">
    <input type="number" class="form-control" name="kuantitas" min="1" required>
    <label>Jumlah Belanja Stok {{ $minuman-> varian }}</label>
  </div>
  <input type="submit" class="btn btn-primary w-100" value="Konfirmasi Belanja">
</form>
...
```
data yang di return dari function show BelanjaMinumanController kemudian dimasukkan kedalam value masing-masing form

terdapat 1 form input untuk menambah stok (belanja) dengan method PUT yang akan di handle pada function update BelanjaMinumanController (disertakan dibawah)
app\Http\Controller\BelanjaMinumanController.php
```php
...
public function update(Request $request, $idMinuman)
{
  $minuman = Minuman::findOrFail($idMinuman);
  $minuman->stok      = $minuman->stok + $request->get('kuantitas');
  $minuman->save();
        
  $belanja = new Belanja;
  $belanja->varian            = $request->get('varian');
  $belanja->tanggalBelanja    = Carbon::now()->toDateString();
  $belanja->kuantitas         = $request->get('kuantitas');
  $belanja->totalBelanja      = $request->get('kuantitas') * $request->get('modal');
  $belanja->save();
  return redirect()->route('belanja.index');
}
...
```
```
route: /belanja/{$idMinuman}
redirect-to: /belanja
note: menambahkan stok berdasarkan input form (stok awal + belanja), kemudian menambahkan data belanja yang di akhiri dengan me-redirect ke halaman belanja
```
