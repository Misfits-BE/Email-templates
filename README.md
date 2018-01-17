# Email templates 

**Heb je een issue gevonden die niet gerelateerd is aan de template zelf gelieve dan een bug report aan te maken in de Foundation for Emails](http://github.com/zurb/foundation-emails/issues) repo.**

Onze email templates die worden gebruikt doorheen onze applicaties.
Deze zijn gebouwd op basis van [Zurb Foundation]()

## Features

- Handlebars HTML templates with [Panini](http://github.com/zurb/panini)
- Simplified HTML email syntax with [Inky](http://github.com/zurb/inky)
- Sass compilation
- Image compression
- Built-in BrowserSync server
- Full email inlining process

## Installatie

Om deze templates te gebruiken en of eraan te ontwikkelen moet de computer in kwestie ondersteund zijn met 
[Node.js](https://nodejs.org/en/) versie 0.12 of hoger.

### Gebruik vanaf de CLI

Installeer de Foundation CLI package met het volgende commando: 

```bash
npm install foundation-cli --global
```

Gebruik het volgende commando een leeg Foundation for Email project aan te maken:

```bash
foundation new --framework emails
```

De CLI omgeving zal je vragen voor een project naam. Om vervolgens de templates te downloaden naar een directory die
de gegeven naam draagt.


### Manuale installatie

Voor het project manueel te installeren moet het eerst een clone binnen trekken van de repository. 

```bash
git clone https://github.com/zurb/foundation-emails-template projectname
```

Vervolgens open je de map in uw CLI, en installeer je de nodige dependencies:

```bash
cd projectname
npm install
```

## Generatie commando's

Voer `npm start` uit om een genratie proces in gang te trekken. Een nieuw browser tab zal worden geopend met een server connectie die gericht is naar je project bestanden. 

Voer `npm run build` om al je CSS als inline `style` attributen te weven in de html. Gevolgd door de rest van het generatie proces.

Voer `npm run litmus` uit om de bovenstaande vermelde generatie processen uit te voeren, Om vervolgens litmus te gebruiken als testing provider. *AWS S3 Account informatie is vereist (config.json)*

Voer `npm run mail` uit om de bovenstaande vermelde generatie processen uit te voeren, Daarnaast worden ook de templates naar een specifiek opgegeven email adres verzonden. *SMTP server informatie vereist (config.json)*

Voer `npm run zip` uit om de bovenstaande vermelde generatie processen uit te voeren, Daarnaast worden ook alle template bestanden in een zip bestand comprimeerd voor snelle en gemakkelijke deployment naar Email Marketing Services. 

### Optimalizatie en versnelling van de generatie commando's

Als u een hoop email templates moet genereren kan het proces vertraagd worden. Omdat elke generatie elke template vervangd en opnieuw compileerd. Vandaar dat er een simpele manier us ingebouwd om mails te archieveren. De mails die u niet langer nodig hebt kunnen verplaats worden naar de volgende map. `src/pages/archive`. 

U kunt ook het zelfde doen voor de images. De kunnen verplaatst worden naar de map. `src/assets/img/archieve`. 

Het generatie proces zal vervolgens alle bestanden in de `archive directories` negeren. 

## Litmus Test service (config.json)

Testing in Litmus vereist dat de image bestanden die gebruikt worden publiek gehost worden. Het meegeleverde gulp command gaat er automatisch aan uit dat de foto's op een AWS S3 account staan. Vandaar dat de gegegevens van Litmus en uw AWS S3 account gedefineerd moeten worden in het configuratie bestand. *(Zie `example.config.json`)*. 

Vergeet ook niet de `example.config.json` te hernoemen naar `config.json`. 

Litmus configuratie en `aws.url` zijn vereiste delen. Maar als de [aws-sdk suggesties](http://docs.aws.amazon.com/AWSJavaScriptSDK/guide/node-configuring.html) volgt hoeft u uw AWS credentials niet mee te geven aan de configuratie.

```json
{
  "aws": {
    "region": "us-east-1",
    "accessKeyId": "UW_ACCOUNT_SLEUTEL",
    "secretAccessKey": "UW_ACCOUNT_WACHTWOORD",
    "params": {
        "Bucket": "elasticbeanstalk-us-east-1-DIT_IS_EEN_VOORBEELD"
    },
    "url": "https://s3.amazonaws.com/elasticbeanstalk-us-east-1-DIT_IS_EEN_VOORBEELD"
  },
  "litmus": {
    "username": "YOUR_LITMUS@EMAIL.com",
    "password": "YOUR_ACCOUNT_PASSWORD",
    "url": "https://YOUR_ACCOUNT.litmus.com",
    "applications": ["ol2003","ol2007","ol2010","ol2011","ol2013","chromegmailnew","chromeyahoo","appmail9","iphone5s","ipad","android4","androidgmailapp"]
  }
}
```

## Manuele email tests (config.json)

Ong. Gelijk aan de Litmus test cases, maar je kunt de email laten sturen naar een specifiek email adres. En ook de Litmus tests laten uitvoeren. Het enige wat u hoeft te doen is zijn de AWS S3 account details te plaatsen in de `config.json`. En vergeet ook niet de SMTP gegevens te definieeren van de SMTP server die u wenst te gebruiken. Het email adres waarnaar u de emails wilt verzeten kan ook configureerd worden in het bestand `package.json` of toegevoegd worden met een commando parameten. Bv. `npm run mail -- -to="email@adres.com"`

Similar to the Litmus tests, you can have the emails sent to a specified email address. Just like with the Litmus tests, you will need to provide AWS S3 account details in `config.json`. You will also need to specify to details of an SMTP server. The email address to send to emails to can either by configured in the `package.json` file or added as a parameter like so: `npm run mail -- --to="example.com"`

```json
{
  "aws": {
    "region": "us-east-1",
    "accessKeyId": "YOUR_ACCOUNT_KEY",
    "secretAccessKey": "YOUR_ACCOUNT_SECRET",
    "params": {
        "Bucket": "elasticbeanstalk-us-east-1-DIT_IS_EEN_VOORBEELD"
    },
    "url": "https://s3.amazonaws.com/elasticbeanstalk-us-east-1-THIS_IS_JUST_AN_EXAMPLE"
  },
  "mail": {
    "to": [
      "example@domain.com"
    ],
    "from": "Bedrijf of persoons naam <naam@domain.com",
    "smtp": {
      "auth": {
        "user": "naam@domain.com",
        "pass": "12345678"
      },
      "host": "smtp.domein.com",
      "secureConnection": true,
      "port": 465
    }
  }
}
```

Voor een volledig lijst van clients (applicaties) zie hun [clients lijst](https://litmus.com/emails/clients.xml).

**Waarschuwing:** Het gebruiken van een AWS Service zal leiden tot het betalen van micro bedragen. Maar deze zijn meestal vrij laag. Omdat alleen het minimale aantal data verkeer gebeurd over de verbinding. Gebruik is op eigen risico.

