SQL Ducan:
________________________________________________________________________

DROP DATABASE IF EXISTS `ducan`;

CREATE DATABASE IF NOT EXISTS `ducan` DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci;
USE `pekara`;

CREATE TABLE IF NOT EXISTS `proizvodi` (
   `id` int UNSIGNED NOT NULL AUTO_INCREMENT,
   `naziv` varchar(100) COLLATE utf8mb4_general_ci NOT NULL,
   `kolicina` int UNSIGNED NOT NULL,
   PRIMARY KEY (`id`)
);

INSERT INTO `proizvodi` (`naziv`, `kolicina`) VALUES
   ('mlijeko', 1000),
   ('kruh', 500),
   ('sunka', 200),
   ('sladoled', 200),
   ('pepsi', 2000);

DROP PROCEDURE IF EXISTS `izmjena_kolicine`;

DELIMITER //

CREATE PROCEDURE IF NOT EXISTS `izmjena_kolicine`(
   IN prodan_proizvod_id INT UNSIGNED,
   IN prodana_kolicina INT UNSIGNED
)

BEGIN
   DECLARE stara_kolicina INT UNSIGNED;

   START TRANSACTION;

   IF prodana_kolicina = 0 THEN
       SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'Izmjena nije potrebna';
   END IF;

   IF NOT EXISTS (SELECT 1 FROM proizvodi WHERE id = prodan_proizvod_id) THEN
       SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'Proizvod ne postoji';
   ELSE
       SELECT kolicina
           INTO stara_kolicina
           FROM proizvodi
           WHERE id = prodan_proizvod_id
           FOR UPDATE;
   END IF;

   IF (stara_kolicina - prodana_kolicina) >= 0 THEN
       UPDATE proizvodi
           SET kolicina = (stara_kolicina - prodana_kolicina)
           WHERE id = prodan_proizvod_id;

       COMMIT;
   ELSE
       ROLLBACK;
       SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'Nema dovoljno na zalihi';
   END IF;

END //

DELIMITER ;

-- poziv procedure
CALL izmjena_kolicine(4, 25);

________________________________________________________________________
HTML FORM
________________________________________________________________________
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Login</title>
</head>
<body>
    <form action="/login" method="POST">
        <div>
            <label for="username">Username</label>
            <input type="text" id="username" name="username" required>
        </div>
        <div>
            <label for="password">Password</label>
            <input type="password" id="password" name="password" required>
        </div>
        <hr>
        <div>
            <button type="submit">Submit</button>
        </div>
    </form>
</body>
</html>

________________________________________________________________________
PHP UNIT / XML
________________________________________________________________________

<?xml version="1.0" encoding="UTF-8"?>
<phpunit xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:noNamespaceSchemaLocation="./vendor/phpunit/phpunit/phpunit.xsd"
         bootstrap="vendor/autoload.php"
         colors="true"
         convertErrorsToExceptions="true"
         convertWarningsToExceptions="true"
         convertNoticesToExceptions="true"
         stopOnFailure="false">

    <!-- testovi -->
    <testsuites>
        <testsuite name="Unit">
            <directory>tests/Unit</directory>
        </testsuite>
        <testsuite name="Feature">
            <directory>tests/Feature</directory>
        </testsuite>
    </testsuites>

    <!-- definiranje koji direktoriji će biti uključeni tokom izvođenja testova -->
    <source>
        <include>
            <directory>app</directory>
        </include>
        <!-- primjer isključivanja direktorija/filea iz provjere -->
        <exclude>
            <directory>app/Providers</directory> 
            <file>app/Providers/AppServiceProvider.php</file>
        </exclude>
    </source>

    <!-- za env varijable umjesto definiranja u phpunit.xml fileu možemo koristiti .env.testing file -->
    <php>
        <env name="APP_ENV" value="testing"/>
        <env name="APP_MAINTENANCE_DRIVER" value="file"/>
        <env name="BCRYPT_ROUNDS" value="4"/>
        <env name="CACHE_STORE" value="array"/> 
        <env name="DB_CONNECTION" value="mysql"/>
        <env name="DB_DATABASE" value="algebra"/>
        <env name="MAIL_MAILER" value="array"/>
        <env name="PULSE_ENABLED" value="false"/>
        <env name="QUEUE_CONNECTION" value="sync"/>
        <env name="SESSION_DRIVER" value="array"/>
        <env name="TELESCOPE_ENABLED" value="false"/>
    </php>
</phpunit>

________________________________________________________________________
PROGRAM TO CLASS
________________________________________________________________________
<?php
class Calculator 
{
    private int $numberA = 0;  // Inicijaliziramo na 0
    private int $numberB = 0;

    public function setA(int $a) 
    {
        $this->numberA = $a;
    }

    public function setB(int $b) 
    {
        $this->numberB = $b;
    }

    public function sum(?int $a = null, ?int $b = null): int
    {
        return ($a ?? $this->numberA) + ($b ?? $this->numberB);
    }

    public function getSum(): int
    {
        return $this->sum();
    }
}

// Kreiranje instance klase
$calculator = new Calculator();

// Poziv metodâ
echo $calculator->getSum() . PHP_EOL; // Vratit će 0

$calculator->setA(7);
$calculator->setB(10);
echo $calculator->getSum() . PHP_EOL; // Vratit će 17 

echo $calculator->sum(4, 5) . PHP_EOL; // Vratit će 9 
?>

Definira se klasa Calculator: Sva funkcionalnost je unutar ove klase.

Privatne varijable: numberA i numberB su privatne varijable koje se koristi za pohranu brojeva.

Javne metode: 

setA(int $a) i setB(int $b) su metode za postavljanje vrijednosti.
sum(?int $a = null, ?int $b = null) izračunava sumu, pri čemu se koriste ili proslijeđene vrijednosti ili uskladištene vrijednosti.
getSum() je metoda koja vraća sumu koristeći trenutne vrijednosti numberA i numberB.
Instanciranje klase: Kreiramo novu instancu klase Calculator kroz $calculator.

Pozivanje metoda: Metode se pozivaju putem instanciranog objekta $calculator, što omogućava jednostavno korištenje funkcionalnosti klase.

Kao rezultat, kada se kod izvrši, ispisat će se:

CopyReplit
0
17
9