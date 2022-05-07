# MomentumSoftKargo
Servisi Bulunan Kargolar
   - Yurtiçi Kargo 
      - Gönderi: http://ahmethamdibayrak.com/api/kargotest/yurtici/kargo 
      - Rapor: http://ahmethamdibayrak.com/api/kargotest/yurtici/info
   - Aras Kargo 
      - Gönderi: http://ahmethamdibayrak.com/api/kargotest/aras/kargo 
      - Rapor: http://ahmethamdibayrak.com/api/kargotest/aras/info
   - MNG Kargo 
      - Gönderi: http://ahmethamdibayrak.com/api/kargotest/mng/kargo 
      - Rapor: http://ahmethamdibayrak.com/api/kargotest/mng/info
   - Sürat Kargo 
      - Gönderi: http://ahmethamdibayrak.com/api/kargotest/surat/kargo 
      - Rapor: http://ahmethamdibayrak.com/api/kargotest/surat/info
   - Ptt Kargo 
      - Gönderi: http://ahmethamdibayrak.com/api/kargotest/ptt/kargo 
      - Rapor: http://ahmethamdibayrak.com/api/kargotest/ptt/info
   
Örnek kod
```csharp
        private string[] kargoTestEt(string firma)
        {
            /**
            CargoGlobalOrderDTO nesnesi oluşturuluyor
            Bu sınıfta nesnenin hangi kargo firması için olduğu bilgisi bulunur
            **/
            CargoGlobalOrderDTO kargo = new CargoGlobalOrderDTO(firma);
            if ( kargo.hangiKargo == CargoGlobalOrderDTO.CargoGlobalCompanies.Empty )
            {
                return new string[] { "Kargo firması geçersiz" };
            }
            /**
            CargoGlobalOrderInfo nesnesi kargo bilgileri için üretiliyor
            Bu sınıfta paketin gönderimiyle ile ilgili bilgiler yer alır yeralır
            **/
            CargoGlobalOrderInfo orderInfo = testOrderInfo();
            CargoGlobalOrderResponse response = kargo.kayitAc( orderInfo);

            return new string[] { kargo.hangiKargo.ToString(), response.isSucceed.ToString(), response.message, response.debug["service_url"], response.debug["request"], response.debug["response"] };

        }
        
        private CargoGlobalOrderInfo testOrderInfo()
        {
            CargoGlobalOrderInfo orderInfo = new CargoGlobalOrderInfo();
            orderInfo.kimOder = CargoGlobalOrderInfo.CargoGlobalPayer.Magaza;
            orderInfo.neTipKargo = CargoGlobalOrderInfo.CargoGlobalPaymentTypes.Normal;
            orderInfo.name = "Alıcı Adı Soyadı";
            orderInfo.email = "test@mailinator.com";
            orderInfo.phone = "05065989387";
            orderInfo.town = "KARTAL";
            orderInfo.city = "İSTANBUL";
            orderInfo.address = "MERKEZ MAHALLESİ HURRİYET SOKAK NO:45/11";
            orderInfo.kargoBarcode = "1";
            orderInfo.orderNumber = "1";
            orderInfo.orderTotal = "125.89";
            orderInfo.desi = "1";
            orderInfo.kilo = "1";
            /**
             * item listesi kargo firmlaranda zorunlu bir alan değildir 
            **/
            CargoGlobalItem item = new CargoGlobalItem();
            item.barcode = "parca-001";
            item.name = "Samsung Telefon Kılıfı";
            item.count = "1";
            item.desi = "1";
            item.kilo = "1";
            orderInfo.items.Add(item);
            return orderInfo;
        }
```
Aras Kargo İçin Test Datası
```xml
      <tem:SetOrder>
         <tem:orderInfo>
            <tem:Order>
               <tem:UserName>*****</tem:UserName>
               <tem:Password>******</tem:Password>
               <tem:TradingWaybillNumber/>
               <tem:ReceiverName>Alıcı Adı Soyadı</tem:ReceiverName>
               <tem:ReceiverAddress>MERKEZ MAHALLESİ HURRİYET SOKAK NO:45/11</tem:ReceiverAddress>
               <tem:ReceiverPhone1>05065989387</tem:ReceiverPhone1>
               <tem:ReceiverPhone2/>
               <tem:ReceiverPhone3/>
               <tem:ReceiverCityName>İSTANBUL</tem:ReceiverCityName>
               <tem:ReceiverTownName>KARTAL</tem:ReceiverTownName>
               <tem:VolumetricWeight/>
               <tem:Weight/>
               <tem:PieceCount>1</tem:PieceCount>
               <tem:SpecialField1/>
               <tem:SpecialField2/>
               <tem:SpecialField3/>
               <tem:CodAmount>0</tem:CodAmount>
               <tem:CodCollectionType/>
               <tem:CodBillingType/>
               <tem:IntegrationCode>1</tem:IntegrationCode>
               <tem:Description>?</tem:Description>
               <tem:TaxNumber/>
               <tem:TtDocumentId/>
               <tem:TaxOffice/>
               <tem:PrivilegeOrder/>
               <tem:Country/>
               <tem:CountryCode/>
               <tem:CityCode/>
               <tem:TownCode/>
               <tem:ReceiverDistrictName>KARTAL</tem:ReceiverDistrictName>
               <tem:ReceiverQuarterName/>
               <tem:ReceiverAvenueName/>
               <tem:ReceiverStreetName/>
               <tem:PayorTypeCode/>
               <tem:IsWorldWide/>
               <tem:IsCod>0</tem:IsCod>
               <tem:UnitID/>
               <tem:PieceDetails>
                  <tem:PieceDetail>
                     <tem:VolumetricWeight/>
                     <tem:Weight/>
                     <tem:BarcodeNumber>1</tem:BarcodeNumber>
                     <tem:ProductNumber>1</tem:ProductNumber>
                     <tem:Description/>
                  </tem:PieceDetail>
               </tem:PieceDetails>
            </tem:Order>
         </tem:orderInfo>
         <tem:userName>*****</tem:userName>
         <tem:password>*****</tem:password>
      </tem:SetOrder>
```
Test Url'si: http://ahmethamdibayrak.com/api/kargotest/aras/kargo
```json
[
"Aras",
"False",
"Sevk adresi bulunamadı.  #1006",
"https://customerws.araskargo.com.tr/arascargoservice.asmx",
"<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:tem="http://tempuri.org/"><soapenv:Header /><soapenv:Body><tem:SetOrder><tem:orderInfo><tem:Order><tem:UserName>****</tem:UserName><tem:Password>****</tem:Password><tem:TradingWaybillNumber></tem:TradingWaybillNumber><tem:ReceiverName></tem:ReceiverName><tem:ReceiverAddress>MERKEZ MAHALLESİ HURRİYET SOKAK NO:45/11</tem:ReceiverAddress><tem:ReceiverPhone1>05065989387</tem:ReceiverPhone1><tem:ReceiverPhone2></tem:ReceiverPhone2><tem:ReceiverPhone3></tem:ReceiverPhone3><tem:ReceiverCityName>İSTANBUL</tem:ReceiverCityName><tem:ReceiverTownName></tem:ReceiverTownName><tem:VolumetricWeight></tem:VolumetricWeight><tem:Weight></tem:Weight><tem:PieceCount>1</tem:PieceCount><tem:SpecialField1></tem:SpecialField1><tem:SpecialField2></tem:SpecialField2><tem:SpecialField3></tem:SpecialField3><tem:CodAmount>0</tem:CodAmount><tem:CodCollectionType></tem:CodCollectionType><tem:CodBillingType></tem:CodBillingType><tem:IntegrationCode>1</tem:IntegrationCode><tem:Description>?</tem:Description><tem:TaxNumber></tem:TaxNumber><tem:TtDocumentId></tem:TtDocumentId><tem:TaxOffice></tem:TaxOffice><tem:PrivilegeOrder></tem:PrivilegeOrder><tem:Country></tem:Country><tem:CountryCode></tem:CountryCode><tem:CityCode></tem:CityCode><tem:TownCode></tem:TownCode><tem:ReceiverDistrictName></tem:ReceiverDistrictName><tem:ReceiverQuarterName></tem:ReceiverQuarterName><tem:ReceiverAvenueName></tem:ReceiverAvenueName><tem:ReceiverStreetName></tem:ReceiverStreetName><tem:PayorTypeCode></tem:PayorTypeCode><tem:IsWorldWide></tem:IsWorldWide><tem:IsCod>0</tem:IsCod><tem:UnitID></tem:UnitID><tem:PieceDetails><tem:PieceDetail><tem:VolumetricWeight></tem:VolumetricWeight><tem:Weight></tem:Weight><tem:BarcodeNumber>1</tem:BarcodeNumber><tem:ProductNumber>1</tem:ProductNumber><tem:Description></tem:Description></tem:PieceDetail></tem:PieceDetails><tem:SenderAccountAddressId>?</tem:SenderAccountAddressId></tem:Order></tem:orderInfo><tem:userName>****</tem:userName><tem:password>****</tem:password></tem:SetOrder></soapenv:Body></soapenv:Envelope>",
"<?xml version="1.0" encoding="utf-8"?><soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema"><soap:Body><SetOrderResponse xmlns="http://tempuri.org/"><SetOrderResult><OrderResultInfo><ResultCode>1006</ResultCode><ResultMessage>Sevk adresi bulunamadı. </ResultMessage><OrgReceiverCustId>1</OrgReceiverCustId></OrderResultInfo></SetOrderResult></SetOrderResponse></soap:Body></soap:Envelope>"
]
```
