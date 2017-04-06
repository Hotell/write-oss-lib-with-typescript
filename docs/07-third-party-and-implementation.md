## Writing our library III

### Adding 3rd party dependencies

- we will use `lodash` for instance

`yarn add lodash`

- now hop back to your editor and import lodash with some method.

Whoops TS errors

- we need to install typings from `npm/@types`

`yarn add -D @types/lodash`


### Implemetation

- create our database of names

> src/sw-names.ts

```ts
export const SW_NAMES = [
  '4-LOM',
  'Aayla Secura',
  'Admiral Ackbar',
  'Admiral Thrawn',
  'Ahsoka Tano',
  'Anakin Solo',
  'Asajj Ventress',
  'Aurra Sing',
  'Senator Bail Organa',
  'Barriss Offee',
  'Bastila Shan',
  'Ben Skywalker',
  'Bib Fortuna',
  'Biggs Darklighter',
  'Boba Fett',
  'Bossk',
  'Brakiss',
  'C-3PO',
  'Cad Bane',
  'Cade Skywalker',
  'Callista Ming',
  'Captain Rex',
  'Carnor Jax',
  'Chewbacca',
  'Clone Commander Cody',
  'Count Dooku',
  'Darth Bane',
  'Darth Krayt',
  'Darth Maul',
  'Darth Nihilus',
  'Darth Vader',
  'Dash Rendar',
  'Dengar',
  'Durge',
  'Emperor Palpatine',
  'Exar Kun',
  'Galen Marek',
  'General Crix Madine',
  'General Dodonna',
  'General Grievous',
  'General Veers',
  'Gilad Pellaeon',
  'Grand Moff Tarkin',
  'Greedo',
  'Han Solo',
  'IG 88',
  'Jabba The Hutt',
  'Jacen Solo',
  'Jaina Solo',
  'Jango Fett',
  'Jarael',
  'Jerec',
  "Joruus C'Baoth",
  'Ki-Adi-Mundi',
  'Kir Kanos',
  'Kit Fisto',
  'Kyle Katarn',
  'Kyp Durron',
  'Lando Calrissian',
  'Luke Skywalker',
  'Luminara Unduli',
  'Lumiya',
  'Mace Windu',
  'Mara Jade',
  'Mission Vao',
  'Natasi Daala',
  'Nom Anor',
  'Obi-Wan Kenobi',
  'Padmé Amidala',
  'Plo Koon',
  'Pre Vizsla',
  'Prince Xizor',
  'Princess Leia',
  'PROXY',
  'Qui-Gon Jinn',
  'Quinlan Vos',
  'R2-D2',
  'Rahm Kota',
  'Revan',
  'Satele Shan',
  'Savage Opress',
  'Sebulba',
  'Shaak Ti',
  'Shmi Skywalker',
  'Talon Karrde',
  'Ulic Qel-Droma',
  'Visas Marr',
  'Watto',
  'Wedge Antilles',
  'Yoda',
  'Zam Wesell',
  'Zayne Carrick',
  'Zuckuss'
]
```

Our lib will have just 2 API functions:
- all -> will return all names
- random -> will return one or N random names from DB


**all()**

> src/all.ts

```ts
import { SW_NAMES } from './sw-names'

export const all = () => { return SW_NAMES.slice() }
```

**random(count?)**

> src/random.ts

```ts
import { sampleSize } from 'lodash'
import { SW_NAMES } from './sw-names'

const getRandomItem = () => {
  return sampleSize(SW_NAMES, 1)[0]
}

export function random(howMany?: number) {
  if (howMany === undefined) {
    return getRandomItem()
  } else {
    const randomItems = []
    for (let i = 0; i < howMany; i++) {
      randomItems.push(getRandomItem())
    }
    return randomItems
  }
}
```


Perfect we have the functionality! Now we need to expose it as our public API via a **barrel** file ( main entry point ).

Hop to `index.ts` and make our API's public

```ts
export * from './random';
export * from './all';
```


GOOD JOB! NOW WHAT?

**Try it out !**


- Compile it `yarn tsc`
- Go to Node REPL
  - `node`
  - `const ourLib = require('./lib')`
  - `ourLib.random()`
  - `ourLib.random(2)`
  - `ourLib.all()`


  WORKS!
