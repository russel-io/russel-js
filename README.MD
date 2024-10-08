# 🚀 Russel Client in JavaScript

Welcome to the **Russel Client** package! This library, crafted in JavaScript, enables seamless integration with the Russel service.

## ⚙️ Setup

Get started by installing the package:

```bash
# npm
npm install Russel-js
```
Russel uses Authorization in order to set clusters. so you need to authorize yourself first.

## 🔒 Authorization

After installing the russel application. russel by default creates a user with this credentials

```bash
 admin // username
 123456 // password
```
This is the default user with the highest priority that can add and remove profiles.

Now, before using the `russel-js` API you need to call `authorize` function when a new client is created.

```typescript

// Example usage:
const russelClient = new RusselClient();
russelClient.authorize();
```

If you need to authorize as another user, there are two different ways to do so.

## 1. Set user in constructor

```typescript

// Example usage:
const russelClient = new RusselClient('admin','123456'); // first arg is username and second is password
russelClient.authorize();
```

## 2. Set user in russelConfig

```typescript

// Example usage:
const russelClient = new RusselClient(); // first arg is username and second is password
russelClient.setRusselConfig({
    username:'admin',
    password:123456
})
russelClient.authorize();
```


# 📬 Handling Responses
Russel-js offers two ways to handle responses from your client operations:

1. Raw value

Retrieve the raw value directly:

```JavaScript
const res = await russelClient.get({
    cluster: 'foo',
    key: 'bar',
});
console.log(res); // raw value

```

2. Decoded Value



Alternatively, decode the value using the built-in function:

```JavaScript
const res = await russelClient.get({
    cluster: 'foo',
    key: 'bar',
});
console.log(res.decodeData()); // decoded value


```


# 🔄 Internal Functions
`Russel-js` provides a straightforward API for CRUD operations. Here's a step-by-step guide on using its functionalities:


## Set a Value in a Cluster

```JavaScript
try {
    const res = await russelClient.set({
        cluster: 'foo',
        key: 'bar',
        value: 'fooBar',
    });
    console.log('Value set successfully');
} catch (error) {
    console.error(error);
}
```
## Get a Value from a Cluster

```JavaScript
try {
    const res = await russelClient.getCluster({
        cluster: 'foo',
        key: 'bar',
    });
    console.log(res.decodeData()); // 'fooBar'
} catch (error) {
    console.error(error);
}

```
## Delete a Value from a Cluster


```JavaScript
try {
    const res = await russelClient.deleteCluster({
        cluster: 'foo',
        key: 'bar',
    });
    console.log('Value deleted');
} catch (error) {
    console.error(error);
}


```
## Clear a Cluster

```JavaScript
try {
    const res = await russelClient.clearCluster('foo'); // cluster name
    console.log('Cluster cleared');
} catch (error) {
    console.error(error);
}


```
## List All Keys in a Cluster


```JavaScript
try {
    const res = await russelClient.getKeysOfCluster('foo'); // cluster name
    console.log(res); // ['bar']
} catch (error) {
    console.error(error);
}

```

## Create a New Cluster



```JavaScript
try {
    const res = await russelClient.setCluster('foo'); // cluster name
    console.log('Cluster created');
} catch (error) {
    console.error(error);
}


```

## Check Russel-js Connection

```JavaScript
try {
    const res = await russelClient.checkConnection();
    console.log('Connection successful');
} catch (error) {
    console.error(error);
}


```

# 🔑 Key Points

All responses are returned in the following format:

```JavaScript
{
    is_success: boolean, // operation status
    data: this.data, // data itself
    message: this.message // message
}

```
In case of errors, the response will include is_success set to false:

```JavaScript
{
    is_success: false, // operation status
    message: this.message // error message
}

```

For more details, visit our [GitHub organization](https://github.com/russel-io/). Happy coding! 🎉



