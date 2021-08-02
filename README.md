# Rush errors out following a symbolic link

1. On MacOS
1. `rush update`
1. `rush deploy --overwrite -p test`

Rush will fail with:

```
ERROR: Internal Error: The path ends prematurely at: /path/to/common/temp/node_modules/.pnpm/puppeteer@10.1.0/node_modules/puppeteer/.local-chromium/mac-884014/chrome-mac/Chromium.app/Contents/Frameworks/Chromium
Framework.framework/Versions/Current/Chromium Framework
You have encountered a software defect. Please consider reporting the issue to the maintainers of this application.
```

This is because there is a symbolic link in the middle of the path, more specifically at `/path/to/common/temp/node_modules/.pnpm/puppeteer@10.1.0/node_modules/puppeteer/.local-chromium/mac-884014/chrome-mac/Chromium.app/Contents/Frameworks/Chromium
Framework.framework/Versions/Current`:

```
{
  kind: 'link',
  nodePath: '/path/to/common/temp/node_modules/.pnpm/puppeteer@10.1.0/node_modules/puppeteer/.local-chromium/mac-884014/chrome-mac/Chromium.app/Contents/Frameworks/Chromium Framework.framework/Versions/Current',
  linkTarget: '/path/to/common/temp/node_modules/.pnpm/puppeteer@10.1.0/node_modules/puppeteer/.local-chromium/mac-884014/chrome-mac/Chromium.app/Contents/Frameworks/Chromium Framework.framework/Versions/92.0.4512.0'
}
```

## Tested on

* MacOS 11.5 Intel
* Rush 5.50
* Node 14.17.0

