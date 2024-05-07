# Imports&Exports (Modules)

### default export v. named export

person.js

```jsx
const person = {
	name:'Max'
}

export default person
```

utility.js

```jsx
export const clean = () => {...}
export const baseData = 10;
```

app.js

```jsx
import person from './person.js' //these two lines import the same.
import prs from './person.js'

import { baseData } from './utility.js'
import { clean } from './utility.js'
```

**default export**

Module defined as default can export only one class, variable, etc. from a file. When importing the default module, you can use any name. 

**named export**

Inside one file, it is possible to export a variety of variables/classes. When importing, however, you have to import the objects as it was named inside the curly brackets({}). You could use other names, but you have to set the new name using ‘as’ keyword.

```jsx
import {smth} from './utility.js'
import {smth as Smth} from './utility.js'
import * as bundled from './utility.js'
```