# QuickMongo

Quick Mongodb wrapper for beginners that provides key-value based interface.

![](https://camo.githubusercontent.com/ee0b303561b8c04223d4f469633e2088968cf514f0f6901c729331c462a32f10/68747470733a2f2f63646e2e646973636f72646170702e636f6d2f6174746163686d656e74732f3739333638393539323431343939343436362f3833323039343438363834353834393631302f6c6f676f2e37393539646231325f35302e706e67)

# Installing

```bash
$ npm install --save mongodb # required
$ npm install --save quickmongo
```

# Documentation
**[https://quickmongo.js.org](https://quickmongo.js.org)**

# Features
- Beginner friendly
- Strongly typed
- Asynchronous
- Dot notation support
- Key-Value like interface
- Easy to use

# Example

```js
const { Collection: MongoCollection, MongoClient } = require("mongodb");
const { Collection } = require("quickmongo");

const mongo = new MongoClient("mongodb://localhost/quickmongo");

mongo.connect()
    .then(() => {
        console.log("Connected to the database!");
        doStuff();
    });

function doStuff() {
    const mongoCollection = mongo.db().collection("JSON");

    const db = new Collection(mongoCollection, {
        difficulty: String,
        items: [String],
        balance: Number
    });
    
    db.set("userInfo", { difficulty: "Easy", items: [], balance: 0 }).then(console.log);
    // -> { difficulty: 'Easy', items: [], balance: 0 }

    db.push("userInfo", "Sword", "items").then(console.log);
    // -> { difficulty: 'Easy', items: ['Sword'], balance: 0 }

    db.set("userInfo", 500, "balance").then(console.log);
    // -> { difficulty: 'Easy', items: ['Sword'], balance: 500 }

    // Repeating previous examples:
    db.push("userInfo", "Watch", "items").then(console.log);
    // -> { difficulty: 'Easy', items: ['Sword', 'Watch'], balance: 500 }

    const previousBalance = await db.get("userInfo", "balance");
    db.set("userInfo", previousBalance + 500, "balance").then(console.log);
    // -> { difficulty: 'Easy', items: ['Sword', 'Watch'], balance: 1000 }

    // Fetching individual properties
    db.get("userInfo", "balance").then(console.log);
    // -> 1000
    db.get("userInfo", "items").then(console.log);
    // -> ['Sword', 'Watch']

    // remove item
    db.pull("userInfo", "Sword", "items").then(console.log);
    // -> { difficulty: 'Easy', items: ['Watch'], balance: 1000 }
}
```

# Discord Support
**[SnowflakeDev Community ❄️](https://snowflakedev.org/discord)**
