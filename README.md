# Postman-FinalProjectAPI-Sanbercode
Final Project for API Testing Automation with Postman in Sanbercode as Learning Partner

## Informasi Dasar
Aplikasi API Testing ini adalah sebuah Final Project dari `Sanbercode` dengan topik `Automation API Testing`, Task berfokus pada bagimana cara kerja API dengan melakukan testing pada semua end Point, yang dibuat oleh:

Nama		                 : `Mohammad Nurdiansyah`\

---

# Panduan Penggunaan Aplikasi

## Requirement yang harus disipkan sebelum running aplikasi ini adalah :
- Menggunakan `Postman`
- Testing dilakukan pada End-Point API yang disediakan oleh [`Simple Books`](https://bronzed-hip-506.notion.site/Books-API-Documentation-136749f8f5eb4db68904205894009613)

# End Point
Keseluruhan Endpoint pada Reqress diuji pada project ini adalah :

## Status
### GET Status
```
https://simple-books-api.glitch.me/status
```
Untuk mendapatkan status API\
Akan menghasilkan response code `200 OK` dan result
```
{
    "status": "OK"
}
```

## List of books
### GET List of books
```
https://simple-books-api.glitch.me/books
```
Untuk mendapatkan daftar buku\
Akan menghasilkan response code `200` dan result
```
  [
    {
        "id": 1,
        "name": "The Russian",
        "type": "fiction",
        "available": true
    },
    {
        "id": 2,
        "name": "Just as I Am",
        "type": "non-fiction",
        "available": false
    },
    {
        "id": 3,
        "name": "The Vanishing Half",
        "type": "fiction",
        "available": true
    },
    {
        "id": 4,
        "name": "The Midnight Library",
        "type": "fiction",
        "available": true
    },
    {
        "id": 5,
        "name": "Untamed",
        "type": "non-fiction",
        "available": true
    },
    {
        "id": 6,
        "name": "Viscount Who Loved Me",
        "type": "fiction",
        "available": true
    }
]
```

## Get a single book
### GET Get a single book
```
https://simple-books-api.glitch.me/books/:bookId
```
Untuk mendapatakn informasi rinci tentang buku, dengan mengambil id buku dengan id 4\
Akan menghasilkan response code `200` dan result
```
{
    "id": 4,
    "name": "The Midnight Library",
    "author": "Matt Haig",
    "type": "fiction",
    "price": 15.6,
    "current-stock": 87,
    "available": true
}
```
Jika id buku yang dimasukan tidak sesuai\
Akan menghasilkan response code `404 Not Found` dan result
```
{
    "error": "No book with id 7"
}
```

## API Authentication
### POST Post API clients
```
https://simple-books-api.glitch.me/api-clients/
```
Untuk mengirimkan atau melihat pesanan, jadi perlu mendaftarkan klien API.\
Dengan request `Body` dalam format `JSON` dan menyertakan properti berikut ini:
```
{
   "clientName": "{{$randomFullName}}",
   "clientEmail": "{{$randomEmail}}"
}
```
Akan menghasilkan response code `201 Created` dan result
```
{
    "accessToken": "133dfddfebc48f7a49f96aba77b3be1daba1d3a5cd446126b8805d4269a3a2ab"
}
```
Jika email yang dimasukan sudah terdaftar\
Akan menghasilkan response code `409 Conflict` dan result
```
{
    "error": "API client already registered. Try a different email."
}
```
## Submit an order
### POST Submit an order
```
https://simple-books-api.glitch.me/orders
```
Untuk melakukan order baru\
Dengan memasukan token yang sudah dibuat pada `Authorization` dengan atribut `Bearer Token` Token {{token}}
Serta mengisi pada `Body` dengan atribut `raw` dan `JSON`

```
{
  "bookId": 3,
  "customerName": "{{$randomFullName}}"
}
```

Akan menghasilkan response code `201 Created` dan result akan menampilkan

```
{
    "created": true,
    "orderId": "94sRiPnfjm72KtlOsGlNd"
}

```
Jika Id book tidak sesuai\
```
{
  "bookId": 7,
  "customerName": "{{$randomFullName}}"
}
```
Akan menghasilkan response code `400 Bad Request` dan result akan menampilkan

```
{
    "error": "Invalid or missing bookId."
}

```

## Get all orders
### GET Get all orders
```
https://simple-books-api.glitch.me/orders
```
Untuk meligat semua orderan yang sudah dibuat\
Dengan memasukan token yang sudah dibuat pada `Authorization` dengan atribut `Bearer Token` Token {{token}}
Akan menghasilkan response code `200 OK` dan result
```
[
    {
        "id": "94sRiPnfjm72KtlOsGlNd",
        "bookId": 3,
        "customerName": "Teresa Cartwright",
        "createdBy": "e6fec39343024d779b441cf422f087e919e454af60d90438e71f07082fd4b50f",
        "quantity": 1,
        "timestamp": 1732640763219
    },
    {
        "id": "vSLDO9SmfY4tgZil_efFS",
        "bookId": 1,
        "customerName": "Andrew Wuckert",
        "createdBy": "e6fec39343024d779b441cf422f087e919e454af60d90438e71f07082fd4b50f",
        "quantity": 1,
        "timestamp": 1732641621340
    }
]
```

## Get an order
### GET Get an order
```
https://simple-books-api.glitch.me/orders/:orderId
```
Untuk meligat orderan berdasrkan Id order\
Dengan memasukan token yang sudah dibuat pada `Authorization` dengan atribut `Bearer Token` Token {{token}}
Akan menghasilkan response code `200 OK` dan result

```
{
    "id": "94sRiPnfjm72KtlOsGlNd",
    "bookId": 3,
    "customerName": "Teresa Cartwright",
    "createdBy": "e6fec39343024d779b441cf422f087e919e454af60d90438e71f07082fd4b50f",
    "quantity": 1,
    "timestamp": 1732640763219
}
```

Jika Id order tidak sesuai\
Akan menghasilkan response code `404 Not Found` dan result akan menampilkan

```
{
    "error": "No order with id 94sRiPnfjm72KtlOsGlNdd."
}

```


## Update an order
### PATCH Update an order
```
https://simple-books-api.glitch.me/orders/:orderId
```
Untuk memperbarui pesanan yang sudah ada\
Dengan memasukan token yang sudah dibuat pada `Authorization` dengan atribut `Bearer Token` Token {{token}}
Serta mengisi pada `Body` dengan atribut `raw` dan `JSON`

```
{
  "customerName": "{{$randomFullName}}"
  
}
```
Akan menghasilkan response code `204 No Content` dan result
```
1
```

## Delete an order
### DELETE Delete an order

```
https://simple-books-api.glitch.me/orders/:orderId
```
Akan menghasilkan response code `204 No Content` dan result
```
1
```

[LinkedIn](https://www.linkedin.com/in/mohammad-nurdiansyah-099b31151/) | [GitHub](https://github.com/nurdinsh)
