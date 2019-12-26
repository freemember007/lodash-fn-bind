# lodash-fn-bind

transform all lodash function to bindable function, with ec39 proposal new function bind syntax (::), you can do code fly.

npm:

https://www.npmjs.com/package/lodash-fn-bind

install:

```bash
yarn add lodash-fn-bind
```

just a look:

```javascript

import { cat } from 'shelljs'
import date from 'date.js'
import { format } from 'date-fns/fp'
import logger from '../util/logger'
import { IS_PROD } from '../constant'
import { renameKeys } from 'ramda-adjunct'
import { _map, _filter, _uniqBy, _tap, } from 'lodash-bound'
import { take, tryCatch, pluck, always, has,  omit, allPass } from 'ramda'

const YESTERDAY = format('yMMdd', date('yesterday'))
const requestLogs = (IS_PROD ? '/usr/local/nginx/logs' : __dirname)
  |> cat(`${#}/access.log-${YESTERDAY}`).split('\n')
  ::_map(tryCatch(JSON.parse, always({})))
  ::_filter({ status: '200' }) // = R.filter(R.propEq('status', '200'))
  ::_map('body') // = R.pluck('body')
  ::_map(tryCatch(JSON.parse, always({})))
  ::_filter(allPass([has('service'), has('__openid')]))
  ::_map(omit(['channel', 'format', 'oper', 'random', 'spid', 'sign', 'userId', '__patientId']))
  ::_map(renameKeys({ service: 'apiname' }))
  ::__uniqBy('__openid')  // = R.uniqBy(R.prop('apiname'))
  ::_tap(xn => logger.log('get log count %d，the first is %j:', xn.length, take(1, xn)))
```
