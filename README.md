# solid-principles-example 
## Medium makalemi okuyunuz lütfen: 

SOLID Principle(Solid Prensipler)
SOLID nedir?
SOLID yazılımda sürdürülebilirliği desteklemek adına kullanılan prensiplerdir.
5 tane temel prensiptir.

SOLID açılımı:
Single Responsibility Principle
Open Closed Principle
Liskov’s Substitution Principle
Interface Seggregation Principle
Dependency Inversion Principle

SOLID’ın amacı nedir?
Amacımız yazılımda sürdürülebilirliği sağlamaktır.

Dipnot: Biz bir inşaat projesi yaptığımızı düşünelim. 5. katı çıktığımızda salonla mutfağın yerini değiştirelim diyemiyoruz.
Ama yazılım öyle değil.

Single Responsibility Principle(Tek Sorumluluk İlkesi) :
Bir metot, if bloğu, bir class, bir katman, yani program modülleri bunların tamamı sadece ve sadece bir iş yapmak zorundadır. Her program modülünün aslında tek bir görevi yahut sorumluluğu vardır.

Open Closed Principle(Açık Kapalı İlke) :
Projemiz, içerisindeki nesneler ve proje kodları geliştirilmeye açık fakat değişime kapalıdır.
Uygulamalar yeni özellik eklemeye açık olmalıdır.
Yeni eklenen özellikler mevcut kodu değiştirilerek yahut silinip yeniden yazılarak yapılmamalıdır. Sürekli üzerine yeni özellikleri kodlar ile ekleyerek yapılmalıdır.

Liskov’s Subsitution Principle(Liskov’un İkame İlkesi):
Örnekli anlatımı: Bir havuzda yüzen gerçek ördek birde oyuncak ördek. İki farklı tür. Biri oyuncak ördek diğeri gerçek ördek. Bunların ikisi aynı soyutlama mekanizmasıyla soyutlanmamalıdır. Çünkü birisinin pile ihtiyacı varken diğerinin yeme ihtiyacı vardır. Bunların ikisi aynı şey değildir. Benziyor gibi duruyorlar ama aynı değildir.!

Gerçek hayat örnekli anlatımı: Bir işletme düşün. İki tip müşteri var. Birisi şahıslar diğeri ise şirketler. Şirketin ünvanı var şahısın ise ismi var. Kişi müşteriler diye bir tablo yapıp müşteri adını ve şirket adını aynı yerde tutuyum diye düşünüyor. Kişi adını ve soyadını giriyor. Ad kolonuna ad, soyad kolonuna soyad giriliyor. Şirket kaydı girilirken ad kolonuna şirket adı, soyad kolonuna boş giriliyor yahut soyadı olan bir şirket adı girilebiliyor. Bu durum saçma sapan bir şeye dönüşüyor. Bunun böyle olmaması gerekiyor. Böyle durumlara veri kaçağı deniyor. Veritabanı bütünlüğünü bozuyor. Müşteriler temel tablosu yapıp ortak özellikleri bunun içinde, bir tane gerçek şahıs müşteri tablosu yapıp müşteri ortak tablosundan inheritance yapıp diğerini de tüzel müşteri tablosunuda müşteriler temel tablosundan inheritance ederiz. O şekilde kayıtları gireriz.

Veritabanın da örnek olarak gösterilebilecek temsili resim:


Interface Segregation Principle(Interface’leri(Arayüzleri) Ayırma Prensibi): Bu prensip anlaması en kolay uygulaması en zor prensiptir.
Bu prensipte olay şudur:
Bir Interface kendisini implemente eden bir Class’ın bellek referansını elinde tutabiliyor. Interfacelerin doğru parçalara ayrılması olayıdır.

Örnek bir Java kodu:

interface IBankConnector{
 void Op();
 void Op2();
}
interface IXBankConn : IBankConnector{
 void Op3()
}
interface IYBankConn : IBankConnector{
 void oOp4()
}
class ABank : IYBankConnector{
 void Op(){
  // burada kod var
 }
 void Op2(){
  //burada kod var
 }
 void Op4(){
  //burada kod var
 }
}

class BBank : IXBankConnector{
 void Op(){
  // burada kod var
 }
 void Op2(){
  //burada kod yok..!!!!!!!
 }/////burası kukla(dummy code) kod oldu gereksiz yere..!
void Op3(){
  //burada kod var
 }
}
Dependency Inversion Principle(Bağımlılık Tersine Çevirme Prensibi):
Yüksek seviyeli sınıfların düşük seviyeli sınıfları somut haliyle değil de soyut halleriyle kullanmasıdır. Buda bağımlılığı düşürüyor.
Bu prensipte temel olarak bir tasarım şablonu kullanılır. Bu tasarım şablonu Dependency Injection’dır.
CI(Constructor Injection),
SI(Setter Injection),
MI(Metot Injection).

Dependency Injection desenini ayağa kaldırmak için IoC Container’lerdan yararlanırız. IoC Container nedir araştırınız ödev. (:

Örnek bir C# kodu:

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Ninject;
namespace DependencyInjection
{
    class Program
    {
        static void Main(string[] args)
        {
            IKernel kernel =new StandardKernel();
            kernel.Bind<IProductDal>().To<NhProductDal>().InSingletonScope();
ProductManager productManager=new ProductManager(kernel.Get<IProductDal>());
            productManager.Save();
            Console.ReadLine();
        }
    }
interface IProductDal
    {
        void Save();
    }
    class EfProductDal:IProductDal
    {
        public void Save()
        {
            Console.WriteLine("Saved with Ef");
        }
    }
class NhProductDal : IProductDal
    {
        public void Save()
        {
            Console.WriteLine("Saved with Nh");
        }
    }
class ProductManager
    {
        private IProductDal _productDal;
public ProductManager(IProductDal productDal)
        {
            _productDal = productDal;
        }
public void Save()
        {
            //Business Code
            _productDal.Save();
        }
    }
}
Özet:

SOLID Yazılım geliştirme prensipleri.

 ➡️ Tek Sorumluluk İlkesi
    Her sınıfın tek bir amacı olmalıdır,
    ve aşırı işlevsellikle doldurulmamalıdır.

 ➡️ Açık Kapalı
    Sınıflar gelişime açık olmalı,
    modifikasyona/değiştirilmeye/bozulmaya kapalı olmalıdır.

    Başka bir deyişle, yeniden yazmak zorunda kalmamalısınız.
    yeni özellikleri uygulamak için mevcut bir sınıf değişmemelidir.

 ➡️ Arayüz Ayrımı
    Arayüzler sınıfları uygulamaya zorlamamalıdır. Gereksiz içi boş
    metot(kukla metot(dummy method)) oluşmuş ise o boş metotlar
    farklı interface'ye ayrılıp implemente edilmelidir.
    Kısacası Büyük arayüzler küçüklere bölünmelidir.

 ➡️ Bağımlılık Tersine Çevirme
    Bileşenler soyutlamalara bağlı olmalıdır,
    somutlara bağlı olmamalıdır.
NHibernate nedir?

Ninject nedir?

SingletonScope nedir?

Araştırınız ödev. (: