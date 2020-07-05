
# A.PROJEN�N HAZIRLANMASI

1.	Solution A��yoruz.

2.	Class Library (.Net Standart) A��yoruz => Ad�na Entities diyoruz. Entity Katman� bizim projemizdeki veri taban�na kar��l�k gelen nesneleri yap�land�rd���m�z katmand�r. Ayr�ca Data Transfer Object (DTO) yap�lar�n� burada tutuyoruz. NOT: Class Library (.Net Standart) B�t�n .NET projelerinde kullan�labilir.

3.	Class Library (.Net Standart) A��yoruz => Ad�na DataAccess diyoruz. DataAccessLayer veya DAL olabilir. DataAccess veri taban� i�lerini yapt���m�z yerdir. Insert, Update, Delete, Select, Alter vb. Temel sorgular� yazd���m�z katmand�r.

4.	Class Library (.Net Standart) A��yoruz => Ad�na Business diyoruz. Business katman�nda projenin i� kurallar�n� yaz�yoruz. Bir i�in algoritmas�n�n yaz�ld��� katmand�r. �rne�in; bir ��rencinin s�n�f� ge�ip ge�emeyece�inin kurallar�n�n yaz�ld��� katmand�r. Veri taban�n veri al�r karar verir. Bu y�zden DataAccess ile ileti�im halindedir. Ondan gelen verileri kullan�r�z. ��inde veri ileti�im kodlar� yazmay�z.

5.	ASP.NET Core Web Application A��yoruz => Ad�na WebUI diyoruz.   Web Application (Model- View- Controller) template�ini ve ASP.NET Core 3.1 versiyonu se�iyoruz. MVC ara y�z kodlar�n� burada yaz�yoruz. Burada veri eri�im ve i� kodlar� yaz�lmaz. Yoksa Api ekledi�imiz zaman apiye tek tek bunlar� eklememiz gerekiyor.

6.	ASP.NET Core Web Application A��yoruz => Ad�na WebUI diyoruz.   API template�ini se�iyoruz.

7.	Class Library (.Net Standart) A��yoruz => Ad�na Core diyoruz.  Core katman� bizim i�in Framework katman� yani sadece bu projemizde de�il di�er projelerimizde de kullanabilece�imiz kodlar� buraya yaz�yoruz. Mesela Hashleme kodlar� buraya yaz�l�r.

#A.1. Entity Katman�

1.	Entity Katman�nda bir klas�r olu�turuyoruz. => Ad�na Concrete diyoruz.  Concrete klas�r�n�n i�ine Product ve Category ad�nda iki Class olu�turuyoruz. �lgili alanlar� propretylerini yaz�yoruz. Her iki Class�na da IEntity ad�ndaki interface�imizden implemente edece�iz.

2.	Entity Katman�nda bir klas�r olu�turuyoruz. => Ad�na Dtos diyoruz.  Dtos klas�r�n�n i�erisine ProductDetail ad�nda bir Class olu�turuyoruz. �lgili alanlar� propretylerini yaz�yoruz. Bu Class�m�zda IDto ad�ndaki interface�imizden implemente edece�iz.

#A.2. Entity Katman�

1.	Core Katman�nda bir klas�r olu�turuyoruz. => Ad�na Entities diyoruz. Not: Genelde kullanaca��m�z katman�n ad� olur.

2.	Core Katman�nda olu�turdu�umuz Entities klas�r�n�n i�erisine bir klas�r olu�turuyoruz => Ad�na Abstract diyoruz. Soyut nesnelerimizi tutmak i�in bu klas�r�m�z� a�t�k. Yani buradaki classlar�m�z veya interfacelerimiz tek ba��na kullan�lmaz imzalamak veya implemente etmek i�in kullan�l�r.  Abstract klas�r�n�n i�erisine IDto ve IEntity ad�nda iki tane interface olu�turuyoruz. ��nk� b�t�n projelerimizde DTO ve ENTITY olur.

#A.3. DataAccess Katman�

1.	DataAccess Katman�nda bir klas�r olu�turuyoruz. => Ad�na Abstract diyoruz. Soyut Classlar�m�z yani imza interface i�in kullanaca��m�z Classlar burada yaz�l�r. Bunun sebebi �rne�in; Entity Framework ORM kullanaca��z. Burada ileti�im halinde oldu�u Business katman� somut Classlar ile ileti�im halinde olursa ve Entity Framework konusunda de�i�ikli�e gidilirse tek tek b�t�n Classlar�m�z� de�i�tirmemiz gerekir. Ama Entity Framework � Soyut Classlar�m�za uygularsak ve de�i�ikli�e gidersek kulland���m�z Somut classlarda herhangi bir de�i�iklik yapmam�za gerek kalmadan imza olarak kulland���m�z Abstract Classlarda tek bir de�i�ik ile rahatl�kla uygulayabiliriz.

2.	DataAccess katman�ndaki Abstract klas�r�ne IProductDal ad�nda bir interface a��yoruz. Bunun i�erisinde Listeleme silme g�ncelleme i�lemlerimiz oluyor.

3.	DataAccess Katman�nda bir klas�r olu�turuyoruz. => Ad�na Concrete diyoruz. Somut i�i yapacak Classlar burada yaz�l�r.

4.	DataAccess katman�ndaki Concrete klas�r�n�n i�ine EntityFramework ad�nda bir klas�r a��yoruz. ��erisini EfProductDal ad�nda bir class olu�turup IProductDal interfacemizden implemente ediyoruz.

#A.4. Core Katman�nda Repository Pattern� uygulama

1.	Core Katman�nda bir klas�r olu�turuyoruz. => Ad�na DataAccess diyoruz.

