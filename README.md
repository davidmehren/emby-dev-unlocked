# emby-dev-unlocked
Emby (dev) with the premium Emby Premiere features unlocked.

## Latest version
[4.1](https://github.com/nicolahinssen/emby-dev-unlocked/releases/tag/4.1)

## Releases

[Arch Linux - emby-server-dev-unlocked](https://aur.archlinux.org/packages/emby-server-dev-unlocked/)

## Modifications

[PluginSecurityManager.cs.patch](https://github.com/nicolahinssen/emby-dev-unlocked/blob/master/patches/PluginSecurityManager.cs.patch)

Before compilation, simply patch the existing file:
```
patch -N -p1 -r - Emby.Server.Implementations/Security/PluginSecurityManager.cs < ../PluginSecurityManager.cs.patch
```
[connectionmanager.js](https://github.com/nicolahinssen/emby-dev-unlocked/blob/master/replacements/connectionmanager.js)

The included version of this in the source distribution is minified. Thus, making a patch is difficult.
The only difference boils down to replacing ``self.getRegistrationInfo`` with this:

```
self.getRegistrationInfo = function(feature, apiClient) {
    var cacheKey = "regInfo-" + apiClient.serverInfo().Id;
    appStorage.setItem(cacheKey, JSON.stringify({
        lastValidDate: new Date().getTime(),
        deviceId: self.deviceId()
    }));
    return Promise.resolve();
}
```

## Special Thanks
[nvllsvm](https://github.com/nvllsvm)
