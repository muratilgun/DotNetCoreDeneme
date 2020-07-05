
# A.PROJENÝN HAZIRLANMASI

1.	Solution Açýyoruz.

2.	Class Library (.Net Standart) Açýyoruz => Adýna Entities diyoruz. Entity Katmaný bizim projemizdeki veri tabanýna karþýlýk gelen nesneleri yapýlandýrdýðýmýz katmandýr. Ayrýca Data Transfer Object (DTO) yapýlarýný burada tutuyoruz. NOT: Class Library (.Net Standart) Bütün .NET projelerinde kullanýlabilir.

3.	Class Library (.Net Standart) Açýyoruz => Adýna DataAccess diyoruz. DataAccessLayer veya DAL olabilir. DataAccess veri tabaný iþlerini yaptýðýmýz yerdir. Insert, Update, Delete, Select, Alter vb. Temel sorgularý yazdýðýmýz katmandýr.

4.	Class Library (.Net Standart) Açýyoruz => Adýna Business diyoruz. Business katmanýnda projenin iþ kurallarýný yazýyoruz. Bir iþin algoritmasýnýn yazýldýðý katmandýr. Örneðin; bir öðrencinin sýnýfý geçip geçemeyeceðinin kurallarýnýn yazýldýðý katmandýr. Veri tabanýn veri alýr karar verir. Bu yüzden DataAccess ile iletiþim halindedir. Ondan gelen verileri kullanýrýz. Ýçinde veri iletiþim kodlarý yazmayýz.

5.	ASP.NET Core Web Application Açýyoruz => Adýna WebUI diyoruz.   Web Application (Model- View- Controller) template’ini ve ASP.NET Core 3.1 versiyonu seçiyoruz. MVC ara yüz kodlarýný burada yazýyoruz. Burada veri eriþim ve iþ kodlarý yazýlmaz. Yoksa Api eklediðimiz zaman apiye tek tek bunlarý eklememiz gerekiyor.

6.	ASP.NET Core Web Application Açýyoruz => Adýna WebUI diyoruz.   API template’ini seçiyoruz.

7.	Class Library (.Net Standart) Açýyoruz => Adýna Core diyoruz.  Core katmaný bizim için Framework katmaný yani sadece bu projemizde deðil diðer projelerimizde de kullanabileceðimiz kodlarý buraya yazýyoruz. Mesela Hashleme kodlarý buraya yazýlýr.

#A.1. Entity Katmaný

1.	Entity Katmanýnda bir klasör oluþturuyoruz. => Adýna Concrete diyoruz.  Concrete klasörünün içine Product ve Category adýnda iki Class oluþturuyoruz. Ýlgili alanlarý propretylerini yazýyoruz. Her iki Classýna da IEntity adýndaki interface’imizden implemente edeceðiz.

2.	Entity Katmanýnda bir klasör oluþturuyoruz. => Adýna Dtos diyoruz.  Dtos klasörünün içerisine ProductDetail adýnda bir Class oluþturuyoruz. Ýlgili alanlarý propretylerini yazýyoruz. Bu Classýmýzda IDto adýndaki interface’imizden implemente edeceðiz.

#A.2. Entity Katmaný

1.	Core Katmanýnda bir klasör oluþturuyoruz. => Adýna Entities diyoruz. Not: Genelde kullanacaðýmýz katmanýn adý olur.

2.	Core Katmanýnda oluþturduðumuz Entities klasörünün içerisine bir klasör oluþturuyoruz => Adýna Abstract diyoruz. Soyut nesnelerimizi tutmak için bu klasörümüzü açtýk. Yani buradaki classlarýmýz veya interfacelerimiz tek baþýna kullanýlmaz imzalamak veya implemente etmek için kullanýlýr.  Abstract klasörünün içerisine IDto ve IEntity adýnda iki tane interface oluþturuyoruz. Çünkü bütün projelerimizde DTO ve ENTITY olur.

#A.3. DataAccess Katmaný

1.	DataAccess Katmanýnda bir klasör oluþturuyoruz. => Adýna Abstract diyoruz. Soyut Classlarýmýz yani imza interface için kullanacaðýmýz Classlar burada yazýlýr. Bunun sebebi örneðin; Entity Framework ORM kullanacaðýz. Burada iletiþim halinde olduðu Business katmaný somut Classlar ile iletiþim halinde olursa ve Entity Framework konusunda deðiþikliðe gidilirse tek tek bütün Classlarýmýzý deðiþtirmemiz gerekir. Ama Entity Framework ü Soyut Classlarýmýza uygularsak ve deðiþikliðe gidersek kullandýðýmýz Somut classlarda herhangi bir deðiþiklik yapmamýza gerek kalmadan imza olarak kullandýðýmýz Abstract Classlarda tek bir deðiþik ile rahatlýkla uygulayabiliriz.

2.	DataAccess katmanýndaki Abstract klasörüne IProductDal adýnda bir interface açýyoruz. Bunun içerisinde Listeleme silme güncelleme iþlemlerimiz oluyor.

3.	DataAccess Katmanýnda bir klasör oluþturuyoruz. => Adýna Concrete diyoruz. Somut iþi yapacak Classlar burada yazýlýr.

4.	DataAccess katmanýndaki Concrete klasörünün içine EntityFramework adýnda bir klasör açýyoruz. Ýçerisini EfProductDal adýnda bir class oluþturup IProductDal interfacemizden implemente ediyoruz.

#A.4. Core Katmanýnda Repository Patterný uygulama

1.	Core Katmanýnda bir klasör oluþturuyoruz. => Adýna DataAccess diyoruz.

