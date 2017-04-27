# egg-mongo

Database ` mongo ` plug-in for ` egg ` provide ` mongo ` database access functions

#  Install

```
$ npm i egg-mongo --save
```

# Configuration

Change `${app_root}/config/plugin.js` to enable MongoDB plugin:


```
exports.mongo = {
  enable: true,
  package: 'egg-mongo',
};
```

Configure database information in `${app_root}/config/config.default.js`:


Simple database instance

```
mongo: {
  urlConfig: {
    host: '127.0.0.1',
    port: '27017'
  },
  dbname: 'dbName',
  username: '',
  password: ''
}
```

#  Multiple database instance
```
mongo: {
  urlConfig: [{
    host: '127.0.0.1',
    port: '27017'
  }, {
    host: '127.0.0.1',
    port: '27018'
  }],
  dbname: 'dbName',
  username: '',
  password: ''
}
```


[More database connection parameter details......](http://mongodb.github.io/node-mongodb-native/2.2/tutorials/connect/)

#  CRUD user guide

`app/controller/home.js`
```
'use strict';
module.exports = app => {
  return class HomeController extends app.Controller {
    get collectionName() {
      return 'qrcode';
    }
    getCollectionDB() {
      return app.mongo.getQuery('qrcode');
    }
    * page() {
      const qrcode = this.getCollectionDB();
      this.ctx.body = yield qrcode.find();
    }
  };
};
```

[More......](https://github.com/mzTeamMeatMan/mongo-co)