## PATCHES: 

### Publishing:

- `app/package.json -> scripts: dist -> changed ... -publish=never to -publish=always`

### Subscription Crack:

- `kernel/model/conf.go` :

(1)
```go
func IsSubscriber() bool {
	//u := Conf.GetUser()
	//return nil != u && (-1 == u.UserSiYuanProExpireTime || 0 < u.UserSiYuanProExpireTime) && 0 == u.UserSiYuanSubscriptionStatus
	return true
}

```

(1)
```go
func IsPaidUser() bool {
	// S3/WebDAV data sync and backup are available for a fee https://github.com/siyuan-note/siyuan/issues/8780

	if IsSubscriber() {
		return true
	}

	u := Conf.GetUser()
	if nil == u {
		//return false
		return true
	}
	//return 1 == u.UserSiYuanOneTimePayStatus
	return true
}
```

- `app/src/util/needSubscribe.ts`:

```js
export const needSubscribe .. {
	...
	//return true;
	return false;
}
```

### Membership Icons (Crown) : iconVIP (app/appearance/icons/material/icon.js), SIYUAN_IMAGE_VIP (app/src/constants.ts)

- Icon choice logic : `app/src/config/account.ts`
 
## REQUIREMENTS:

- `node`
- `pnpm : npm install -g pnpm@9.1.1`
- `golang`
- `mingw64 -> gcc`

`git clone https://github.com/siyuan-note/siyuan.git`

## TESTING:

### KERNEL

```
cd kernel
$env:CGO_ENABLED=1
go build --tags "fts5" -o "../app/kernel/SiYuan-Kernel.exe"
cd ../app/kernel
./SiYuan-Kernel.exe --wd=.. --mode=dev
```

### UI

```
cd siyuan/app
echo "run either dev or build"
pnpm run dev -> webview compilation (shitty pdf preview page) 
pnpm run build -> webview compilation (good pdf prewiew page)
pnpm run start 
```  

## Electron-Builder (For creating Windows Executables):

```
`pnpm run dist`
```
