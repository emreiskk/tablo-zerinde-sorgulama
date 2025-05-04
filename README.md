# tablo-zerinde-sorgulama

1 - Satış yapılan müşterilerin isimlerini listelemek için gerekli SQL ifadesini yazınız.
SELECT Madi, Msoyadi
FROM Musteriler
WHERE Madres = 'Turhal/Tokat';

2 - Hangi müşteriden hangi aracın alındığını listelemek için gerekli SQL ifadesini yazınız.
SELECT Madi, Msoyadi, SiparisTarihi
FROM Musteriler
JOIN Siparisler ON Musteriler.Mno = Siparisler.Mno;

3 - Her bir müşteriden alınan araçların sayısını listelemek için gerekli SQL ifadesini yazınız.
SELECT Madi, Msoyadi, UrunAdi
FROM Musteriler
JOIN Siparisler ON Musteriler.Mno = Siparisler.Mno
JOIN Urunler ON Siparisler.UrunNo = Urunler.UrunNo;

4 - Satılan araçların marka ve modelini bulmak için gerekli SQL ifadesini yazınız.
SELECT DISTINCT UrunAdi
FROM Urunler
JOIN Siparisler ON Urunler.UrunNo = Siparisler.UrunNo
JOIN Musteriler ON Siparisler.Mno = Musteriler.Mno
WHERE Madres = 'Turhal/Tokat';

5 - Toplam satış ve toplam alım tutarlarını ve bunların farkını bulmak için gerekli SQL ifadesini yazınız.
SELECT UrunAdi, COUNT(*) AS SiparisSayisi
FROM Urunler
JOIN Siparisler ON Urunler.UrunNo = Siparisler.UrunNo
GROUP BY UrunAdi;

6 - Hiç satışı yapılmamış araçları listelemek için gerekli SQL ifadesini yazınız.
SELECT Madi, Msoyadi, UrunAdi
FROM Musteriler
JOIN Siparisler ON Musteriler.Mno = Siparisler.Mno
JOIN Urunler ON Siparisler.UrunNo = Urunler.UrunNo
WHERE UrunAdi = 'Televizyon';

7 - Her aracın ortalama satış tutarını bulmak için gerekli SQL ifadesini yazınız.
SELECT Madi, Msoyadi
FROM Musteriler
WHERE Mno NOT IN (
    SELECT Mno FROM Siparisler
);

8 - Alımı ve satışı yapılan tüm araçların marka, model ve alım-satış sayısını listelemek için gerekli SQL ifadesiniz yazınız.
SELECT UrunAdi, Fiyat
FROM Urunler
WHERE Fiyat = (
    SELECT MAX(Fiyat) FROM Urunler
);

9 - 20000’den fazla tutara satılan araçları kimlerin hangi aracı aldığını bulmak için gerekli SQL ifadesini yazınız.
SELECT Madi, Msoyadi, SUM(Fiyat) AS ToplamTutar
FROM Musteriler
JOIN Siparisler ON Musteriler.Mno = Siparisler.Mno
JOIN Urunler ON Siparisler.UrunNo = Urunler.UrunNo
GROUP BY Madi, Msoyadi;

10 - Tokatta bulunan müşterilere satışı yapılan araçları listelemek için gerekli SQL ifadesini yazınız.
SELECT UrunAdi, COUNT(*) AS SiparisSayisi
FROM Urunler
JOIN Siparisler ON Urunler.UrunNo = Siparisler.UrunNo
GROUP BY UrunAdi
ORDER BY SiparisSayisi DESC
LIMIT 1;
