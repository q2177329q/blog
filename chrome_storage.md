# Chrome 插件中的持久化存储

在 Chrome 插件开发中，我们通常需要使用持久化存储来保存插件的状态和数据。Chrome 提供了三种不同的存储方式：`chrome.storage.local`、`chrome.storage.session` 和 `chrome.storage.sync`。

## chrome.storage.local

`chrome.storage.local` 可以用来存储插件的数据，并且数据的生命周期是永久的，除非手动删除或卸载插件。以下是一些常见的 API 使用示例：

- `chrome.storage.local.set()`：设置一个或多个键值对。

  ```javascript
  chrome.storage.local.set({ key1: 'value1', key2: 'value2' }, function() {
    console.log('Data saved to local storage');
  });
  ```

- `chrome.storage.local.get()`：获取一个或多个键对应的值。

  ```javascript
  chrome.storage.local.get(['key1', 'key2'], function(result) {
    console.log('Value of key1:', result.key1);
    console.log('Value of key2:', result.key2);
  });
  ```

- `chrome.storage.local.remove()`：删除一个或多个键值对。

  ```javascript
  chrome.storage.local.remove(['key1', 'key2'], function() {
    console.log('Data removed from local storage');
  });
  ```

## chrome.storage.session

`chrome.storage.session` 可以用来存储插件的数据，并且数据的生命周期是在浏览器会话期间，当浏览器关闭时，数据会被清除。以下是一些常见的 API 使用示例：

- `chrome.storage.session.set()`：设置一个或多个键值对。

  ```javascript
  chrome.storage.session.set({ key1: 'value1', key2: 'value2' }, function() {
    console.log('Data saved to session storage');
  });
  ```

- `chrome.storage.session.get()`：获取一个或多个键对应的值。

  ```javascript
  chrome.storage.session.get(['key1', 'key2'], function(result) {
    console.log('Value of key1:', result.key1);
    console.log('Value of key2:', result.key2);
  });
  ```

- `chrome.storage.session.remove()`：删除一个或多个键值对。

  ```javascript
  chrome.storage.session.remove(['key1', 'key2'], function() {
    console.log('Data removed from session storage');
  });
  ```

## chrome.storage.sync

`chrome.storage.sync` 可以用来实现跨设备同步插件的数据。以下是一些常见的 API 使用示例：

- `chrome.storage.sync.set()`：设置一个或多个键值对。

  ```javascript
  chrome.storage.sync.set({ key1: 'value1', key2: 'value2' }, function() {
    console.log('Data saved to sync storage');
  });
  ```

- `chrome.storage.sync.get()`：获取一个或多个键对应的值。

  ```javascript
  chrome.storage.sync.get(['key1', 'key2'], function(result) {
    console.log('Value of key1:', result.key1);
    console.log('Value of key2:', result.key2);
  });
  ```

- `chrome.storage.sync.remove()`：删除一个或多个键值对。

  ```javascript
  chrome.storage.sync.remove(['key1', 'key2'], function() {
    console.log('Data removed from sync storage');
  });
  ```
