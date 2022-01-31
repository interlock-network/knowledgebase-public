# Trust On First Use

As mentioned in [interlock-extension](./interlock-extension.md) we use the
[visual-blockhash](./visual-blockhash.md) as a
[visual-threat-indicator](./visual-threat-indicator.md) to determine if a website
is malicious. Put differently, if a website's favicon looks like the favicon of
a trusted website we lock it. So, how do we determine if a website is _trusted_?
Well if we saw Website A before we saw Website B (and they have similar blurry
favicons) we block Website B. Is it rigorous? No, not any more than blockhashing
the favicon, but it is effective (and cheap) the vast majority of the time.

#threat-detection