2.	Core Katmanýndaki DataAccess klasörümüzün içerisine Abstract adýnda bir klasör oluþturuyoruz.  Ýçerisine IEntityRepository adýnda bir interface açýyoruz. Burada temel operasyonlarýmýzý yapacaðýz. Örneðin; List<Product> veya List<Category> yapacaðýz ne olacaðýný bilmediðimiz için Generic tip Yapýyoruz yani IEntityRepository<T> yapýyoruz.

3.	List<T> GetList || (Expression<Func<T,bool>> filter=null)  => Lambda expression geçiyoruz. Bu bir delegedir.  Filter null default null demek. Func<T,bool> dediðimiz parametre verirsek uygulamak içindir. Bunun gidi temel crud operasyonlarý yazýyoruz.

4.	Daha sonra DataAccess katmanýmýzdaki IProductDal class ýmýza IEntityRepository<Product> interfacemizi implemente ediyoruz. Tip olarakta product tablosuyla iþlem yapacaðýmýz için product tipini tanýmlýyoruz.

5.	Daha sonrada Entity Framework kullandýðýmýz IEntityRepository i implemente ettiðimiz IProductDal interfacemizi DataAccess katmanýnda Entity Framework kullanarak iþlemlerini yapmayý planladýðýmýz Entity Framework katmanýndaki EfProductDal classýmýza implemente ediyoruz.
6.	Core Katmanýnda bir klasör oluþturuyoruz. => Adýna Concrete diyoruz.

7.	Core Katmanýnda Concrete klasörünün içerisine EntityFramework Adýnda bir klasör oluþturuyoruz. 

8.	Daha sonra Core katmanýna sað týklayýp, Manage Nuget Packages’ a týklýyoruz Browse kýsmýndan Microsoft.EntityFrameworkCore.SqlServer adýyla aratýp EntityFramework Core kurulumunu gerçekleþtiriyoruz.

9.	Core katmanýndaki Concrete klasörünün içerisindeki EntityFramework klasörüne EfEntityRepositoryBase adýnda bir Class oluþturuyoruz. IEntityRepository interfaceni implemente ediyoruz. EfEntityRepositoryBase<TEntity, TContext> : || IEntityRepository<TEntity>  => kodun 1. Kýsmýnda <TEntity> koduyla alacaðý tipi belirtiyoruz. <TContext> kodu ile Entity Classlarý ile veri tabanýný map ettiðimiz unit of work denilen tasarým desenini implemente eden hazýr Entity Framework yapýsýdýr. 2. Kýsmýnda temel kodlarýmýzýn geleceði kýsým oluyor. <> içerisinde vereceðimiz tipi belirtiyoruz.

10.	Generic kýsýtlarýmýzý belirliyoruz. where TEntity : class, new() => TEntity referans tip olmak zorunda ve instance(örnekleme)  alabilecektir.

11.	where TContext : DbContext, new() => TContext DbContext ten inheritance alacak ve instance(örnekleme) alabilecektir.

12.	 Daha sonra DataAccess Katmanýmýzdaki Concrete klasörünün içerisindeki EntityFramework klasöründe bulunun EfProductDal Class’ýna gidip EfEntityRepositoryBase<Product, NorthwindContext>, IProductDal yazarak implement’e ediyoruz. Bu þekilde ekleme listeleme vs. temel iþlemler için tekrar kod yazmamýza gerek kalmayacaktýr.

#A.5. Context Yapýsý

1.	DataAccess Katmanýnda Concrete klasörünün içesine Entityframework klasörünün içerisine bir klasör oluþturuyoruz. => Adýna Contexts diyoruz.

2.	Contexts klasörünün içerisine Class oluþturuyoruz => Adýna NorthwindContext diyoruz. Context olabilmesi için EntityFramework ten gelen DbContext sýnýfýndan inheritance ediyoruz.

3.	Tablolarýmýzla, entitylerimizi map etmek için public Dbset<Product> Products {get; set;} yazýyoruz. Ayný iþlemi Categories içinde yapýyoruz.

4.	Hangi Databaseyi kullanacaðýmýzý OnConfiguring metodunu override ederek içine yazýyoruz. protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)        {optionsBuilder.UseSqlServer(connectionString:@"Server=(localdb)\mssqllocaldb;initial catalog=northwind; integrated security=true");}

5.	Daha önce yazmýþ olduðumuz NorthwindContext ler için gerekli usingleri ekliyoruz.

#A.6. Business Katmaný

1.	Business Katmanýna 2 tana klasör açýyoruz. => Abstract ve Concrete diyoruz.

2.	Abstract klasörünün içerisine interface açýyoruz Adýna IProductService diyoruz.  Ýçerisine Listelemek iþlemlerimizi yapacaðýmýz kodlarý yazýyoruz.

3.	Concrete Klasörünün içerisine ProductManager adýnda bir Class oluþturuyoruz. IProductService interfacemizi implemente ediyoruz. Ve IProductDal interfaceni enjekte ediyoruz. Bu þekilde Entity Framework e direk bir baðýmlýlýk oluþturmadýðýmýz bir yapý kuruyoruz.

4.	Ayný iþlemleri Category içinde uyguluyoruz.

Not: Direk Repository’i kullanmamýzýn sebebi; Business katmanýnda yeni parametreler gelebilir.  Bu yüzden Repository’nin kendisi kullanýlmaz. Örneðin; Bütün Ürünlerimizi Listelerken, Yeni bir iþ kuralý gelir Id sine göre deðil isimlerine göre listelemek gibi ve buna göre bütün Listeleme kurallarýný deðiþtirmemiz ve buna uygun parametre yazmamýz gerekebilir. Bu yüzden ayýrýyoruz.

