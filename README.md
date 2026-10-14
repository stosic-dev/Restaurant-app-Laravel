# Restoran – Laravel aplikacija za naručivanje hrane

Web aplikacija za restoran napravljena u Laravel-u. Posetioci mogu da pregledaju meni, a registrovani korisnici da dodaju jela u korpu i potvrde porudžbinu. Ulogovani korisnici imaju i CRUD stranice za jela, kategorije i porudžbine.

Projekat je rađen u okviru fakultetskog predmeta (RAF).

## Funkcionalnosti

- Početna stranica i javni meni sa jelima po kategorijama
- Registracija, prijava i izmena profila (Laravel Breeze)
- Korpa i potvrda porudžbine
- CRUD za **jela**, **kategorije** i **porudžbine**
- Oznaka "izdvojeno" (`featured`) za jela
- Validacija unosa preko Form Request klasa
- Migracije i seederi sa probnim podacima
- Automatski testovi (PHPUnit) i GitHub Actions workflow

## Tehnologije

- PHP 8.2+ i Laravel 12
- Blade šabloni, Tailwind CSS 3, Vite
- MariaDB / MySQL (testovi koriste SQLite u memoriji)
- Laravel Breeze (autentikacija), Laravel Pint (stil koda)

## Struktura podataka

| Model      | Opis                                                    |
| ---------- | ------------------------------------------------------- |
| `Category` | Kategorija jela (naziv)                                 |
| `Food`     | Jelo: naziv, opis, cena, slika, kategorija, `featured`  |
| `Order`    | Porudžbina: korisnik, ukupna cena, status               |
| `User`     | Korisnik aplikacije                                     |

Jela i porudžbine su povezani preko pivot tabele `food_order`.

## Pokretanje lokalno

Potrebno je: PHP 8.2+, Composer, Node.js i npm, kao i MariaDB ili MySQL.

```bash
git clone https://github.com/stosic-dev/restoran-laravel-app.git
cd restoran-laravel-app

composer install
npm install

cp .env.example .env
php artisan key:generate
```

Napravi praznu bazu (u `.env.example` je podrazumevano ime `projekat_drugi_deo`, a korisnik `root` bez lozinke; prilagodi `DB_*` vrednosti u `.env` svom okruženju), pa pokreni migracije i seedere:

```bash
php artisan migrate --seed
```

Zatim u dva terminala:

```bash
npm run dev
```

```bash
php artisan serve
```

Aplikacija je dostupna na `http://localhost:8000`.

### Probni nalozi (samo za lokalni razvoj)

Seeder pravi dva korisnika:

| Email                    | Lozinka     |
| ------------------------ | ----------- |
| `admin@restaurant.test`  | `pass12345` |
| `user@restaurant.test`   | `password`  |

## Testovi i stil koda

```bash
php artisan test
./vendor/bin/pint
```

## Licenca

Projekat je napravljen u edukativne svrhe. Laravel framework je licenciran pod [MIT licencom](https://opensource.org/licenses/MIT).