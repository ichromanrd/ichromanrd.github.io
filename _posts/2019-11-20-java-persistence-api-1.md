---
layout: post
title: "Java Persistence API #1"
date: 2019-11-20 17:30:00 +7
comments: true
categories:
---

Artikel ini adalah bagian pertama dari seri Java Persistence API

### 1. Apa itu JPA

JPA adalah sebuah spesifikasi atau standar, tentang bagaimana kita menyimpan sebuah objek di Java. JPA sendiri adalah singkatan dari Java Persistence API. *Persist* sendiri berarti: teguh; tahan lama; tidak berubah dalam kurun waktu tertentu. Umumnya objek di Java adalah data. Data biasanya disimpan agar dapat digunakan kembali (reusable). *Persistence* sendiri dimaksudkan agar objek Java yang pakai di aplikasi ini dapat disimpan sehingga tetap ada dan dapat digunakan kembali nantinya meskipun (misalnya) aplikasi yang memproduksi atau mengkonsumsi objek ini sudah mati atau tidak berjalan lagi.

Berbicara tentang JPA, biasanya tidak terlepas dari berbicara tentang database. JPA ada dalam package `javax.persistence.*`.


### 2. Mengapa menggunakan JPA

Sesuai dengan deskripsi pada poin 1, kita menggunakan JPA sebagai standar untuk mengimplementasikan:

1. data mana yang akan disimpan dan, 
2. bagaimana cara kita menyimpan data tersebut.


### 3. Keuntungan menggunakan JPA

Dengan menggunakan JPA, kita tidak perlu ribet memikirkan bagaimana data tersebut akan di-*store* ke database, cara menerjemahkan sebuah objek menjadi tabel di database ataupun cara kita mengambil 1 row data dari tabel dan diterjemahkan kembali menjadi sebuah objek yang dapat kita gunakan langsung di dalam aplikasi Java.

### 4. ORM

Object Relational Mapping (ORM) sederhananya adalah framework yang mengimplementasi standar yang ditetapkan oleh JPA. ORM melakukan translasi dari sebuah objek Java ke dalam tabel database yang dimaksud. Jika JPA menetapkan bahwa, agar sebuah class Java dapat ditranslasi menjadi tabel, class tersebut harus dipasangi anotasi `@Entity`. Lalu tugas ORM adalah menerjemahkan class tersebut ke dalam tabel. ORM juga melakukan mapping field atau properti dari sebuah class menjadi kolom pada tabel di database. Sebuah properti `firstName` pada class `Student` akan menjadi kolom `first_name` pada tabe `student` di database, misalnya.

Framework ORM yang paling *mature* dan banyak digunakan untuk implementasi JPA adalah **Hibernate**.

### 5. Langkah-langkah menggunakan JPA di Spring Boot

#### Dependensi

Untuk menggunakan JPA pada Spring Boot, pertama-tama buat sebuah Spring Boot project dari Spring Initializr (start.spring.io). Dan tambahkan dependensi `spring-boot-starter-jpa`.

Gradle:

```
dependencies {
	implementation 'org.springframework.boot:spring-boot-starter-data-jpa'
}
```

Maven: 

```
<dependencies>
	<dependency>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-data-jpa</artifactId>
	</dependency>
	<!-- other dependencies -->
</dependencies>
```

#### Konfigurasi

Selanjutnya lakukan konfigurasi di file `application.propertie` atau `application.yml`.

```
spring:
  datasource:
    url: // (a)
    driverClassName: // (b)
    username: (c)
    password: (d)
  jpa:
  	hibernate:
  	   ddl-auto: (e)
```

**(a)** Isi dengan URL database. <br/>
**(b)** Isi dengan driver database yang kita gunakan. Untuk ini kita juga perlu menambahkan dependensi driver database tersebut. Contoh (Gradle):

```
dependencies {
	implementation 'org.springframework.boot:spring-boot-starter-data-jpa'
	runtimeOnly 'mysql:mysql-connector-java'
}
```

**(c)** Isi dengan username database. <br/>
**(d)** Isi dengan password database (opsional). <br/>
**(e)** Isi dengan *DDL type* Hibernate (create, create-drop, update).

Contoh lengkap file konfigurasinya sebagai berikut:

```
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/testdb
    driverClassName: com.mysql.cj.jdbc.Driver
    username: root
    password: root123
  jpa:
    hibernate:
  	  ddl-auto: create
```

#### Membuat Entity

Kita akan membuat class `Student` sebagai contoh entitas yang akan di-*mapping* ke database. Buat class tersebut di dalam package `com.belajar.jpa.entity`:

```
package com.example.jpa.entity;

import javax.persistence.Entity;
import javax.persistence.Id;

@Entity
public class Student {
    @Id // (a)
    private Long id;
    private String firstName;
    private String middleName;
    private String lastName;
    private String address;
    
    // setter & getter
}
```
**(a)** Setiap class yang ditandai dengan anotasi `@Entity` wajib memiliki anotasi `@Id` pada salah satu propertinya. Ini bertujuan agar JPA menandai properti tersebut sebagai primary key.

Lalu run aplikasi Spring Boot kita dan selanjutnya cek di database, tabel student telah dibuat.

![](https://raw.githubusercontent.com/ichromanrd/blog-images/master/jpa-start/jpa-start-01.png)

<br/>
Cek juga properti dari tabel tersebut dengan perintah **DESC**.

![](https://raw.githubusercontent.com/ichromanrd/blog-images/master/jpa-start/jpa-start-02.png)

<br/>
Artikel selanjutnya akan membahas fitur-fitur dari JPA. Source code dalam artikel ini dapat ditemukan di [repository github](https://github.com/ichromanrd/blog-codes/tree/master/jpa-start/jpa-mysql-gradle) saya.

Terima kasih telah membaca! :raised_hands:
