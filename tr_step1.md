Bu senaryoda sizlerden, size tahsis edilen makinelerde aşağıdaki talimatlar gereğince Linux komut satırında kullanıcının SQL sorgularını deneyebileceği şekilde gerekli komutların sağlandığı, "Trigger" işleminin yapılması beklenmektedir.

Trigger: Tetikleyiciler herhangi bir database olayın olması durumunda tetiklenmesi sağlanabilir update,insert,delete vs gibi olaylar meydana geldiginde tetiklenip bir iş yaptırılabilir.örnegin : databaseden bir bilgi silinidiginde log alıp saat kacta kim tarafından yapıldıgının bilgisini almak gibi .
Senaryo boyunca uygulama adımlarında belirtildiği şekilde SQL veritabanı tabloları oluşturulacak ve "Trigger" yardımıyla bir insert işlemi olursa kim tarafından ve tarihinin gözlemlenmesi istenmektedir.

### 🚀 Uygulama Adımları 🚀

1. Alpine Linux sisteminizde SQLite veritabanının kurulu olduğundan emin olunuz. Eğer kurulu değilse, Alpine Linux paket yöneticisi olan `apk` ile SQLite kurabilirsiniz. `apk add sqlite`
2. `/home/bb/` dizini altında `turktelekomtrigger.db` adında veritabanı dosyası oluşturunuz.
3. `sqlite3 turktelekomtrigger.db`komutunu girerek veritabanına bağlananın.
4. `.mode column` komutunu kullanarak sorgu sonuçlarını sütun düzeninde görüntülemeyi ayarlayın.
5. `.headers on` komutunu kullanarak sorgu sonuçlarında sütun başlıklarını görüntülemeyi ayarlayın.
6. Aşağıdaki SQL komutlarını kullanarak örnek tablo oluşturunuz.

```
CREATE TABLE company (
    id INTEGER PRIMARY KEY,
    name TEXT,
    age INTEGER
);
```

7. Aşağıdaki SQL komutlarıyla da Log almak için bir tablo ekleyiniz.

```
CREATE TABLE audit (
    emp_id INTEGER PRIMARY KEY NOT NULL,
    entry_date TEXT NOT NULL,
);
```

8. Aşağıdaki SQL komutlarıyla da bir tetikleyici oluşturunuz, company tablosuna insert işlemi olursa audit tablosuna id ve o anın tarihlerini yazdırınız.

```
CREATE TRIGGER audit_log AFTER INSERT ON company
BEGIN
INSERT INTO audit(emp_id,entry_date) VALUES (new.id,datetime('now'));
END;
```

9. Aşağıdaki SQL komutlarıyla da company tablosuna örnek bir veri ekleyiniz.

```
INSERT INTO company(id,name,age) VALUES(23,'Furkan Aytekin',27);
```

10. Aşağıdaki SQL komutlarıyla da audit tablosunu görüntüleyiniz.

```
SELECT * FROM audit;
```

11. Aşağıdaki SQL komutlarıyla da oluşturulan triggerları listeleyiniz.

```
select name from sqlite_master where type = "trigger";
```

12. `.quit` komutunu kullanarak SQLite terminalinden çıkabilirsiniz.
