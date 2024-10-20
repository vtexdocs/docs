---
title: "orderForm"
slug: "orderform-fields"
hidden: false
createdAt: "2020-09-02T13:59:41.676Z"
updatedAt: "2022-10-27T19:51:49.586Z"
---
The `orderForm` is the main object processed by VTEX checkout, and one of the most important data structures in the architecture of every VTEX store.

It stores a lot of contextual information about the order which is important to the processing of the order: order items, client's personal data, delivery address, freight information, etc. 

Using VTEX APIs this information can be accessed, processed, and even changed on certain occasions. 

VTEX's Checkout API is one of the main interfaces interacting with the `orderForm` object. Most of its operations will return the `orderForm` or part of it.

The object's basic structure is:

```json
{
  "allowManualPrice": boolean,
  "canEditData": boolean,
  "clientPreferencesData": {},
  "clientProfileData": {},
  "commercialConditionData": {},
  "customData": {},
  "giftRegistryData": {},
  "hooksData": {},
  "ignoreProfileData": boolean,
  "isCheckedIn": boolean,
  "itemMetadata": {},
  "items": {},
  "itemsOrdination": {},
  "loggedIn": boolean,
  "marketingData": {},
  "messages": [],
  "openTextField": {},
  "orderFormId": string,
  "paymentData": {},  
  "ratesAndBenefitsData": {},
  "salesChannel": "1",
  "selectableGifts": {},
  "sellers": {},
  "shippingData": {},
  "storeId": {},
  "storePreferencesData": {},
  "totalizers": {},
  "userProfileId": {},
  "userType": {},
  "value": number
}
```

This structure is made of many __sections__.

>⚠️ Any properties representing monetary values will have __cents__ as their units. (e.g. `10390` means __R$103,90__ in Brazilian stores). In the following menu, you can find details regarding these sections.

## `OrderForm` Sections

