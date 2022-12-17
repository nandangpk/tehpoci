# Teh Poci
Menggunakan Laravel versi 9.19 dan PHP versi 8.0.2

**Terdapat 5 Controller:**
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

**Terdapat 4 Model:**
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


## #1 Menu Order
![image](https://user-images.githubusercontent.com/54816942/208220021-a85171f9-fb51-4881-86ab-cd843f7209bd.png)
```php
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
```
Tes
