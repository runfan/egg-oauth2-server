# egg-oauth2-server

[![NPM version][npm-image]][npm-url]
[![build status][travis-image]][travis-url]
[![Test coverage][codecov-image]][codecov-url]
[![David deps][david-image]][david-url]
[![Known Vulnerabilities][snyk-image]][snyk-url]
[![npm download][download-image]][download-url]

[npm-image]: https://img.shields.io/npm/v/egg-oauth2-server.svg?style=flat-square
[npm-url]: https://npmjs.org/package/egg-oauth2-server
[travis-image]: https://img.shields.io/travis/Azard/egg-oauth2-server.svg?style=flat-square
[travis-url]: https://travis-ci.org/Azard/egg-oauth2-server
[codecov-image]: https://img.shields.io/codecov/c/github/Azard/egg-oauth2-server.svg?style=flat-square
[codecov-url]: https://codecov.io/github/Azard/egg-oauth2-server?branch=master
[david-image]: https://img.shields.io/david/Azard/egg-oauth2-server.svg?style=flat-square
[david-url]: https://david-dm.org/Azard/egg-oauth2-server
[snyk-image]: https://snyk.io/test/npm/egg-oauth2-server/badge.svg?style=flat-square
[snyk-url]: https://snyk.io/test/npm/egg-oauth2-server
[download-image]: https://img.shields.io/npm/dm/egg-oauth2-server.svg?style=flat-square
[download-url]: https://npmjs.org/package/egg-oauth2-server

<!--
Description here.
-->
[Chinese Example | 中文样例教程](https://cnodejs.org/topic/592b2aedba8670562a40f60b)

## Install

```bash
$ npm i egg-oauth2-server --save
```

## Usage

```js
// {app_root}/config/plugin.js
exports.oauth2Server = {
  enable: true,
  package: 'egg-oauth2-server',
};

// {app_root}/app/router.js
app.all('/user/grant', app.oauth.grant());
app.get('/user/check', app.oauth.authorise(), 'user.check');
```

## Configuration

```js
// {app_root}/config/config.default.js
module.exports = config => {
  const exports = {};
  exports.oauth2Server = {
    debug: config.env === 'local',
    grants: [ 'password' ],
  };
  return exports;
};
```

See [test/fixtures/apps/oauth2-server-test/config/config.unittest.js](test/fixtures/apps/oauth2-server-test/config/config.unittest.js) for reference.

Full description see [https://www.npmjs.com/package/oauth2-server](https://www.npmjs.com/package/oauth2-server).

## Implementation Example

A simple implementation of password mode OAuth 2.0 server, see [test/fixtures/apps/oauth2-server-test/app/extend/oauth.js](test/fixtures/apps/oauth2-server-test/app/extend/oauth.js)

```js
// {app_root}/app/extend/oauth.js
'use strict';

module.exports = app => {
  const model = {};
  model.getClient = (clientId, clientSecret, callback) => {};
  model.grantTypeAllowed = (clientId, grantType, callback) => {};
  model.getUser = (username, password, callback) => {}; // only for password mode
  model.saveAccessToken = (accessToken, clientId, expires, user, callback) => {};
  model.getAccessToken = (bearerToken, callback) => {};
  return model;
};
```

Full description see [https://www.npmjs.com/package/oauth2-server](https://www.npmjs.com/package/oauth2-server).

### password mode `app.oauth.grant()` lifecycle

`getClient` --> `grantTypeAllowed` --> `getUser` --> `saveAccessToken`

### password mode `app.oauth.authorise()` lifecycle

Only `getAccessToken`

## Questions & Suggestions

Please open an issue [here](https://github.com/Azard/egg-oauth2-server/issues).

## License

[MIT](LICENSE)
