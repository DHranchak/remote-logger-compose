# Remote Logger Service

A lightweight client-side logging service that collects logs from React Native apps and sends them to a remote backend for debugging, monitoring, and analytics.

## Features

- Logs with various severity levels (`TRACE`, `DEBUG`, `INFO`, etc.)
- Automatically includes device info and OS version
- Batches and sends logs to a remote server
- Uses `react-native-device-info` for device metadata


---

## 🔧 Usage

### Initialize the Logger

Call `RemoteLogger.init()` before logging anything. You can do this in your app's entry point:

```ts
RemoteLogger.init();
```

### Log Examples

```ts
RemoteLogger.trace('App start trace');
RemoteLogger.debug('Debugging API response', { data: 'example' });
RemoteLogger.error('Unexpected exception', errorObject);
RemoteLogger.ok('Heartbeat - App is healthy');
```

---

## 🛰️ API Endpoint

All logs are sent to the following endpoint:

```
POST https://<REMOTE_LOGGER_BACKEND_ADDRESS>/api/log
```

### Payload Format

```json
[
  {
    "level": "INFO",
    "title": "User logged in",
    "data": "{\"userId\":1234}",
    "timestamp": "2025-04-07T10:30:00.000Z",
    "device": "Samsung SM-G991B",
    "os": "android 33",
    "uuid": "device-unique-id-123"
  }
]
```

### Field Description

| Field           | Type   | Description                          |
| --------------- | ------ | ------------------------------------ |
| level           | string | Log level (`TRACE`, `DEBUG`, etc.)   |
| title           | string | Short description of the log         |
| data (optional) | string | JSON-encoded metadata or message     |
| timestamp       | string | ISO timestamp of the log             |
| device          | string | Manufacturer and model of the device |
| os              | string | OS name and version                  |
| uuid            | string | Unique device identifier             |

---

## 🧾 Available Log Levels

The following log levels are supported by the logger. Use these values for the `level` field in your logs:

```ts
enum LogLevel {
  TRACE = 'TRACE',
  DEBUG = 'DEBUG',
  INFO = 'INFO',
  LOG = 'LOG',
  WARN = 'WARN',
  ERROR = 'ERROR',
  CRITICAL = 'CRITICAL',
  OK = 'OK'
}
```