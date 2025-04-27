Aspectify

![Kotlin](https://img.shields.io/badge/Kotlin-1.9.0-blue)
![License](https://img.shields.io/badge/license-MIT-green)
![Build](https://github.com/muhammedalikocabey/aspectify/actions/workflows/ci.yml/badge.svg)

Latest commit date: ![Last Commit](https://img.shields.io/github/last-commit/makocabey/aspectify)

Repo stars: ![Stars](https://img.shields.io/github/stars/makocabey/aspectify?style=social)

Repo forks: ![Forks](https://img.shields.io/github/forks/makocabey/aspectify?style=social)
---

## 🇹🇷 Türkçe

### ✨ Proje Tanıtımı

**Aspectify**, Android ve Kotlin JVM projeleri için geliştirilen, hafif, modüler ve modern bir **Aspect-Oriented Programming (AOP)** framework'üdür.

Amacı, uygulamalarda tekrar eden işlemleri (loglama, yetkilendirme, timeout, cache vb.) **ana iş mantığından ayırarak** temiz, okunabilir ve yönetilebilir kod mimarisi sağlamaktır.

Dynamic Proxy ve Kotlin Reflection altyapısıyla çalışır.

---

### 🎯 Proje Hedefi

- **Cross-Cutting Concern'ları** (Loglama, Güvenlik, Performans, Caching) merkezi yönetmek,
- **Business Logic** kodlarının sade ve net olmasını sağlamak,
- **Test edilebilirliği** artırmak,
- **Kod tekrarını azaltmak**.

---

### 🚀 Desteklenen Özellikler

- `@Loggable` → Method giriş/çıkış loglaması
- `@Retryable` → Hata alınca belirli sayıda tekrar deneme
- `@Authenticated` → Kullanıcı rol kontrolü
- `@Transactional` → İşlem (Transaction) yönetimi
- `@Cacheable` → Method sonuçlarını cache'leme
- `@Timed` → Method çalışma süresi ölçümü
- `@Debounce` → Hızlı ardışık method çağrılarını engelleme
- `@Timeout` → Belirli sürede method tamamlama zorunluluğu
- `@RateLimit` → Belirli zaman diliminde çağrı sınırı
- `@BackgroundThread` → Sadece background thread üzerinde çalıştırma

---

### 📦 Kurulum ve Kullanım

#### 1. Proxy Nesnesi Oluşturma

```kotlin
val service = proxyOf<UserService> {
    target = RealUserService()
    logger = ConsoleLogger // Android projelerinde AndroidLogger da kullanılabilir
}
```

#### 2. Annotation Kullanımı

```kotlin
@Loggable
@Retryable(times = 3)
@Authenticated(role = "admin")
fun deleteUser(userId: String) {
    // Kullanıcı silme işlemleri
}
```

#### 3. Proxy Üzerinden Çağrı Yapmak

```kotlin
val service = proxyOf<UserService> {
    target = RealUserService()
}

service.deleteUser("user123")
```

---

### ⚙️ Gereksinimler

- Kotlin 1.9+
- Android API 21+
- JVM 8+
- Kotlin Coroutines desteği

---

### 🔄 Continuous Integration (CI)

Aspectify, GitHub Actions üzerinden otomatik build ve test işlemleri için bir CI (Continuous Integration) altyapısına sahiptir.

Her **push** veya **pull request** sonrasında:

- Proje kodu checkout edilir,
- Java 17 kurulumu yapılır,
- Gradle ile proje temizlenir, build edilir ve tüm testler çalıştırılır.

Workflow dosyası yolu:

```
.github/workflows/ci.yml
```

Workflow içeriği:

```yaml
name: Aspectify CI

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build-and-test:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Code
        uses: actions/checkout@v3

      - name: Setup JDK
        uses: actions/setup-java@v3
        with:
          java-version: '17'
          distribution: 'temurin'

      - name: Build Project and Run Tests
        run: ./gradlew clean build test
```

---

### 📑 Dikkat Edilmesi Gerekenler

- `AndroidLogger` **sadece Android projelerinde** kullanılmalıdır.
- JVM projeleri için **ConsoleLogger** kullanılması önerilir.
- `UserSession` sınıfı SharedPreferences kullanarak kalıcı oturum yönetimi sağlar.

---

### 🧪 Test Kapsamı

- Retry mekanizması test edilmiştir.
- Cache işlemleri test edilmiştir.
- Timeout yönetimi doğrulanmıştır.
- Background thread kontrolü sağlanmıştır.
- Rate limit sınırlamaları test edilmiştir.

Tüm detaylar `InterceptorHandlerTest` dosyasında bulunmaktadır.

---

### 🛠️ Katkıda Bulunmak

Katkıda bulunmak isterseniz:

1. Fork yapın 🍴
2. Feature branch oluşturun (`feature/ozellik-ekleme`)
3. Pull request gönderin ✔️

---

### 🛡️ Lisans

Bu proje [MIT License](LICENSE) altında lisanslanmıştır.

---

## 🇬🇧 English

### ✨ Project Introduction

**Aspectify** is a lightweight, modular, and modern **Aspect-Oriented Programming (AOP)** framework designed for Android and Kotlin JVM projects.

It aims to **separate cross-cutting concerns** (logging, authentication, timeout, caching etc.) from core business logic, achieving cleaner, readable, and maintainable code structure.

Built on top of Dynamic Proxy and Kotlin Reflection.

---

### 🎯 Project Goals

- Manage **cross-cutting concerns** centrally,
- Keep **business logic** clean and focused,
- Increase **testability**,
- Reduce **code duplication**.

---

### 🚀 Supported Features

- `@Loggable` → Logs method entry/exit
- `@Retryable` → Retries on failure
- `@Authenticated` → User role validation
- `@Transactional` → Transaction management
- `@Cacheable` → Caches method results
- `@Timed` → Measures execution time
- `@Debounce` → Debounces rapid method calls
- `@Timeout` → Forces method completion within time
- `@RateLimit` → Rate limits method calls
- `@BackgroundThread` → Forces background thread execution

---

### 📦 Installation & Usage

#### 1. Create a Proxy

```kotlin
val service = proxyOf<UserService> {
    target = RealUserService()
    logger = ConsoleLogger // Or AndroidLogger for Android platform
}
```

#### 2. Annotate Your Methods

```kotlin
@Loggable
@Retryable(times = 3)
@Authenticated(role = "admin")
fun deleteUser(userId: String) {
    // User deletion logic
}
```

#### 3. Make Calls via Proxy

```kotlin
val service = proxyOf<UserService> {
    target = RealUserService()
}

service.deleteUser("user123")
```

---

### ⚙️ Requirements

- Kotlin 1.9+
- Android API 21+
- JVM 8+
- Kotlin Coroutine support

---

### 🔄 Continuous Integration (CI)

Aspectify provides a GitHub Actions workflow for automatic build and test runs.

Every **push** or **pull request**:

- Checks out the project,
- Installs Java 17,
- Runs Gradle clean build and tests.

Workflow file:

```
.github/workflows/ci.yml
```

Workflow content:

```yaml
name: Aspectify CI

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build-and-test:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Code
        uses: actions/checkout@v3

      - name: Setup JDK
        uses: actions/setup-java@v3
        with:
          java-version: '17'
          distribution: 'temurin'

      - name: Build Project and Run Tests
        run: ./gradlew clean build test
```

---

### 📑 Important Notes

- Use `AndroidLogger` **only on Android platform**.
- For JVM/Desktop use **ConsoleLogger**.
- `UserSession` provides persistent user role management using SharedPreferences.

---

### 🧪 Test Coverage

- Retry mechanism verified.
- Cache behavior tested.
- Timeout handling validated.
- Background thread enforcement checked.
- Rate limiting functionality confirmed.

Check the `InterceptorHandlerTest` file for more.

---

### 🛠️ Contributing

If you wish to contribute:

1. Fork 🍴
2. Create a feature branch (`feature/add-something`)
3. Open a pull request ✔️

---

### 🛡️ License

Distributed under the [MIT License](LICENSE).

---

## 📢 Project Summary

> **Aspectify** delivers a modern, modular, and powerful code architecture by integrating **Aspect-Oriented Programming** with **Dynamic Proxy** and **Annotation-driven** design in Android and JVM environments.  
> It separates cross-cutting concerns cleanly, enhances maintainability, and increases testability.  
> This project is a strong demonstration of advanced software design principles, Kotlin Reflection mastery, and modern Android development practice.

---
