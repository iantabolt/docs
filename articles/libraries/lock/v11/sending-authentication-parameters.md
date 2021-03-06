---
section: libraries
description: Lock v11 documentation on setting authentication parameters.
---
# Lock Authentication Parameters

You can send parameters when starting a login by adding them to the options object. The example below adds a `state` parameter with a value equal to `'foo'`.

```js
var options = {
  auth: {
    params: {state: 'foo'},
  }
};
```

The following parameters are supported: `access_token`, `scope`, `protocol`, `device`, `request_id`, `nonce` and `state`.

::: note
This would be analogous to triggering the login with `https://${account.namespace}/authorize?state=foo&...`.
:::

## Supported parameters

### scope {string}

```js
var options = {
  auth: {
    params: {scope: 'openid email user_metadata app_metadata picture'},
  }
};
```

There are different values supported for scope. Keep in mind that JWTs are sent on every API request, so it is desirable to keep them as small as possible.

The default `scope` value in Lock 11 is `openid profile email`.

For more information about scopes, see the [scopes documentation page](/scopes).

#### Example: retrieve a token

In Lock 11, if you wish to receive a token with the ability to fetch the user's profile data, you should add the `scope` parameter.

```js
var options = {
  auth: {
    params: {
        scope: 'openid profile'
    }
  }
};
```

::: note
There is also a `connectionScopes` configuration option for Lock 11, which allows you to specify scopes on any specific connection. This will be useful if you want to initially start with a set of scopes (defined on the dashboard), but later on request additional permissions or attributes from a specific connection. Read more about it on the [Lock Configuration Options](/libraries/lock/v11/configuration#connectionscopes-object-) page.
:::

### state {string}

The `state` parameter is an arbitrary state value that will be mantained across redirects. It is useful to mitigate [XSRF attacks](http://en.wikipedia.org/wiki/Cross-site_request_forgery) and for any contextual information, [such as a return url](/tutorials/redirecting-users), that you might need after the authentication process is finished. If a custom state parameter is not provided, Lock will automatically generate one.

[Click here to learn more about how to send/receive the state parameter.](/protocols/oauth-state)

### nonce {string}

The `nonce` parameter is used to help prevent replay attacks, and will be automatically generated by Lock if a custom value is not provided.
