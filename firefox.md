# Nice addons
- [KeepassXC](https://addons.mozilla.org/en-US/firefox/addon/keepassxc-browser/)
- [ClearURLs](https://addons.mozilla.org/en-US/firefox/addon/clearurls/) - Remove tracking elements from URLs
- [LocalCDN](https://addons.mozilla.org/en-US/firefox/addon/localcdn-fork-of-decentraleyes/) - Serve CDN content from local cache
- [uBlock Origin](https://addons.mozilla.org/en-US/firefox/addon/ublock-origin/) - ❤
- [Privacy redirect](https://addons.mozilla.org/en-US/firefox/addon/privacy-redirect/) - Redirect to privacy friendly alternatives of websites
- Containerise
- Vimium
- IPFS

# about:config
- `browser.fixup.domainsuffixwhitelist.XX` -  Allow custom domain suffix to resolve
- `privacy.resistFingerprinting` - Enable resistFingerprinting

## Spoof location
Set `geo.provider.network.url`
```json
data:,{"location":{"lat":51.5,"lng":-0.11},"accuracy":1000}
```
Also setting `geo.provider.testing` to true might help

Need to close all tabs for a site before it updates

# Librewolf
Is pretty cool.