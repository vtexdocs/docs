title: "Teste - Conversão Markdwon"

slug: "markdown-new-file"

hidden: false

createdAt: "2024-04-08T00:00:15.623Z"

updatedAt: ""

Título Principal

# Título Nível 1

## Título Nível 2

### Título Nível 3

#### Título Nível 4

Para se tornar um provedor VTEX integrado , é necessário utilizar uma das seguintes soluções:

* A infraestrutura **onde o conector será construído** precisa ter o certificado PCI-DSS assinado por um QSA (Qualified Security Assessor). Maiores informações no [Conselho de Normas de Segurança do PCI](https://www.pcisecuritystandards.org/).
* Caso não possua o certificado, implementar o provedor utilizando o [Secure Proxy](https://developers.vtex.com/docs/guides/payments-integration-secure-proxy).

1. A infraestrutura onde o **conector será construído** precisa ter o certificado PCI-DSS assinado por um QSA *(Qualified Security Assessor)*. Maiores informações no [Conselho de Normas de Segurança do PCI](https://www.pcisecuritystandards.org/).
2. Caso não possua o certificado, implementar o provedor utilizando o [Secure Proxy](https://developers.vtex.com/docs/guides/payments-integration-secure-proxy).

```json

[

    {

        "cardId": "92de2449-0e02-4ca9-a4aa-a09cc9d8f7ff_74",

        "id": "c2b69a5990404a11b26888964bed3868",

        "_self": {

            "href": "cosmetics2/giftcards/92de2449-0e02-4ca9-a4aa-a09cc9d8f7ff_74/transactions/c2b69a5990404a11b26888964bed3868"

        }

    },

    {

        "cardId": "92de2449-0e02-4ca9-a4aa-a09cc9d8f7ff_74",

        "id": "465f2d7370f349879f4c194ac81d8e98",

        "_self": {

            "href": "cosmetics2/giftcards/92de2449-0e02-4ca9-a4aa-a09cc9d8f7ff_74/transactions/465f2d7370f349879f4c194ac81d8e98"

        }

    }

]
```

|
|Coluna 1|Coluna 2|Coluna 3|Coluna 4|Coluna 5|
|Linha 1 x Coluna 1||Linha 1 x Coluna 3||Linha 1 x Coluna 5|
||Linha 2 x Coluna 2||Linha 2 x Coluna 4|

**Se o provedor for certificado ou já iniciou o processo de certificação, é possível entrar em contato com a equipe de negócios da VTEX para começar a integração.**

O provedor deve encaminhar à VTEX, o [AOC](https://www.pcisecuritystandards.org/document_library) (Attestation of Compliance for Onsite Assessments – Service Provider Version) totalmente preenchido, observando os seguintes pontos:

* **Nome da empresa**: o campo "URL" (Parte 1a.) deve ser o mesmo da empresa que está solicitando o procedimento de integração. Caso seja preenchido com outro nome (exemplo: empresa adquirida por outra), será necessário encaminhar a documentação extra que comprove a relação entre as empresas, e que a URL de serviço do provedor foi avaliada pelo PCI DSS.
* **Assinatura**: Documento assinado pelo representante da empresa e pelo QSA.
* **Data de expiração**: a validade do AOC é de 1 ano após a data de assinatura. Um AOC emitido a mais de 11 meses não deve ser encaminhado à VTEX, ou seja, com tempo inferior a 30 dias para a data de expiração.

> ❗ Os documentos SAQ (Self-Assessment Questionnaire) e AOC (Attestation of Compliance for Onsite Assessments – Merchants Version) não são aceitos no processo de integração da VTEX.

> ℹ️ [Provedores de pagamentos com boletos, promissórias ou cartões de loja com bandeira própria (Private Label ou cartões em geral, mas que envolvam soluções com redirect)](https://help.vtex.com/pt/tutorial/payment-provider-protocol--RdsT2spdq80MMwwOeEq0m?&utm_source=autocomplete#provedores-de-pagamentos-com-boletos-promissorias-ou-cartoes-de-loja-com-bandeira-propria-private-label-ou-cartoes-em-geral-mas-que-envolvam-solucoes-com-redirect)

> ⚠️ O provedor deve encaminhar à VTEX, o [AOC](https://www.pcisecuritystandards.org/document_library) (Attestation of Compliance for Onsite Assessments – Service Provider Version) totalmente preenchido, observando os eguintes pontos:

![](https://raw.githubusercontent.com/vtexdocs/.jpg)
