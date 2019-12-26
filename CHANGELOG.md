# Change Log

## [1.1.1] - 2019-12-26 by freemember007

- undo modify by version 1.1.0, don't use require('lodash-bound/map')` or `require('lodash-bound/lib/map')`, use:
```javascript
const { map, filter } = require('lodash-bind')
// or
import { map, filter } from 'lodash-bind'
```

## [1.1.0] - 2016-06-07

- Place generated files in root in the `npm` pacakge, so `require` looks like `require('lodash-bound/map')` instead of `require('lodash-bound/lib/map')`

## [1.0.2] - 2016-06-07

- Added basic POC test

## [1.0.0] - 2016-05-26

- Initial release
