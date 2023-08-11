# vite-plugin-mock-server-plus

Based on the `vite-plugin-mock-server` plugin modification.

## New Features

Support direct use mock schema.

You can control whether the current mock file is enabled through the disable field.

```ts
export default <MockHandler>{
  pattern: "/app/car/driver",
  disable: true,
  method: "POST",
  schema: {
    requestId: "@string",
    code: 0,
    msg: "@string",
    data: {
      carNo: /[\d\w]{8,8}/,
      "carColor|1": ["black", "white", "red"],
      carBrand: "@string",
      "carType|1": [1, 2, 3, 4],
      driverName: "@string",
      driverPhone: /\d{11,11}/,
      "driverScore|1-5.1": 1,
    },
  },
};
```

You can modify the mock schema to generate data in the handle.

```ts
export default <MockHandler>{
  pattern: "/app/car/driver",
  method: "POST",
  schema: {
    requestId: "@string",
    code: 0,
    msg: "@string",
    data: {
      carNo: /[\d\w]{8,8}/,
      "carColor|1": ["black", "white", "red"],
      carBrand: "@string",
      "carType|1": [1, 2, 3, 4],
      driverName: "@string",
      driverPhone: /\d{11,11}/,
      "driverScore|1-5.1": 1,
    },
  },
  handle(req, res) {
    req.mock.data.carNo = "66666666";
    res.end(JSON.stringify(req.mock));
  },
};
```
