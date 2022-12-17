# Teh Poci
Menggunakan Laravel versi 9.19 dan PHP versi 8.0.2

## DAFTAR ISI
[DAFTAR ISI](https://github.com/nandangpk/tehpoci/edit/main/README.md#daftar-isi)

[CONTROLLER](https://github.com/nandangpk/tehpoci/edit/main/README.md#terdapat-5-controller)

[MODEL](https://github.com/nandangpk/tehpoci/edit/main/README.md#terdapat-4-model)

[#1. MENU ORDER](https://github.com/nandangpk/tehpoci/blob/main/README.md#1-menu-order-ordercontroller)
* [ROUTING](https://github.com/nandangpk/tehpoci/edit/main/README.md#routing)
* [GET DATA DARI CONTROLLER + RETURN VIEW](https://github.com/nandangpk/tehpoci/edit/main/README.md#get-data-dari-controller--return-view-dengan-data)
* [MENAMPILKAN DATA ORDER DARI CONTROLLER PADA BLADE](https://github.com/nandangpk/tehpoci/edit/main/README.md#menampilkan-data-dari-controller)
* [MEMASUKKAN DATA ORDER](https://github.com/nandangpk/tehpoci/edit/main/README.md#menampilkan-data-dari-controller)

[#2. MENU DATA PENJUALAN](https://github.com/nandangpk/tehpoci/edit/main/README.md#2-menu-data-penjualan-datapenjualancontroller)
* [ROUTING](https://github.com/nandangpk/tehpoci/edit/main/README.md#routing-1)
* [GET DATA DARI CONTROLLER + RETURN VIEW](https://github.com/nandangpk/tehpoci/edit/main/README.md#get-data-dari-controller--return-view-dengan-data-1)
* [MENAMPILKAN DATA PENJUALAN DARI CONTROLLER PADA BLADE](https://github.com/nandangpk/tehpoci/edit/main/README.md#menampilkan-data-penjualan-dari-controller-pada-blade)
* [MENAMPILKAN DATA 'DETAIL' PENJUALAN DARI CONTROLLER PADA BLADE](https://github.com/nandangpk/tehpoci/edit/main/README.md#menampilkan-data-detail-penjualan-dari-controller-pada-blade)

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
> http://127.0.0.1:8000/order

![image](https://user-images.githubusercontent.com/54816942/208220021-a85171f9-fb51-4881-86ab-cd843f7209bd.png)
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
  @foreach ($order as $orderr)
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
</table>
...
```
menampilkan data yang di passing dari Controller ($order) dengan menggunakan _@foreach_ sekaligus membuat clickable button yang akan me-redirect ke '/data-penjualan/{$id}' (halaman detail data penjualan) yang di handle pada function show DataPenjualanController 

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

Tes
