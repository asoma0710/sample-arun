# `filldisk.js` - Masterful trolling with HTML5 localStorage

#### Use HTML5 `localStorage` to completely fill up Chrome, Safari, and IE users' hard disks.

#### Check out the [demo](http://www.filldisk.com)!

#### Info about how this works [in this blog post](http://feross.org/fill-disk/).

## Features:

- Fills up the user's hard disk on Chrome, Safari (iOS and desktop), and IE.
- Fills up **1 GB every 16 seconds** on my Macbook Pro Retina (with solid state drive)
- Tested with latest Chrome (25), Safari (6), IE (10).
- For 32-bit browsers, like Chrome, **the entire browser may crash** before the disk is filled.
- Does not work on Firefox, since Firefox's implementation of localStorage is smarter.
- Includes a button to reclaim your disk space ;)

## How it works

The [HTML5 localStorage](http://www.w3.org/TR/webstorage/) standard was developed to allow sites to store larger amounts of data (like 5-10 MB) than was previously allowed by cookies (like 4KB). The standard is supported in all modern browsers (Chrome, Firefox, Safari, IE, etc.).

The standard anticipated that sites might abuse this feature ;) and advised that browsers limit the total amount of storage space that each origin could use. Quoting from the HTML5 spec:

> User agents should limit the total amount of space allowed for storage areas.

The [current limits](http://en.wikipedia.org/wiki/Web_storage#Storage_size) are:

- 2.5 MB per origin in Google Chrome
- 5 MB per origin in Mozilla Firefox and Opera
- 10 MB per origin in Internet Explorer

However, what if we get clever and make lots of subdomains like `1.filldisk.com`, `2.filldisk.com`, `3.filldisk.com`, and so on? Should we get 5MB of space per subdomain? **The standard says no.**

> User agents should guard against sites storing data under the origins other affiliated sites, e.g. storing up to the limit in a1.example.com, a2.example.com, a3.example.com, etc, circumventing the main example.com storage limit.
>
> A mostly arbitrary limit of five megabytes per origin is recommended.

However, **Chrome, Safari, and IE currently do not implement any such storage limit**. Thus, cleverly coded websites effectively have unlimited storage space on their visitor's computer.

I wrote [http://www.filldisk.com](fill-disk.js) as a proof-of-concept to include with the bug reports I filed. Bug reports here:

- [Chromium bug report](https://code.google.com/p/chromium/issues/detail?id=178980)
- [Apple bug report](http://openradar.appspot.com/radar?id=2792401)
- [IE Bug Report](https://connect.microsoft.com/IE/feedback/details/780246/localstorage-stores-unlimited-amount-of-data-with-unlimited-subdomains-against-spec) (requires login)
- Opera bug report (closed tracker, bug ID: DSK-383073) - fills to 75MB in my testing, which isn't so bad.

## How to reclaim space (last resort)

If clicking on the "Stop the madness" button fails to give back your disk space, you can reclaim it manually (in Chrome) by going to Preferences > Show advanced settings... > Content settings > All cookies and site data... > search for "filldisk" > Remove all.

I'm less familiar with other browsers, but deleting your cookies and cache will definitely do the trick.


