---
description: 'Saiba mais sobre: como criar um serviço que retorna dados arbitrários usando o modelo de programação do WCF Web HTTP'
title: 'Como: criar um serviço que retorna dados arbitrários usando o modelo de programação HTTP Web do WCF'
ms.date: 03/30/2017
ms.assetid: 0283955a-b4ae-458d-ad9e-6fbb6f529e3d
ms.openlocfilehash: aeb03e0dad6c63c463db419027f5556922b2f160
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99793526"
---
# <a name="how-to-create-a-service-that-returns-arbitrary-data-using-the-wcf-web-http-programming-model"></a>Como: criar um serviço que retorna dados arbitrários usando o modelo de programação HTTP Web do WCF

Às vezes, os desenvolvedores devem ter controle total de como os dados são retornados de uma operação de serviço. Esse é o caso quando uma operação de serviço deve retornar dados em um formato sem suporte pelo WCF. Este tópico discute o uso do modelo de programação do WCF WEB HTTP para criar um serviço desse tipo. Esse serviço tem uma operação que retorna um fluxo.  
  
### <a name="to-implement-the-service-contract"></a>Para implementar o contrato de serviço  
  
1. Defina o contrato de serviço. O contrato é chamado `IImageServer` e tem um método chamado `GetImage` que retorna um <xref:System.IO.Stream> .  
  
    ```csharp  
    [ServiceContract]  
        public interface IImageServer  
        {  
            [WebGet]  
            Stream GetImage(int width, int height);  
        }  
    ```  
  
     Como o método retorna um <xref:System.IO.Stream> , o WCF assume que a operação tem controle total sobre os bytes retornados da operação de serviço e não aplica formatação aos dados retornados.  
  
2. Implemente o contrato de serviço. O contrato tem apenas uma operação ( `GetImage` ). Esse método gera um bitmap e, em seguida, salva-o em um <xref:System.IO.MemoryStream> formato no. jpg. Em seguida, a operação retorna esse fluxo para o chamador.  
  
    ```csharp
    public class Service : IImageServer
    {
        public Stream GetImage(int width, int height)
        {
            Bitmap bitmap = new Bitmap(width, height);
            for (int i = 0; i < bitmap.Width; i++)
            {
                for (int j = 0; j < bitmap.Height; j++)
                {
                    bitmap.SetPixel(i, j, (Math.Abs(i - j) < 2) ? Color.Blue : Color.Yellow);
                }
            }
            MemoryStream ms = new MemoryStream();
            bitmap.Save(ms, System.Drawing.Imaging.ImageFormat.Jpeg);
            ms.Position = 0;
            WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";
            return ms;
        }
    }
    ```  
  
     Observe a segunda para a última linha de código: `WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";`  
  
     Isso define o cabeçalho de tipo de conteúdo como `"image/jpeg"` . Embora este exemplo mostre como retornar um arquivo. jpg, ele pode ser modificado para retornar qualquer tipo de dados necessário, em qualquer formato. A operação deve recuperar ou gerar os dados e, em seguida, gravá-los em um fluxo.  
  
### <a name="to-host-the-service"></a>Para hospedar o serviço  
  
1. Crie um aplicativo de console para hospedar o serviço.  
  
    ```csharp
    class Program  
    {  
        static void Main(string[] args)  
        {  
        }
    }  
    ```  
  
2. Crie uma variável para conter o endereço base para o serviço dentro do `Main` método.  
  
    ```csharp
    string baseAddress = "http://" + Environment.MachineName + ":8000/Service";  
    ```  
  
3. Crie uma <xref:System.ServiceModel.ServiceHost> instância para o serviço especificando a classe de serviço e o endereço base.  
  
    ```csharp
    ServiceHost host = new ServiceHost(typeof(Service), new Uri(baseAddress));  
    ```  
  
4. Adicione um ponto de extremidade usando o <xref:System.ServiceModel.WebHttpBinding> e o <xref:System.ServiceModel.Description.WebHttpBehavior> .  
  
    ```csharp  
    host.AddServiceEndpoint(typeof(IImageServer), new WebHttpBinding(), "").Behaviors.Add(new WebHttpBehavior());  
    ```  
  
5. Abra o host do serviço.  
  
    ```csharp  
    host.Open();  
    ```  
  
6. Aguarde até que o usuário pressione ENTER para encerrar o serviço.  
  
    ```csharp
    Console.WriteLine("Service is running");  
    Console.Write("Press ENTER to close the host");  
    Console.ReadLine();  
    host.Close();  
    ```  
  
### <a name="to-call-the-raw-service-using-internet-explorer"></a>Para chamar o serviço bruto usando o Internet Explorer  
  
1. Execute o serviço, você deverá ver a seguinte saída do serviço. `Service is running Press ENTER to close the host`  
  
2. Abra o Internet Explorer e digite-o para `http://localhost:8000/Service/GetImage?width=50&height=40` ver um retângulo amarelo com uma linha diagonal azul no centro.  
  
## <a name="example"></a>Exemplo  

 A seguir está uma lista completa do código para este tópico.  
  
```csharp  
using System;  
using System.Collections.Generic;  
using System.Text;  
using System.ServiceModel;  
using System.ServiceModel.Web;  
using System.ServiceModel.Description;  
using System.IO;  
using System.Drawing;  
  
namespace RawImageService  
{  
    // Define the service contract  
    [ServiceContract]  
    public interface IImageServer  
    {  
        [WebGet]  
        Stream GetImage(int width, int height);  
    }  
  
    // implement the service contract  
    public class Service : IImageServer  
    {  
        public Stream GetImage(int width, int height)  
        {  
            // Although this method returns a jpeg, it can be  
            // modified to return any data you want within the stream  
            Bitmap bitmap = new Bitmap(width, height);  
            for (int i = 0; i < bitmap.Width; i++)  
            {  
                for (int j = 0; j < bitmap.Height; j++)  
                {  
                    bitmap.SetPixel(i, j, (Math.Abs(i - j) < 2) ? Color.Blue : Color.Yellow);  
                }  
            }  
            MemoryStream ms = new MemoryStream();  
            bitmap.Save(ms, System.Drawing.Imaging.ImageFormat.Jpeg);  
            ms.Position = 0;  
            WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";  
            return ms;  
        }  
    }  
  
    class Program  
    {  
        static void Main(string[] args)  
        {  
            string baseAddress = "http://" + Environment.MachineName + ":8000/Service";  
            ServiceHost host = new ServiceHost(typeof(Service), new Uri(baseAddress));  
            host.AddServiceEndpoint(typeof(IImageServer), new WebHttpBinding(), "").Behaviors.Add(new WebHttpBehavior());  
            host.Open();  
            Console.WriteLine("Service is running");  
            Console.Write("Press ENTER to close the host");  
            Console.ReadLine();  
            host.Close();  
  
        }  
    }  
}  
```  
  
## <a name="compiling-the-code"></a>Compilando o código  
  
- Ao compilar a referência de código de exemplo System.ServiceModel.dll e System.ServiceModel.Web.dll.  
  
## <a name="see-also"></a>Consulte também

- [Modelo de programação WCF Web HTTP](wcf-web-http-programming-model.md)
