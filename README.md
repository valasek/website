[![Netlify Status](https://api.netlify.com/api/v1/badges/55d70577-8dcd-40be-8032-58b23ba8c4a5/deploy-status)](https://app.netlify.com/sites/stanislavvalasek/deploys)

# www.stanislavvalasek.com

Personal website of [Stanislav Valasek](www.stanislavvalasek.com).

## Standing on the shoulded of giants
Static page generator [Hugo](https://gohugo.io/) using [**academic theme**](https://github.com/gcushen/hugo-academic) hosted on [Netlify](https://www.netlify.com/).

## License

Copyright 2020-present [Stanislav Valasek](www.stanislavvalasek.com).

Released under the [MIT](https://github.com/sourcethemes/academic-kickstart/blob/master/LICENSE.md) license.

## Notes for updates
Localy site can be started using the command

```
hugo server
```

In case of any error
```
Error: Error building site: "...": failed to extract shortcode: template for shortcode "..." not found
```

```
hugo mod clean
hugo mod get -u ./...
```

and error
```
Error: from config: failed to resolve output format "headers" from site config
```

In your config/_default/config.yaml file change the line

home: [HTML, RSS, JSON, WebAppManifest, headers, redirects]

to

home: [] #[HTML, RSS  , JSON, WebAppManifest, headers, redirects]

then at the command line type hugo mod get. Then return the home: line back to its original contents and all should be well when you type hugo server.