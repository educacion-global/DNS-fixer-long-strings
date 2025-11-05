# DNS-fixer-long-strings

Split long DNS TXT / DKIM records into DNS-friendly segments (≤255 bytes each) and produce output ready to paste into Google Domains or other registrars.

## Features
- Byte-aware splitting (handles multi-byte UTF-8 characters safely)
- Returns quoted segments by default (e.g. "part1" "part2")
- Simple CLI for one-off usage
- Small test file with examples

## Usage (JS)
```js
const { formatDnsTxtRecord, joinForGoogleDomains } = require('dns-fixer-long-strings');

const dkim = 'v=DKIM1; k=rsa; p=MIIBIjANBgk...';
const segments = formatDnsTxtRecord(dkim); // array of quoted segments
console.log(segments.join('\n'));

// Or produce a single string formatted for Google Domains:
console.log(joinForGoogleDomains(segments)); // => '"part1" "part2" ...'
```

## CLI
- Install globally: npm i -g .
- Usage:
  - dns-fixer -s "your long txt"         # prints quoted segments, one per line
  - dns-fixer -s "..." -c 255 -j space   # -j space will join as a single line separated by spaces (Google Domains)

## Examples
```bash
# Split a DKIM value and print segments
node bin/dns-fixer.js -s 'v=DKIM1; k=rsa; p=MIIBIjANBgkqh...'

# Join segments into one line separated by spaces for Google Domains
node bin/dns-fixer.js -s '...' -j space
```

## License
MIT