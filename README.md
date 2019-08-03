# UAS_ORACLE
UAS Pemrosesan Data Tersebar


  
# UAS Pemrosesan Data Tersebar

Aplikasi Pembelian dan Penjualan dengan menggunakan database Oracle, System Administrator menggunakan CodeIgniter dan Interface di Mobile Apps (Android). Komunikasi data antar Aplikasi menggunakan *RESTful Service* di oracle.

## Requirements

- [Virtual Box](https://www.virtualbox.org/wiki/Downloads) (Virtual Server)
- [Oracle Developer Day 11g](https://www.oracle.com/technetwork/database/enterprise-edition/databaseappdev-vm-161299.html) (Database)
- [Android Studio](https://developer.android.com/studio) (Android IDE)
- [Codeigniter](https://www.codeigniter.com/) (Framework PHP)

## Tutorial

### Database

Aplikasi ini memiliki 5 table, yaitu :

1. [Customer](#t_customer)
2. [Barang](#t_barang)
3. [Penjualan](#t_penjualan)
4. [Pembelian](#t_pembelian)
5. [Supplier](#t_supplier)

#### Table Customer

![Table Customer!](./UAS/t_costumer.PNG "Table Customer")

#### Table Barang

![Table Barang!](./UAS/t_barang.png "Table Barang")

#### Table Penjualan

![Table Penjualan!](./UAS/t_penjualan.png "Table Penjualan")

#### Table Pembelian

![Table Pembelian!](./UAS/t_pembelian.png "Table Pembelian")

#### Table Supplier

![Table Supplier!](./UAS/t_supplier.png "Table Supplier")

### *RESTful Services*

![RESTful Services](./UAS/restful.png)

PUT dan DELETE menggunakan {id} untuk mengidentifikasi data yang akan dieksekusi.  
Metode HTTP yang digunakan dalam aplikasi ini adalah:

| Method | Description |
| ------ | ------ |
| **GET** | menyediakan hanya akses baca pada _resource_ |
| **POST** | digunakan untuk menciptakan _resource_ baru |
| **PUT** | digunakan untuk memperbarui _resource_ yang ada atau membuat _resource_ baru |
| **DELETE** | digunakan untuk menghapus _resource_ |

*Resource Handler* & *Query* dapat dilihat pada gambar dibawah ini.

#### *RESTful Service* pada Barang

- **GET Barang**  
![GET](./UAS/get_barang.PNG)

- **POST Barang**  
![POST](./UAS/post_barang.PNG)

- **PUT Barang**  
![PUT](./UAS/put_barang.PNG)

- **DELETE Barang**  
![DELETE](./UAS/delete_barang.PNG)


#### *RESTful Service* pada Customer

- **GET Customer**  
![GET](./UAS/get_costumer.PNG)

- **POST Customer**  
![POST](./UAS/post_costumer.PNG)


- **PUT Customer**  
![PUT](./UAS/put_costumer.PNG)


- **DELETE Customer**  
![DELETE](./UAS/delete_costumer.PNG)
#### *RESTful Service* pada Penjualan

- **GET Penjualan**  
![GET](./UAS/get_penjualan.PNG)
- **POST Penjualan**  
![POST](./UAS/post_barang.PNG)

#### *RESTful Service* pada Pembelian

- **GET Pembelian**  
![GET](./UAS/get_pembelian.PNG)

- **POST Pembelian**  
![POST](./UAS/post_barang.PNG)
#### *RESTful Service* pada Supplier

- **GET Supplier**  
![GET](./UAS/get_supplier.PNG)

- **POST Supplier**  
![POST](./UAS/post_supplier.PNG)

- **PUT Supplier**  
![PUT](./UAS/put_supplier.PNG)
- **DELETE Supplier**  
![DELETE](./UAS/delete_supplier.PNG)

### CodeIgniter

[Script](./oracle-uas/application/libraries/Api.php) dibawah ini merupakan script php yang digunakan untuk mengakses *RESTful Services* dari Oracle menggunakan library [Goutte](https://github.com/FriendsOfPHP/Goutte).

```php
use GuzzleHttp\Client;

defined('BASEPATH') or exit('No direct script access allowed');

class Api
{
    private $client;

    public function __construct()
    {
        // base url yang digunakan untuk mengakses RESTful API
        $this->client = new Client(['base_uri' => 'http://192.168.43.75:8888/apex/obe/']);
    }

    public function request($method, $uri, $data = [])
    {
        // data di convert menjadi data JSON
        $options['json'] = $data;

        // jika metode HTTP nya adalah DELETE maka response yang diberikan adalah status code nya
        if ($method == 'delete') {
            $request = $this->client->request($method, $uri);
            return $request->getStatusCode();
        }

        $request = $this->client->request($method, $uri, $options);

        // response yang diberikan berupa content nya
        return $request->getBody()->getContents();
    }
}
```

#### Tampilan Web

- Barang
![List Barang](./UAS/web/barang.PNG)

- Customer
![List Customer](./UAS/web/customer.PNG)

- Penjualan
![List Penjualan](./UAS/web/penjualan.PNG)

- Pembelian
![List Pembelian](./UAS/web/pembelian.PNG)

- Supplier
![List Supplier](./UAS/web/supplier.PNG)

#### Tampilan Mobile Apps

![Gambar Android](./UAS/android.jpg)

### License

Copyright © 2019, [Vina Agustina]
