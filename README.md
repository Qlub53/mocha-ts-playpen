# mocha-ts-playpen

[Mocha Test Explorer](https://marketplace.visualstudio.com/items?itemName=hbenl.vscode-mocha-test-adapter) **only** seems to work with `commonjs`.

Attempts to make ES Module works always ended up with
> TypeError [ERR_UNKNOWN_FILE_EXTENSION]: Unknown file extension “.ts”

-------------------------

Below seems to be the **only** way in which Mocha Test Explore works

**package.json**
```json
{
	"type": "commonjs"
}
```

**tsconfig.json**
```json
{
    "compilerOptions": {
        "module": "commonjs",
        "target": "esnext",
        "esModuleInterop": true,
    },
    "include": [
        "app/test",
    ]
}
```
`esModuleInterop` is required to default-import Module ‘chai’

**settings.json** of VSCode
```json
{
    "mochaExplorer.files": "app/test/**/*.test.{j,t}s",
    "mochaExplorer.require": [
        "ts-node/register", // doesn't seem necessary, everything works even without this
        "esm" // always necessary, the Explore fails without this
    ]
}
```
