## FetchType Eager vs Lazy di Hibernate

Relasi table di Hibernate ada 2:

* **Lazy**
* **Eager**

**_Lazy Loading_** itu mengambil data parent dan child tanpa me-load semua data child ke memory. Data akan di-load ketika ada method spesifik yang dipanggil.

Sedangkan **_Eager Loading_** me-load semua data pada saat query dilakukan, sehingga dapat memperlambat performance.

<br/>
--

Referensi:

* [https://www.baeldung.com/hibernate-lazy-eager-loading](https://www.baeldung.com/hibernate-lazy-eager-loading)
* [http://www.java2novice.com/hibernate/eager-vs-lazy-fetch-type/](http://www.java2novice.com/hibernate/eager-vs-lazy-fetch-type/)

