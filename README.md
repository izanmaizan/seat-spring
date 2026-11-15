# Seat

Penjualan tiket acara dengan pemilihan kursi. Backend Spring Boot untuk belajar transaksi, locking, security, dan event streaming.

## Tech stack

| Bagian | Teknologi |
|---|---|
| Bahasa | Java 21 |
| Framework | Spring Boot 4.1 |
| Data | Spring Data JPA, PostgreSQL, Flyway |
| Keamanan | Spring Security, JWT |
| Messaging | Spring for Apache Kafka |
| Ops | Actuator |
| Build | Maven Wrapper |

## Alur singkat

1. Pengunjung memilih acara dan kursi.
2. Server mengunci kursi dalam transaksi dan memberi batas waktu bayar.
3. Pembayaran dikonfirmasi lewat webhook.
4. Tiket terbit, event `ticket.sold` dikirim ke Kafka.
5. Kursi yang kedaluwarsa dilepas kembali ke daftar.

## Menjalankan

Butuh JDK 21 dan PostgreSQL.

```bash
export DB_URL=jdbc:postgresql://localhost:5432/seat
export DB_USER=postgres
export DB_PASS=postgres
./mvnw spring-boot:run
```

Server di `http://localhost:8080`, health di `/actuator/health`.

```bash
./mvnw test
./mvnw package
```

## Struktur

```
src/main/java/id/izanmaizan/seat/SeatSpringApplication.java   entrypoint
src/main/resources/application.properties                     konfigurasi
pom.xml                                                        dependency
```

## Status

Scaffold dari Spring Initializr. Dependency terpasang, belum ada domain, controller, atau migration.
