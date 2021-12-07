# quick-json-server

Node App stub to run the [JSON-Server](https://www.npmjs.com/package/json-server) into a full REST service without 
spending a lot of time to create a service to connect into a database, marshal the result set into a readable json, 
etc ...

## Requirements

* Node 12+

## Installation

```shell
npm install
```

## Resources

Resources are our "_Tables_" into JSON model and we can have a lot of them inside into the same JSON file.

Just add into the root of this project all JSON files named as `db.json` (**_it will be ignored by GIT_**) and the script will publish all them on
the JSON-server resources.

```
Please also rememeber to follow the JSON good practices using the correct format and conventions.
```

**Example:**

* _Array of Media_

```json
{
  "media": [
    {
      "id": "film/2021/dec/06/spider-man-no-way-home-uk-record-advance-ticket-sales",
      "type": "article",
      "sectionId": "film",
      "sectionName": "Film",
      "webPublicationDate": "2021-12-06T15:59:22Z",
      "webTitle": "Spider-Man: No Way Home breaks UK record for advance ticket sales",
      "webUrl": "https://www.theguardian.com/film/2021/dec/06/spider-man-no-way-home-uk-record-advance-ticket-sales",
      "apiUrl": "https://content.guardianapis.com/film/2021/dec/06/spider-man-no-way-home-uk-record-advance-ticket-sales",
      "fields": {
        "body": "<p>The upcoming Hollywood blockbuster Spider-Man: No Way Home is set to be a box office hit after breaking the UK record for advance ticket sales, which are being snapped up at three times the rate of those for the James Bond movie <a href=\"https://www.theguardian.com/film/2021/oct/04/no-time-to-die-james-bond-movie-box-office-daniel-craig-007\">No Time to Die.</a></p> <p>Odeon, the biggest operator in the UK and Ireland with more than 120 cinemas, said it had sold many more than 200,000 tickets for the film in the first seven days since release.</p> <p>The rate of ticket sales to see the film, which stars British actor Tom Holland as Peter Parker, has broken the presale record set by 2019’s Avengers: Endgame. Odeon also said that the Spider-Man presales rate in the first seven days was three times that amassed by Daniel Craig’s <a href=\"https://www.theguardian.com/film/2021/sep/24/bondmania-cinemas-hire-extra-staff-ahead-of-no-time-to-die-release\">eagerly anticipated, much delayed and final outing</a> as James Bond.</p> <p>“As we head into the festive period, we are really pleased with the advance booking numbers for Spider-Man: No Way Home,” said Carol Welch, managing director of Odeon Cinemas UK and Ireland. “It shows guests are loving being back at cinemas and are excited about the magic that our big screen experience brings to movies.”</p> <p>The premiere of the new Bond film, which has made $763m (£576m) in global ticket sales to date, helped to reignite cinemagoing in the UK with the strongest October attendance in a decade.</p> <aside class=\"element element-rich-link element--thumbnail\"> <p> <span>Related: </span><a href=\"https://www.theguardian.com/business/2021/aug/06/uk-cinemas-covid-closures-admissions\">‘We are pretty bruised’: UK cinemas bounce back from Covid closures</a> </p> </aside>  <p>This week the film, which is the third-highest grossing movie of all time in the UK and Ireland behind Skyfall and Star Wars: The Force Awakens, will crack the £100m mark domestically, cementing its position as the biggest hit of the year.</p> <p>As Bond is a particular favourite of audiences in the UK and Ireland, it performs disproportionately well at the box office, making it a tall order for Spider-Man to eclipse its popularity.</p> <p>Nevertheless, on the global stage the superhero movie is on track to become one of the biggest films since the pandemic hit. AMC, the world’s largest cinema operator and owner of Odeon, said that in the US it had generated the second-busiest ticket sales day ever, after Avengers: Endgame.</p> <p>US analysts estimate that its opening weekend is likely to gross at least $150m at the North American box office, which if it does will make it the first film since pre-pandemic 2019 to do so.</p> <p>To date, the top two highest grossing films of the year are both Chinese – The Battle at Lake Changjin ($896m) and Hi, Mom ($822m) – with the third and fourth spots taken by No Time To Die ($763m) and F9: The Fast Saga ($726m).</p>"
      },
      "isHosted": false,
      "pillarId": "pillar/arts",
      "pillarName": "Arts"
    }
  ]
}
```

## Run

### Using the Books example JSON file

Just ask to `npm` start the service for you

```bash
npm run start:books
```

Then you will see on the console

```shell
npm-cli.js run start --scripts-prepend-node-path=auto

> quick-json-server@1.0.0 start
> json-server --watch $(ls db-*.json)


  \{^_^}/ hi!

  Loading books.json
  Done

  Resources
  http://localhost:3000/books

  Home
  http://localhost:3000

  Type s + enter at any time to create a snapshot of the database
  Watching...
```
### Using your JSON file

Just ask to `npm` start the service for you

```bash
npm run start
```

Then you will see on the console

```shell
npm-cli.js run start --scripts-prepend-node-path=auto

> quick-json-server@1.0.0 start
> json-server --watch $(ls db-*.json)


  \{^_^}/ hi!

  Loading db.json
  Done

  Resources
  http://localhost:3000/media

  Home
  http://localhost:3000

  Type s + enter at any time to create a snapshot of the database
  Watching...
```

## Usage

* `GET http://localhost:3000/media`
  List all Media
* `GET http://localhost:3000/media/<ID>`
  Retrieve the Media with `id` equals to `<ID>`. If the `<ID>` is not a **Number** (e.g. 123), **IT MUST BE** 
  URL encoded;  
* `GET http://localhost:3000/media?webTitle=<VALUE>`. If the `<VALUE>` is a complex String (e.g. _C&A_, or 
  _Aviões & Música_), **IT MUST BE** URL encoded;   
  Filter all media by `webTitle` equals to `<VALUE>`.
* `GET http://localhost:3000/media/<ID>/<PROPERTY>`
  Retrieve just the Media's `<PROPERTY>` field for the matching `<ID>`
* `POST http://localhost:3000/media`
  Create an entry at the related resource JSON file

## Examples

```shell
curl -X GET "http://localhost:3000/media/film%2F2021%2Fdec%2F06%2Fspider-man-no-way-home-uk-record-advance-ticket-sales"                     ✔  10139  15:11:14
{
  "id": "film/2021/dec/06/spider-man-no-way-home-uk-record-advance-ticket-sales",
  "type": "article",
  "sectionId": "film",
  "sectionName": "Film",
  "webPublicationDate": "2021-12-06T15:59:22Z",
  "webTitle": "Spider-Man: No Way Home breaks UK record for advance ticket sales",
  "webUrl": "https://www.theguardian.com/film/2021/dec/06/spider-man-no-way-home-uk-record-advance-ticket-sales",
  "apiUrl": "https://content.guardianapis.com/film/2021/dec/06/spider-man-no-way-home-uk-record-advance-ticket-sales",
  "fields": {
    "body": "<p>The upcoming Hollywood blockbuster Spider-Man: No Way Home is set to be a box office hit after breaking the UK record for advance ticket sales, which are being snapped up at three times the rate of those for the James Bond movie <a href=\"https://www.theguardian.com/film/2021/oct/04/no-time-to-die-james-bond-movie-box-office-daniel-craig-007\">No Time to Die.</a></p> <p>Odeon, the biggest operator in the UK and Ireland with more than 120 cinemas, said it had sold many more than 200,000 tickets for the film in the first seven days since release.</p> <p>The rate of ticket sales to see the film, which stars British actor Tom Holland as Peter Parker, has broken the presale record set by 2019’s Avengers: Endgame. Odeon also said that the Spider-Man presales rate in the first seven days was three times that amassed by Daniel Craig’s <a href=\"https://www.theguardian.com/film/2021/sep/24/bondmania-cinemas-hire-extra-staff-ahead-of-no-time-to-die-release\">eagerly anticipated, much delayed and final outing</a> as James Bond.</p> <p>“As we head into the festive period, we are really pleased with the advance booking numbers for Spider-Man: No Way Home,” said Carol Welch, managing director of Odeon Cinemas UK and Ireland. “It shows guests are loving being back at cinemas and are excited about the magic that our big screen experience brings to movies.”</p> <p>The premiere of the new Bond film, which has made $763m (£576m) in global ticket sales to date, helped to reignite cinemagoing in the UK with the strongest October attendance in a decade.</p> <aside class=\"element element-rich-link element--thumbnail\"> <p> <span>Related: </span><a href=\"https://www.theguardian.com/business/2021/aug/06/uk-cinemas-covid-closures-admissions\">‘We are pretty bruised’: UK cinemas bounce back from Covid closures</a> </p> </aside>  <p>This week the film, which is the third-highest grossing movie of all time in the UK and Ireland behind Skyfall and Star Wars: The Force Awakens, will crack the £100m mark domestically, cementing its position as the biggest hit of the year.</p> <p>As Bond is a particular favourite of audiences in the UK and Ireland, it performs disproportionately well at the box office, making it a tall order for Spider-Man to eclipse its popularity.</p> <p>Nevertheless, on the global stage the superhero movie is on track to become one of the biggest films since the pandemic hit. AMC, the world’s largest cinema operator and owner of Odeon, said that in the US it had generated the second-busiest ticket sales day ever, after Avengers: Endgame.</p> <p>US analysts estimate that its opening weekend is likely to gross at least $150m at the North American box office, which if it does will make it the first film since pre-pandemic 2019 to do so.</p> <p>To date, the top two highest grossing films of the year are both Chinese – The Battle at Lake Changjin ($896m) and Hi, Mom ($822m) – with the third and fourth spots taken by No Time To Die ($763m) and F9: The Fast Saga ($726m).</p>"
  },
  "isHosted": false,
  "pillarId": "pillar/arts",
  "pillarName": "Arts"
}%
```
