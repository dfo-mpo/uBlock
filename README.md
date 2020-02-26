[![Build](https://travis-ci.org/gorhill/uBlock.svg?branch=master)](https://travis-ci.org/gorhill/uBlock)
[![Crowdin](https://d322cqt584bo4o.cloudfront.net/ublock/localized.svg)](https://crowdin.com/project/ublock)
[![License](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://github.com/gorhill/uBlock/blob/master/LICENSE.txt)

*** 

<h1 align="center">
<sub>
<img  src="https://raw.githubusercontent.com/gorhill/uBlock/master/doc/img/icon38@2x.png"
      height="38"
      width="38">
</sub>
uBlock Origin
</h1>
<p align="center">
<sup> <!-- Pronounciation -->
      pronounced <i>you-block origin</i> (<code>/ˈjuːˌblɒk/</code>) — <i>you</i> decide what enters your browser.
</sup>
<br>
<sup> <!-- Languages -->
      <img src="https://raw.githubusercontent.com/gorhill/uBlock/master/doc/img/languageicon-36.png" width="18" height="18">
      <sup>
            English,
            <a href="https://github.com/fang5566/uBlock/blob/master/README.md#ublock-origin">Chinese (中文)</a>,
            <a href="https://github.com/delightbot/uBlock/blob/master/README.md#ublock-origin">Korean (한국어)</a>,
            <a href="https://github.com/ialexsilva/uBlock/blob/master/README.md#ublock-origin">Português (Brasil)</a>
      </sup>
</sup>
<br>
<br>
<sup><a href="https://github.com/gorhill/uBlock/wiki/uBlock-Origin-is-completely-unrelated-to-the-web-site-ublock.org"><b>BEWARE!</b> uBlock Origin is (and has always been) COMPLETELY UNRELATED to the web site <code>ublock.org</code></a>.</sup>
</p>

***

**An efficient blocker add-on for various browsers. Fast, potent, and lean.**

uBlock Origin is **NOT** an "ad blocker": [it is a wide-spectrum blocker](https://github.com/gorhill/uBlock/wiki/Blocking-mode) -- which happens to be able to function as a mere "ad blocker". The default behavior of uBlock Origin when newly installed is to block ads, trackers and malware sites -- through [_EasyList_](https://easylist.github.io/#easylist), [_EasyPrivacy_](https://easylist.github.io/#easyprivacy), [_Peter Lowe’s ad/tracking/malware servers_](https://pgl.yoyo.org/adservers/policy.php), various lists of [malware](http://www.malwaredomainlist.com/) [sites](http://www.malwaredomains.com/), and uBlock Origin's [own filter lists](https://github.com/uBlockOrigin/uAssets/tree/master/filters).

# DFO Fork
Code is reviewed. Upstream changes are reviewed before being merged to the fork.

## What are we looking for?
Primarily data exfiltration - scraping and sending data elsewhere. To a lesser extent, data injection. Without exfiltration, injection/impersonation is of questionable value.

## Files of interest
- src/js/cloud-ui.js
    - Cloud storage, but must be enabled, and is [user-specific inside their own account](https://github.com/gorhill/uBlock/wiki/Cloud-storage). It is for storing user settings only.
- src/js/redirect-engine.js 

## Useful Substring Searches
- .post(
- .put(
- .listen(

## Building
````
sudo apt -yqq install git zip
git clone https://github.com/dfo-mpo/uBlock
git clone https://github.com/uBlockOrigin/uAssets
cd uBlock

# Wants to make /assets
sudo ./tools/make-assets.sh

./tools/make-chromium.sh all

````

## Deployment
`ignoreScriptInjectFilters` must be set to `true`. It would be near impossible vouch for any scriptlet injection.
`ignoreRedirectFilters` should also be considered to be `true`.
`cloudStorageEnabled` is a setting which respects Chrome's policy, but could also be set to `false` for an extra layer.

This can be done with an `adminSettings` file with
````
  {
      "userSettings": {
            "cloudStorageEnabled": false,
      },
      "hiddenSettings": {
            "ignoreScriptInjectFilters": true,
            "ignoreRedirectFilters": true
      }
  }
  ````

This file can also have a whitelist section.
````
{
    "whitelist": [
        "about-scheme",
        "dfo-mpo.gc.ca"
    ]
}
````

### Some notes
- [CSP has nothing to do with cloud](https://github.com/gorhill/uBlock/wiki/Dashboard:-Settings#block-csp-reports)

## License

[GPLv3](https://github.com/gorhill/uBlock/blob/master/LICENSE.txt).
