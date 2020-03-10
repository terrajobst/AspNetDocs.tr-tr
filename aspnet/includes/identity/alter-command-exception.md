> Uygulamanın kimlik veri deposu olarak SQLite kullanması durumunda bazı komutlar desteklenmez. Veritabanı altyapısından sınırlamalar nedeniyle `Alter` komutlar aşağıdaki özel durumu oluşturur:
>
> "System. NotSupportedException: SQLite bu geçiş işlemini desteklemiyor." 
>
> Geçici bir çözüm olarak, tabloları değiştirmek için veritabanında Code First geçişleri çalıştırın.
