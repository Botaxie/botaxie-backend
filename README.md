<h1 align="center">
  <br>
  <a href="https://botaxie.org"><img src="https://botaxie.org/static/media/logo.a54f985f.png" alt="Botaxie" width="200"></a>
  <br>
  <strong>Axie infinity marketplace bot as a service</strong>
  <br>
</h1>

<h4 align="center">NFT (Axie Infinity) Sniper bot as-a-service in <a href="https://nestjs.com/" target="_blank">Nest.js</a>.</h4>



<p align="center">
  <a href="#key-features">Key Features</a> •
  <a href="#how-to-use">How To Use</a> •
  <a href="#technologies">Technologies</a> •
  <a href="#contact-and-support">Contact and Support</a> •
  <a href="#license">License</a>
</p>

![screenshot](https://raw.githubusercontent.com/Botaxie/botaxie/main/screenshots/screenshot-rocks(2).png)


## Key Features

* Authetication:
    - Json Web Token (JWT)
* Fetches and filters recently listed axies
* Replicates Ronin Wallet's purchase transaction
* Buys the axie instantly if it matches the user's configuration (See <a href="#configurations">Configurations</a>)
* Retries to buy a good axie while user wallet has funds available
* Stops filtering for a user if reached target number of axies or funds were withdrawn
* Logs all activity and purchase attempts
* Protected HTTP endpoints for all user activity

## How To Use

To clone and run this application, you'll need [Git](https://git-scm.com) and [Node.js](https://nodejs.org/en/download/) (which comes with [npm](http://npmjs.com)) installed on your computer.


> **Note** :
> Before running the app, make you sure you made a `.env` file with valid parameters, see `.env.sample`

```bash
# .env
JWT_SECRET=secret
JWT_EXP=1d
ENCRYPTION_KEY=d85117047fd06d3afa79b6e44ee3a52eb426f
MIN_RON_BALANCE=0.001
```

From your command line:
```bash
# Clone this repository
$ git clone https://github.com/yahyaoukharta/botaxie-backend.git
# Go into the repository
$ cd botaxie-backend
# Install dependencies
$ npm install
# Run the app
$ npm run start:dev
```

## Configurations

Users can specify to the bot which axies they are interested in by creating Configurations, the data type used resembles this :

```typescript
// /src/types/AxieConfig
interface AxieConfig {
  maxPrice: number;

  minId?: number;
  maxId?: number;

  //Class
  _class?: AxieClass;

  //Min Stats
  minStats?: AxieStats;

  //Breed Count 0-7
  minBreedCount?: number;
  maxBreedCount?: number;

  // Purity 1-6
  minPurity?: number;
  maxPurity?: number;

  //Pureness 0-100 %
  minPureness?: number;
  maxPureness?: number;

  //Potential points
  minPotentialPoints?: PotentialPoints;

  //genes
  eyesD?: BodyPart;
  earsD?: BodyPart;
  backD?: BodyPart;
  mouthD?: BodyPart;
  hornD?: BodyPart;
  tailD?: BodyPart;
  eyesR1?: BodyPart;
  earsR1?: BodyPart;
  backR1?: BodyPart;
  mouthR1?: BodyPart;
  hornR1?: BodyPart;
  tailR1?: BodyPart;
  eyesR2?: BodyPart;
  earsR2?: BodyPart;
  backR2?: BodyPart;
  mouthR2?: BodyPart;
  hornR2?: BodyPart;
  tailR2?: BodyPart;
}
```

> **Note** :
> You can notice that only `maxPrice` is mandatory, but users can use any other filters or leave empty

## Instances

After creating a configuration, and having a wallet with enough funds, users can launch instances.
When you have an instance running, it means the following :

* The main bot's cron job will consider the user configuration when filtering the recently listed axies
* Axies are matched with the oldest instances first 
    - If an axie recently listed, and matches with two configurations, Botaxie will give priority to the owner of the oldest instance created: `first come, first served`.
* When a config matches with an axie, a purchase attempt is done, the result is logged, and emitted in real time to the user.
* Instance stop conditions :
    - Not enough funds in the user's wallet.
    - Reached the target amount of axie to buy using that instance.
    - Instance with no purchase for more than 24 hours.

## Testing

Test the app's endpoint, by importing the collection `/test/backend.postman_collection.json` to [Postman](https://postman.com/) and running the requests.

## Technologies

This app uses the following frameworks and libraries :

- [Node.js](https://nodejs.org/)
- [Nest.js](http://nestjs.com/)
- [SQLite](https://sqlite.org/)
- [Web3.js](https://web3js.readthedocs.io/)
- [agp-npm - Gene parsing package for Axie Infinity](https://github.com/ShaneMaglangit/agp-npm)
- [TypeORM](https://typeorm.io/)

## Contact and Support

You can always contact me for support via the following channels

> LinkedIn [Yahya Oukharta](https://linkedin.com/in/yahyaoukharta)

> GitHub [@yahyaoukharta](https://github.com/yahyaoukharta)

> Discord [@Yhyo#9751](https://discordapp.com/users/Yhyo#9751)

> Email [youkharta@gmail.com](#contact-and-support)

## License

[MIT](./LICENSE)
