# AsyncArray
==========

Yet another control flow library after getting fustrated with previous ones.

## Usage

The `next` callback takes the arguments (error, data)

    var AsyncArray = require('async-array')

    var array = new AsyncArray([1, 2, 3, 4])

    array
      .map(function (item, i, next) {
        db.query('SELECT * FROM x WHERE id = ?', [item], next)
      })
      .done(function (error, results) {
        console.log("Got me database listings partner!")
      })
      .forEach(function (db_result, i, next) {
        doSomethingAsync(db_result, next)
      })
      .exec()

As you can see, you can chain stuff and the result is passed along from the previous operation. If you don't call `exec` immediately you can store the operation to be executed at some later time.

## Features

`AsyncArray` inherits from `Array` with the following methods added:

- map
- mapSerial
- filter
- filterSerial
- forEach
- forEachSerial

Serial methods do things one after another instead of in parallel.
