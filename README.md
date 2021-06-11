# jekyll-mathjax-csp

See the README at [fmeum/jekyll-mathjax-csp](https://github.com/fmeum/jekyll-mathjax-csp/tree/switch_to_mathjax_3) to see how to use the plugin.

Changes:
- Improved compatibility with jekyll-minify
  - The hashes were generated against the unminified version, after jekyll-minify the inline styles were minified, invalidating the original hashes.
- Automatically create `csp.conf` which maps the `$uri` variable in nginx to `$csp`
  - Specify `default_csp` option in the config, add `[CSP]` in the `style-src` to indicate where the style hashes should be added.
    - Example (and fallback value): `"default-src 'self'; style-src 'self' [CSP];"`
  - Use by importing `csp.conf` into the http block in your nginx config, then inside the server block add `add_header Content-Security-Policy $csp always;`
- Removed `Remember to <link> in external stylesheet!` message.

### Warning: Add `csp.conf` into the exclusions inside your `_config.yml`, otherwise you will enter an infinite loop.

## License

MIT
