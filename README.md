# Webpack source map + InlineChunkHtmlPlugin bug MWE

Steps to reproduce:

- Setup Webpack with `devtool: "eval-source-map"` and `react-dev-utils/InlineChunkHtmlPlugin`.
- Use a .js file that includes `</script>` in a comment.

The `</script>` tag gets included in the inlined HTML via the source map, confusing the browser, which interprets it as an actual closing script tag.

You can see an example broken HTML file in `dist/index.html`. `firefox_screenshot.png` shows what the file looks like in Firefox.

I encountered this bug when using [react-markdown](https://www.npmjs.com/package/react-markdown) in a project. react-markdown imports [micromark](https://www.npmjs.com/package/micromark), which includes an offending `</script>` on [this line](https://github.com/micromark/micromark-extension-gfm-footnote/blob/740919f2c98248c1f978515410c5d995c5dade00/dev/lib/html.js#L13).