- [clientPreferencesData](#clientpreferencesdata)
- [clientProfileData](#clientprofiledata)
- [commercialConditionData](#commercialconditiondata)
- [customData](#customdata)
- [giftRegistryData](#giftregistrydata)
- [hooksData](#hooksdata)
- [items](#items)
    - [items[].priceDefinition](#itemspricedefinition)
    - [items[].attachmentOfferings](#itemsattachmentofferings)
- [invoiceData](#invoicedata)
- [itemsOrdination](#itemsordination)
- [marketingData](#marketingdata)
- [messages](#messages)
- [openTextField](#opentextfield)
- [paymentData](#paymentdata)
- [ratesAndBenefitsData](#ratesandbenefitsdata)
- [selectableGifts](#selectablegifts)
- [sellers](#sellers)
- [shippingData](#shippingdata)
- [storeId](#storeid)
- [storePreferencesData](#storepreferencesdata)
- [subscriptionData](#subscriptiondata)
- [totalizers](#totalizers)

### clientPreferencesData

Object containing preferences from the client who placed the order.

__Example:__

```json
{
  "locale": "pt-BR",
  "optinNewsLetter": true
}
```

| Field     | Type     | Description     |
| ---------- | ---------- | ---------- |
| locale       | String       | Client's locale. Examples: `"pt-BR"` and `"en-US"`. The method `sendLocale()`, from vtex.js, changes the value of this field.       |
| optinNewsLetter       | Boolean       | `true` if the client opted to receive newsletters from the store.       |

### clientProfileData

Object containing the data of the customer who placed the order.

If the customer has not yet informed her or his email, much of the data may be empty (`null`).

If the customer's email has not yet been confirmed, several personal data will be censored, that is, some of its parts will be hidden by asterisks to avoid identification.

__Example:__

```json
{
  "email": "customer@mailprovider.com",
  "firstName": "Bre******",
  "lastName": "Bar******",
  "document": "*1*2*5*5*3*",
  "documentType": "cpf",
  "phone": "******0879",
  "corporateName": null,
  "tradeName": null,
  "corporateDocument": null,
  "stateInscription": null,
  "corporatePhone": null,
  "isCorporate": false
}
```

| Field      | Type      | Description |
| ---------- | ---------- | ---------- |
|      email      |    String    |  Customer's email.      |
|   firstName         |     String       |  Customer's first name.     |
|    lastName        |   String         |   Customer's last name.      |
|   document         |   String         |  Document number informed by the customer.          |
|   documentType         |   String         |  Type of the document informed by the customer.          |
|   phone         |     String       |   Customer's phone number.    |
|    corporateName        |  String          |     If it's a legal entity, here goes the company name.       |
|  tradeName          |  String          |     If legal entity, here goes the trade name.       |
|  corporateDocument          |      String      |   If legal entity, here goes the corporate document.         |
|   stateInscription         |    String        |   If legal entity, here goes the state inscription.         |
|   corporatePhone         |    String        |   If legal entity, here goes the company phone.        |
|   isCorporate         |     Boolean       |  It has the value `true` if it's a legal entity.         |

### commercialConditionData

>⚠️ This guide is currently being written and published as content becomes available.

### customData

During the checkout process, some stores need to include data gathered from the client that is not part of our standard `orderForm` format (e.g. gender, cell phone number, age).

To do that you will need to create extra fields in the `orderForm` and those will be located inside the `customData` parameter.

__Example:__

```json
"customData": {
	"attachmentId": "customData",
	"customApps": [
		{
			"fields": {
				"number": "78550693",
				"street": "Rua Voluntários da Pátria",
				"complement": "Em frente à Torre Citi",
				"name": "101 - Delco Autopista",
				"neighborhood": "Botafogo",
				"city": "Rio de Janeiro",
				"state": "RJ"
			},
			"id": "pickupinfo",
			"major": 1
		},
		{
			"fields": {
				"deliveryEstimate": "30"
			},
			"id": "deliveryinfo",
			"major": 1
		}
	]
}
```

| Field      | Type      | Description |
| ---------- | ---------- | ---------- |
|    customApps |    Array  |  Array containing the apps created by the store.      |
|    fields |    Object  |  Object that contains the fields created by the store for each app.      |
|    id   |    String   |   App ID.      |
|    major   |   Integer     |  App major version.         |

### giftRegistryData

Object containing the gift registration list data.

__Example:__

```json
{
  "giftRegistryId": "22222",  
  "giftRegistryType": null,
  "giftRegistryTypeName": null,
  "addressId": null,
  "description": "gift1"    
}
```

| Field      | Type      | Description |
| ---------- | ---------- | ---------- |
|    giftRegistryId |    String  |  Gift registry ID.      |
|    giftRegistryType |    String  |  Gift registry type.      |
|    giftRegistryTypeName   |    String   |   Gift registration typen name.       |
|    addressId   |    String   |   Address ID.      |
|    description   |    String   |   Gift registry description.      |

### hooksData

>⚠️ This guide is currently being written and published as content becomes available.

### items

it is an array containing an object describing every item in the buyer's cart.

__Example:__

```json
"items": [
        {
            "uniqueId": "3B31329E5DDA4A1A81449DD7466D9575",
            "id": "4",
            "productId": "3",
            "productRefId": "",
            "refId": null,
            "ean": "978073487962",
            "name": "Mild Hair Cleanser 50 ml",
            "skuName": "50 ml",
            "modalType": null,
            "parentItemIndex": null,
            "parentAssemblyBinding": null,
            "priceValidUntil": "2022-04-07T18:31:11Z",
            "tax": 0,
            "taxCode":"54WC8ZN6K8",
            "price": 3190,
            "listPrice": 3190,
            "manualPrice": 1700,
            "manualPriceAppliedBy": "in542e51-5863-4c34-8i86-ed8fcf597a09",
            "sellingPrice": 1700,
            "rewardValue": 0,
            "isGift": false,
            "additionalInfo": {
                "dimension": null,
                "brandName": "VALCOSMETICS",
                "brandId": "2000000",
                "offeringInfo": null,
                "offeringType": null,
                "offeringTypeId": null
            },
            "preSaleDate": null,
            "productCategoryIds": "/2/",
            "productCategories": {
                "2": "Computers"
            },
            "quantity": 3,
            "seller": "seller1",
            "sellerChain": [
                "seller1"
            ],
            "imageUrl": "http://cosmeticsstore.vteximg.com.br/arquivos/ids/155401-55-55/ID-001-MAIN.jpg?v=637109313796670000",
            "detailUrl": "/mild-hair-cleanser/p",
            "bundleItems": [],
            "attachments": [],
            "attachmentOfferings": [
              {
                  "name":"vtex.subscription.weekly",
                  "required":false,
                  "schema":{
                    "vtex.subscription.key.frequency":{
                        "MaximumNumberOfCharacters":7,
                        "Domain":[
                          "1 week",
                          " 2 week",
                          " 3 week",
                          " 4 week"
                        ]
                    }
                  }
              }
            ],
            "offerings": [],
            "priceTags": [
                {
                    "name": "DISCOUNT@MANUALPRICE",
                    "value": -4470,
                    "rawValue": -44.7,
                    "isPercentual": false,
                    "identifier": null
                }
            ],
            "availability": "available",
            "measurementUnit": "un",
            "unitMultiplier": 1.0000,
            "manufacturerCode": null,
            "priceDefinition": {
                "sellingPrice": [
                    {
                        "quantity": 1,
                        "value": 1700
                    }
                ],
                "total": 5100
            }
        }
    ]
```

| Field      | Type      | Description |
| ---------- | ---------- | ---------- |
|    uniqueId |    String  |  Obsolete field. This string is the unique identifier for each occurrence of a SKU in an order. Two units of the same SKU in an order will have different uniqueIds.    |
|    id |    String  |  ID of the item.     |
|    productId   |    String   |   Product ID.       |
|    productRefId   |    String   |   Product Ref ID.      |
|    refId   |    String   |   Ref ID.    |
|    ean |    String  |  EAN (codebar) field from [SKU registry](https://help.vtex.com/pt/tutorial/cadastrar-o-codigo-de-barra-dos-skus-para-o-instore--2jkOdRB4XSMG2ke0uUQIKS#cadastrar-o-campo-ean).      |
|    name |    String  |  Product name.     |
|    skuName |    String  |  SKU name.    |
|    modalType   |    String   |   Modal type.     |
|    parentItemIndex   |    Integer   |   Parent item index.     |
|    parentAssemblyBinding   |    String   |   Parent assembly binding.   |
|    priceValidUntil |    String  |  Price expiration date and time.    |
|    tax |    Integer |  Tax value in cents.    |
|    taxCode |    String|  A unique identifier code assigned to a tax within the VTEX Admin.    |
|    price   |    Integer   |   Price in cents.    |
|    listPrice   |    Integer  |   List price in cents.    |
|    manualPrice   |    Integer  |   Manual price in cents.   |
|    manualPriceAppliedBy |    String  |  User that applied the manual price, if that is the case.    |
|    sellingPrice |    Integer |  Selling price in cents. Note that this field may be subject to rounding discrepancies. We recommend retrieving data from the `priceDefinition` data structure instead.   |
|    rewardValue   |    Integer   |   Reward value in cents.   |
|    isGift   |    Boolean  |   Indicates whether item is a gift.   |
|    additionalInfo   |    Object  |   Additional information. |
|    dimension |    String  |  Dimension.    |
|    brandName |    String |  Brand name.   |
|    brandId |    String |  Brand ID.   |
|    offeringInfo  |    String  |   Offering information.  |
|    offeringType  |    String|   Offering type.   |
|    offeringTypeId  |    String  |   Offering type ID. |
|    preSaleDate |    String  |  Presale date.   |
|    productCategoryIds |    String |  Product category IDs.  |
|    productCategories  |    Object  |   Object, where each field is an ID from `productCategoryIds`.  |
|    {ID}  |    String|   Product category corresponding to the ID in the field key.   |
|    quantity  |    Integer  |   Quantity. |
|    seller |    String  |  Seller information.   |
|    sellerChain |    Array of strings |  Sellers involved in the chain. The list should contain only one seller, unless it is a [Multilevel Omnichannel Inventory](https://help.vtex.com/en/tutorial/multilevel-omnichannel-inventory--7M1xyCZWUyCB7PcjNtOyw4) order.   |
|    imageUrl  |    String  |   Image URL.  |
|    detailUrl  |    String|   Detail URL.   |
|    bundleItems |    Array of objects |   Information on services sold along with the SKU. Example: a gift package. |
|    type |    String  |  Service type.  |
|    id |    Integer |  Service identifier. |
|   name  |    String |   Service name.  |
|    price  |     Integer |   Service price in cents.  |
|    attachments |    Array of strings |   Array containing information on attachments. |
|    priceTags |    Array of objects  |  Array of price tags, each of which, modifies the price in some way, like discounts or rates that apply to the item in the context of the order.  |
|    name  |     String |   Price tag name. |
|    value |    Integer  |  Price tag value.  |
|    rawValue |    Integer |   Price tag raw value. |
|   isPercentual  |    Boolean |   Indicates whether price tag value is applied through a percentage.  |
|    identifier |    String |  Price tag identifier. |
|    owner |    String |  Identification of the responsible for the price tag. |
|    availability |    String |  SKU availability. The values are: `available`, `withoutStock`and `cannotBeDelivered`. Only SKUs with  `available` value can be sold and delivered. |
|   measurementUnit  |    String |   Measurement unit.  |
|    unitMultiplier  |     String |   Unit multiplier. |
|    manufacturerCode |    String |   Manufacturer code. |
|    priceDefinition |    Object  |  Price information for all units of a specific item. |
|    calculatedSellingPrice |    Integer |  Item's calculated unitary selling price in cents. |
|   total  |     Integer |   Total value for all units of the item in cents. |
|    sellingPrices  |     Array of objects |   Array of objects, each containing value (in cents) and quantity for the different rounding instances that can be combined to form the correctly rounded total. |
|    value |    Integer |   Value in cents for that specific rounding. |
|    quantity |    Integer |   Rounding quantity, meaning how many items are rounded to this value. |

>⚠️ If you use integrations that consume price data, such as checkout or order integrations, note that the field `sellingPrice` may be subject to rounding discrepancies. We recommend retrieving data from the `priceDefinition` data structure instead.

#### items[].priceDefinition

```json
{
    "items": [
        {
            "id": "1001669",
            "price": 199,
            "quantity": 3,
            "unitMultiplier": 0.3,
            "measurementUnit": "kg",
            "sellingPrice": 59,
            "priceDefinition": {
                "calculatedSellingPrice": 59,
                "total": 179,
                "sellingPrices": [
                    {
                        "value": 60,
                        "quantity": 2
                    },
                    {
                        "value": 59,
                        "quantity": 1
                    }
                ]
            }
        }
    ]
}
```

| **Atribute**                                   | **Type** | **Description**                                                                                                                                                      |
|------------------------------------------------|----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| items[].priceDefinition                        | Object   | Price information for all units of a specific item.                                                                                                                  |
| items[].priceDefinition.total                  | Integer  | Total value for all units of the item in cents.                                                                                                                      |
| items[].priceDefinition.calculatedSellingPrice | Integer  | Item's calculated unitary selling price in cents.                                                                                                                    |
| items[].priceDefinition.sellingPrices          | Array    | Array of objects, each containing `value` (in cents) and `quantity` for the different rounding instances that can be combined to form the correctly rounded `total`. |

#### items[].attachmentOfferings

```json
"attachmentOfferings":[
  {
      "name":"vtex.subscription.weekly",
      "required":false,
      "schema":{
        "vtex.subscription.key.frequency":{
            "MaximumNumberOfCharacters":7,
            "Domain":[
              "1 week",
              "2 week",
              "3 week",
              "4 week"
            ]
        }
      }
  }
]
```

| **Atribute**                                   | **Type** | **Description**                                                                                                                                                      |
|------------------------------------------------|----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| items[].attachmentOfferings.name                        | string or null   | Name of the attachment.                                                                                                                  |
| items[].attachmentOfferings.required               | boolean or null  |       If the attachment is required (true) or not (false).                                                                                                                |
| items[].attachmentOfferings.schema | object or null  | Schema of the content declared in the field attachmentOfferings.                                                                                                                    |

### invoiceData

This is an object containing information pertinent to the order's invoice.

```json
{
   "address": {
   "postalCode": "******000",
   "city": "Rio ** *******",
   "state": "RJ",
   "country": "BRA",
   "street": "Rua *** *****nte",
   "number": "***",
   "neighborhood": "Bot*****",
   "complement": "*** ** *",
   "reference": null
   },
    "settleInvoices":[]  
}
```

| Field      | Type      | Description |
| ---------- | ---------- | ---------- |
|    address |    Object  |  Address information.      |
|    settleInvoices |    String  |  List of strings corresponding to invoice numbers.      |

### itemsOrdination

This is an object containing information about the ordering of items within the orderForm.

__Example:__

```json
{
  "criteria": "NAME",  
  "ascending": true  
}
```

| Field      | Type      | Description |
| ---------- | ---------- | ---------- |
|    criteria  |    String |  Criteria adopted to order the items in the list. The values are: `NAME`, `ADD_TIME` (date information), and `GIFT` (non-gift items are mentioned before gift items).              |
|    ascending |    String |  Indicates whether the ordering is ascending.              |


### marketingData

This object contains promotion data such as coupon tracking information and internal or external UTMs.

__Example:__

```json
{
  "attachmentId": "marketingData",
  "coupon": null,
  "marketingTags": [],
  "utmCampaign": "christmas",
  "utmMedium": null,
  "utmSource": "fb",
  "utmiCampaign": "",
  "utmiPart": "",
  "utmipage": ""  
}
```

| Field      | Type      | Description |
| ---------- | ---------- | ---------- |
|    attachmentId  |    String |   Attachment ID.     |
|    coupon |    String |   Coupon code information.     |
|    marketingTags |    Array |   Marketing tags information. This field can be used to register campaign data or informative tags regarding promotions.    |
|    utmCampaign  |    String |  Value of the `utm_campaign` parameter of the URL that led to the request.      |
|    utmMedium  |    String |  Value of the `utm_medium` parameter of the URL that led to the request.      |
|    utmSource  |    String |  Value of the `utm_source` parameter of the URL that led to the request.      |
|    utmiCampaign  |    String |  Internal UTM value `utmi_cp`.     |
|    utmiPart  |    String |  Internal UTM value `utmi_pc`.      |
|    utmipage  |    String |  Internal UTM value `utmi_p`.      |

### messages

This array contains an object for each message generated by our servers while processing the request.

__Example:__

```json
[
  {
    "code": null,
    "status": "error",
    "text": "Voucher code AAAA-BBBB-CCCC-DDDD was not found in the system"
  }
]
```

### openTextField

Optional field meant to hold additional information about the order. We recommend using this field for text, not data formats such as `JSON` even if escaped. For that purpose, see [Add and handle custom information in the order](https://developers.vtex.com/docs/guides/add-and-handle-custom-information-in-the-order).

```json
{
    "value": "{\"Phones\":[\"55555555\"]}"
}
```
  
| Field      | Type      | Description |
| ---------- | ---------- | ---------- |
|    value |    String |  Additional information about the order.               |


### paymentData

This object contains all payment information inserted for this purchase.

__Example:__

```json
{
  "giftCards": [
    {
      "redemptionCode": "HYUO-TEZZ-QFFT-HTFR",
      "value": 500,
      "balance": 500,
      "name": null,
      "id": "-1390324156495k195pmab4rall3di",
      "inUse": true,
      "isSpecialCard": false
    }, {
      "redemptionCode": "MTHU-WNTD-VXJW-TIDC",
      "value": 0,
      "balance": 700000,
      "name": "loyalty-program",
      "id": "122",
      "inUse": false,
      "isSpecialCard": true
    }
  ],
  "giftCardMessages": [],
  "availableAccounts": [
    {
      "accountId": "71F2775D46BF44B1BF217F828F4E6131",
      "paymentSystem": "2",
      "paymentSystemName": "Visa",
      "cardNumber": "************1111",
      "availableAddresses": ["-1363804954758", "-1366200971560"]
    }
  ],
  "availableTokens": [],
  "installmentOptions": [
    {
      "paymentSystem": "2",
      "value": 16175,
      "installments": [
        {
          "count": 1,
          "hasInterestRate": false,
          "interestRate": 0,
          "value": 16175,
          "total": 16175
        }, {
          "count": 2,
          "hasInterestRate": false,
          "interestRate": 132,
          "value": 4178,
          "total": 16712
        }
      ]
    }
  ],
  "paymentSystems": [
    {
      "id": 2,
      "name": "Visa",
      "groupName": "creditCardPaymentGroup",
      "validator": {
        "regex": "^4",
        "mask": "9999 9999 9999 9999",
        "cardCodeRegex": "[^0-9]",
        "cardCodeMask": "999",
        "weights": [2, 1, 2, 1, 2, 1, 2, 1, 2, 1, 2, 1, 2, 1, 2, 1, 2, 1, 2]
      },
      "stringId": null,
      "template": "creditCardPaymentGroup-template",
      "requiresDocument": false,
      "selected": false,
      "isCustom": false,
      "description": null
    }
  ],
  "payments": [
    {
      "accountId": null,
      "bin": null,
      "installments": 2,
      "paymentSystem": "12",
      "referenceValue": 16175,
      "value": 16175
    }
  ]
}
```

| Field      | Type      | Description |
| ---------- | ---------- | ---------- |
|    giftCards  |    Array  |    Gift cards information.    |
|    giftCardMessages |    Array  |    Gift cards message information.    |
|    availableAccounts |    Array  |    Available accounts information.    |
|    availableTokens  |    Array  |    Available tokes information.    |
|    installmentOptions  |    Array  | For accurate information on installment options and values, we recommend using the [Cart installments endpoint](https://developers.vtex.com/docs/api-reference/checkout-api#get-/api/checkout/pub/orderForm/-orderFormId-/installments), instead of this field's data. |
|    paymentSystems |    Array  |    Payment systems information.    |
|    payments  |    Array  |    Payments information.    |
|    updateStatus    |    String    |    Checkout can not be concluded if value is `"outdated"`.    |

>⚠️ This guide is currently being written and published as content becomes available.

### ratesAndBenefitsData

Information on rates and benefits that apply to the order.

__Example:__

```json
{
   "rateAndBenefitsIdentifiers": [
     {
      "items": {}
     }
  ],
   "teaser":[
     {
      "items": {}
     }
  ]
}
```

| Field      | Type      | Description |
| ---------- | ---------- | ---------- |
|    rateAndBenefitsIdentifiers    |    Array    |    List with rates and benefits identifiers.    |
|    items    |   Object    |    Object that contains identifiers information.    |
|    teaser    |    Array   |    List with rates and benefits teasers.    |
|    items    |    Object   |    Object that contains teasers information.  |


### selectableGifts

Array containing the data of the item selected as a gift.

```json
 [
  {
    "id": null,
    "availableQuantity": "3",
    "availableGifts": {
       "items": [
                 {},
                 "isSelected": true
                ]
   }
  }
 ]
```

| Field      | Type      | Description |
| ---------- | ---------- | ---------- |
|    id    |    String    |    Identification of the selectable gifts list.    |
|    availableQuantity    |    Integer   |    Number of items available.    |
|    items   |    Integer   |    Array containing an object describing each item that can be selected as a gift.    |
|    isSelected    |    Boolean   |    Indication if the item was selected as a gift.    |


### sellers

An array containing an object for each seller being used in the order.

__Example:__

```json
[
  {
    "id": "1",
    "name": "meuamigopet",
    "logo": "http://portal.vtexcommerce.com.br/arquivos/logo.jpg"
  }
]
```

| Field      | Type      | Description |
| ---------- | ---------- | ---------- |
|    id  |    String  |   ID of the seller.     |
|    name |    String  |   Name of the seller.     |
|    logo  |    String  |  URL pointing to where the image is hosted.     |


### shippingData

This object contains shipping information for the order.

__Example:__

```json
{
  "attachmentId": "shippingData",
  "address": {
    "addressType": "residential",
    "receiverName": "Gui***rme",
    "addressId": "-1368194386810",
    "postalCode": "******000",
    "city": "Rio ** *******",
    "state": "RJ",
    "country": "BRA",
    "street": "Rua *** *****nte",
    "number": "***",
    "neighborhood": "Bot*****",
    "complement": "*** ** *",
    "reference": null
  },
  "availableAddresses": [
    {
      "addressType": "residential",
      "receiverName": "Gui***rme",
      "addressId": "-1368194386810",
      "postalCode": "******000",
      "city": "Rio ** *******",
      "state": "RJ",
      "country": "BRA",
      "street": "Rua *** *****nte",
      "number": "***",
      "neighborhood": "Bot*****",
      "complement": "*** ** *",
      "reference": null
    }
  ],
  "logisticsInfo": [
    {
      "itemIndex": 0,
      "selectedSla": ".Transportadora",
      "selectedDeliveryChannel": "delivery",
      "addressId": "teste",
      "slas": [
        {
          "id": ".Transportadora",
          "deliveryChannel": "delivery",
          "name": ".Transportadora",
          "deliveryIds": [
            {
              "courierId": "67",
              "warehouseId": "1_1",
              "dockId": "1_1_1",
              "courierName": "Transportadora",
              "quantity": 1
            }
          ],
          "shippingEstimate": "3d",
          "shippingEstimateDate": "2023-09-09T11:29:00+00:00",
          "lockTTL": null,
          "availableDeliveryWindows": [],
          "deliveryWindow": null,
          "price": 956,
          "tax": 0
        }, {
          "id": "Agendada",
          "name": "Agendada",
          "deliveryIds": [
            {
              "courierId": "FA02F72F-FEBD-41A0-AF70-83A77E8C77A0",
              "warehouseId": "1_1",
              "dockId": "1_1_1",
              "courierName": "Entrega agendada",
              "quantity": 1
            }
          ],
          "shippingEstimate": "90d",
          "shippingEstimateDate": "2023-09-09T11:29:00+00:00",
          "lockTTL": null,
          "availableDeliveryWindows": [
            {
              "startDateUtc": "2014-04-21T09:00:00+00:00",
              "endDateUtc": "2014-04-21T12:00:00+00:00",
              "listprice": 1000,
              "tax": 0
            }, {
              "startDateUtc": "2014-04-21T13:00:00+00:00",
              "endDateUtc": "2014-04-21T17:00:00+00:00",
              "listprice": 1000,
              "tax": 0
            }
          ],
          "deliveryWindow ": [
            {
              "startDateUtc": "2014-04-21T09:00:00+00:00",
              "endDateUtc": "2014-04-21T12:00:00+00:00",
              "listprice": 1000,
              "tax": 0
            }, {
              "startDateUtc": "2014-04-21T13:00:00+00:00",
              "endDateUtc": "2014-04-21T17:00:00+00:00",
              "listprice": 1000,
              "tax": 0
            }
          ],
          "price": 1220,
          "tax": 0,
          "pickupStoreInfo": {
              "isPickupStore": false,
              "friendlyName": null,
              "address": null,
              "additionalInfo": null,
              "dockId": null
            },
            "pickupPointId": null,
            "pickupDistance": 0,
            "polygonName": null,
            "transitTime": "3bd"
          }
        ],
         "shipsTo": [
           "BRA",
           "COL",
           "USA"
        ],
         "itemId": "2",
         "deliveryChannels": [
           {
             "id": "delivery"
           },
           {
             "id": "pickup-in-point"
           }
         ]
       }
      ],
  "selectedAddresses": []
}
```

| Field      | Type      | Description |
| ---------- | ---------- | ---------- |
|    attachmentId  |    String  |   Attachment ID.     |
|    address  |    Object  |   Address information.     |
|    availableAddresses  |    Array  |   Information about available shipping addresses.    |
|    logisticsInfo  |    Array  |   Logistics information.     |
|    itemIndex  |    Integer  |   Index corresponding to the position of the object in the `items` array.     |
|    selectedSla  |    String  |   SLA selected by the customer.     |
|    selectedDeliveryChannel  |    String  |   Delivery channel selected by the customer.     |
|    addressId  |    String  |   Address ID.    |
|    slas |    Array  |   Information on available SLAs.     |
|    id |    String  |   SLA ID.    |
|    deliveryChannel |    String  |   Delivery channel.    |
|    name |    String  |   SLA name.    |
|    deliveryIds |    Array  |   Information on each delivery ID.    |
|    courierId |    String  |   Courier ID.    |
|    warehouseId |    String  |   Warehouse ID.    |
|    dockId |    String  |   Dock ID.    |
|    courierName |    String  |   Courier name.   |
|    quantity |    Integer  |   Quantity.   |
|    shippingEstimate |    String  | Total shipping estimate time, represented by a number followed by a time unit. For instance, three business days is represented as `3bd`. The time unit can be one of the following: <ul><li><code>m</code> (minutes)</li><li><code>h</code> (hours)</li><li><code>bd</code> (business days)</li><li><code>d</code> (days)</li></ul> |
|    shippingEstimateDate |     String  |   When using the query parameter `individualShippingEstimates=true`, it will contain the estimated shipping date, otherwise it will contain `null`.  |
|    lockTTL |     String  |   Estimate date of delivery.  |
|    availableDeliveryWindows |     String  |   Available shipping date.  |
|    startDateUtc |     String  |   Available delivery window start date in UTC.  |
|    endDateUtc |     String  |   Available delivery window end date in UTC.  |
|    deliveryWindow |     Object  |   Scheduled delivery window information, in case it applies to the item.  |
|    startDateUtc |     String  |   Scheduled delivery window start date in UTC.  |
|    endDateUtc |     String  |   Scheduled delivery window end date in UTC.  |
|    listPrice |     Integer  |   Scheduled delivery window list price.  |
|    price |     Integer  |   Price in cents.  |
|    tax |     Integer  |   Tax in cents.  |
|    pickupStoreInfo |     Object  |   Information on the pickup store.  |
|    isPickupStore |     Boolean  |   Indicates whether it is the pickup store.  |
|    friendlyName |     String  |   Friendly name.  |
|    address |     Object  |   Address information.  |
|    additionalInfo |     String  |   Additional information.  |
|    dockId |     String  |   Corresponding dock ID.  |
|    pickupPointId |     String  |   Pickup point ID.  |
|    pickupDistance |     Integer  |   Pickup point distance.  |
|    polygonName |     String  |   Polygon name.  |
|    transitTime |     String  |   Transit time. For instance, "three business days" is represented `3bd`.  |
|    shipsTo |     Array  |   List of countries that the item may be shipped to.  |
|    itemId |     String  |   Item ID.  |
|    deliveryChannels |     String  |   List of available delivery channels.  |
|    id |     String  |   Delivery channel ID.  |
|    selectedAddresses  |    Array  |   Selected addresses information.     |

### storeId

It is a string containing the store ID.

__Example:__

```json
{
    "storeId": "2"
}
```

| Field      | Type      | Description |
| ---------- | ---------- | ---------- |
|    storeId  |    integer  |   Identification of the store.    |

### storePreferencesData

This object contains data from the store's configuration.

__Example:__

```json
{
  "countryCode": "BRA",
  "saveUserData": true,
  "templateOptions": {
    "toggleCorporate": false
  },
  "timeZone": "E. South America Standard Time",
  "currencyCode": "BRL",
  "currencyLocale": 0,
  "currencySymbol": "R$",
  "currencyFormatInfo": {
    "currencyDecimalDigits": 2,
    "currencyDecimalSeparator": ",",
    "currencyGroupSeparator": ".",
    "currencyGroupSize": 3,
    "startsWithCurrencySymbol": true
  }
}
```

### totalizers

This array contains an object for each totalizer for the purchase. Totalizers contain the sum of values for a specific part of the order (e.g. Total item value, Total shipping value).

__Example:__

```json
[
  {
    "id": "Items",
    "name": "Total items",
    "value": 35620
  },
  {
    "id": "Shipping",
    "name": "Total freight",
    "value": 399
  }
]
```