2.	Core Katman�ndaki DataAccess klas�r�m�z�n i�erisine Abstract ad�nda bir klas�r olu�turuyoruz.  ��erisine IEntityRepository ad�nda bir interface a��yoruz. Burada temel operasyonlar�m�z� yapaca��z. �rne�in; List<Product> veya List<Category> yapaca��z ne olaca��n� bilmedi�imiz i�in Generic tip Yap�yoruz yani IEntityRepository<T> yap�yoruz.

3.	List<T> GetList || (Expression<Func<T,bool>> filter=null)  => Lambda expression ge�iyoruz. Bu bir delegedir.  Filter null default null demek. Func<T,bool> dedi�imiz parametre verirsek uygulamak i�indir. Bunun gidi temel crud operasyonlar� yaz�yoruz.

4.	Daha sonra DataAccess katman�m�zdaki IProductDal class �m�za IEntityRepository<Product> interfacemizi implemente ediyoruz. Tip olarakta product tablosuyla i�lem yapaca��m�z i�in product tipini tan�ml�yoruz.

5.	Daha sonrada Entity Framework kulland���m�z IEntityRepository i implemente etti�imiz IProductDal interfacemizi DataAccess katman�nda Entity Framework kullanarak i�lemlerini yapmay� planlad���m�z Entity Framework katman�ndaki EfProductDal class�m�za implemente ediyoruz.
6.	Core Katman�nda bir klas�r olu�turuyoruz. => Ad�na Concrete diyoruz.

7.	Core Katman�nda Concrete klas�r�n�n i�erisine EntityFramework Ad�nda bir klas�r olu�turuyoruz. 

8.	Daha sonra Core katman�na sa� t�klay�p, Manage Nuget Packages� a t�kl�yoruz Browse k�sm�ndan Microsoft.EntityFrameworkCore.SqlServer ad�yla arat�p EntityFramework Core kurulumunu ger�ekle�tiriyoruz.

9.	Core katman�ndaki Concrete klas�r�n�n i�erisindeki EntityFramework klas�r�ne EfEntityRepositoryBase ad�nda bir Class olu�turuyoruz. IEntityRepository interfaceni implemente ediyoruz. EfEntityRepositoryBase<TEntity, TContext> : || IEntityRepository<TEntity>  => kodun 1. K�sm�nda <TEntity> koduyla alaca�� tipi belirtiyoruz. <TContext> kodu ile Entity Classlar� ile veri taban�n� map etti�imiz unit of work denilen tasar�m desenini implemente eden haz�r Entity Framework yap�s�d�r. 2. K�sm�nda temel kodlar�m�z�n gelece�i k�s�m oluyor. <> i�erisinde verece�imiz tipi belirtiyoruz.

10.	Generic k�s�tlar�m�z� belirliyoruz. where TEntity : class, new() => TEntity referans tip olmak zorunda ve instance(�rnekleme)  alabilecektir.

11.	where TContext : DbContext, new() => TContext DbContext ten inheritance alacak ve instance(�rnekleme) alabilecektir.

12.	 Daha sonra DataAccess Katman�m�zdaki Concrete klas�r�n�n i�erisindeki EntityFramework klas�r�nde bulunun EfProductDal Class��na gidip EfEntityRepositoryBase<Product, NorthwindContext>, IProductDal yazarak implement�e ediyoruz. Bu �ekilde ekleme listeleme vs. temel i�lemler i�in tekrar kod yazmam�za gerek kalmayacakt�r.

#A.5. Context Yap�s�

1.	DataAccess Katman�nda Concrete klas�r�n�n i�esine Entityframework klas�r�n�n i�erisine bir klas�r olu�turuyoruz. => Ad�na Contexts diyoruz.

2.	Contexts klas�r�n�n i�erisine Class olu�turuyoruz => Ad�na NorthwindContext diyoruz. Context olabilmesi i�in EntityFramework ten gelen DbContext s�n�f�ndan inheritance ediyoruz.

3.	Tablolar�m�zla, entitylerimizi map etmek i�in public Dbset<Product> Products {get; set;} yaz�yoruz. Ayn� i�lemi Categories i�inde yap�yoruz.

4.	Hangi Databaseyi kullanaca��m�z� OnConfiguring metodunu override ederek i�ine yaz�yoruz. protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)        {optionsBuilder.UseSqlServer(connectionString:@"Server=(localdb)\mssqllocaldb;initial catalog=northwind; integrated security=true");}

5.	Daha �nce yazm�� oldu�umuz NorthwindContext ler i�in gerekli usingleri ekliyoruz.

#A.6. Business Katman�

1.	Business Katman�na 2 tana klas�r a��yoruz. => Abstract ve Concrete diyoruz.

2.	Abstract klas�r�n�n i�erisine interface a��yoruz Ad�na IProductService diyoruz.  ��erisine Listelemek i�lemlerimizi yapaca��m�z kodlar� yaz�yoruz.

3.	Concrete Klas�r�n�n i�erisine ProductManager ad�nda bir Class olu�turuyoruz. IProductService interfacemizi implemente ediyoruz. Ve IProductDal interfaceni enjekte ediyoruz. Bu �ekilde Entity Framework e direk bir ba��ml�l�k olu�turmad���m�z bir yap� kuruyoruz.

4.	Ayn� i�lemleri Category i�inde uyguluyoruz.

Not: Direk Repository�i kullanmam�z�n sebebi; Business katman�nda yeni parametreler gelebilir.  Bu y�zden Repository�nin kendisi kullan�lmaz. �rne�in; B�t�n �r�nlerimizi Listelerken, Yeni bir i� kural� gelir Id sine g�re de�il isimlerine g�re listelemek gibi ve buna g�re b�t�n Listeleme kurallar�n� de�i�tirmemiz ve buna uygun parametre yazmam�z gerekebilir. Bu y�zden ay�r�yoruz.

