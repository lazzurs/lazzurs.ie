# lazzurs.ie

GitHub Pages site for the `lazzurs.ie` apex. Its only job is to serve the
Matrix well-known files that delegate the `lazzurs.ie` server name to the
family's Family Chat homeserver (unicornops/family-chat#237):

- `/.well-known/matrix/server` → `{"m.server": "<serving-host>.safechat.family:443"}`
  (the `:443` is required; without it federation falls back to port 8448)
- `/.well-known/matrix/client` → `{"m.homeserver": {"base_url": "https://<serving-host>.safechat.family"}}`

`<serving-host>` is generated when the migration provisions the new
instance; the Family Chat panel shows the exact JSON to publish. Until then
both files are `{}`, which Matrix servers and clients treat as "no
delegation".

GitHub Pages sends `Access-Control-Allow-Origin: *`, which web clients need
on the client file. `.nojekyll` is required, otherwise Jekyll skips the
`.well-known` directory.

DNS for the apex lives in neamh/octodns (`config/lazzurs.ie.yaml`).
