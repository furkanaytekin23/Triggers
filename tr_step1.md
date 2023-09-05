Bu senaryoda sizlerden, size tahsis edilen makinelerde aşağıdaki talimatlar gereğince Linux komut satırında kullanıcının SQL veritabanı tabloları oluşturulacak ve "Trigger" yardımıyla bir insert işlemi olursa kim tarafından ve tarihinin gözlemlenmesi istenmektedir.

Trigger: Tetikleyiciler herhangi bir database olayın olması durumunda tetiklenmesi sağlanabilir update,insert,delete vs gibi olaylar meydana geldiginde tetiklenip bir iş yaptırılabilir.örnegin : databaseden bir bilgi silinidiginde log alıp saat kacta kim tarafından yapıldıgının bilgisini almak gibi .

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
    entry_date TEXT NOT NULL
);
```

8. SQL komutlarıyla bir tetikleyici oluşturunuz, company tablosuna insert işlemi olursa audit tablosuna id ve o anın tarihlerini yazdırınız.


9. SQL komutlarıyla company tablosuna örnek bir veri ekleyiniz.


10. SQL komutlarıyla  audit tablosunu görüntüleyiniz.


11. Aşağıdaki SQL komutlarıyla da oluşturulan triggerları listeleyiniz.

```
select name from sqlite_master where type = "trigger";
```
12. Yazmış olduğunuz trigger syntaxını kopyalayıp `/home/bb/` dizini altında vim editörüyle `trigger.txt` adında dosyaya yapıştırıp kaydediniz.

13. `.quit` komutunu kullanarak SQLite terminalinden çıkabilirsiniz.
