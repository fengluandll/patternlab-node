---
title: Editing the Configuration Options
tags:
  - docs
category: getting-started
eleventyNavigation:
  key: getting-started
  title: Editing the Configuration Options
  order: 30
---

Pattern Lab Node comes with a configuration file [(`patternlab-config.json`)](https://github.com/pattern-lab/patternlab-node/blob/master/packages/core/patternlab-config.json) that allows you to modify certain aspects of the system. The latest default values are included within. This file is shipped within [the editions](https://github.com/pattern-lab?utf8=%E2%9C%93&query=edition-node) or can be supplied from core and the command line interface. Below is a description of each configuration option and how it affects Pattern Lab Node.

### cacheBust

Instructs Pattern Lab to append a unique query string to Javascript and CSS assets throughout the frontend.

```javascript
"cacheBust": true
```

**default**: `true`

### cleanPublic

Sets whether or not to delete `public.patterns/` upon each build of Pattern Lab. When set to false, [incremental builds](https://github.com/pattern-lab/patternlab-node/wiki/Incremental-Builds) are also enabled.

**default**: `true`

### defaultPattern

Sets a specific pattern upon launch of the styleguide. This pattern will not be available in the navigation, or in view all pages. The only way to get to it will be via a refresh. Set it using the [short-hand pattern-include syntax](http://localhost:4000/docs/pattern-including.html):

```javascript
"defaultPattern": "pages-welcome",
```

A special value of `all` can also be supplied to display all patterns on load.

**default**: `all`

### defaultShowPatternInfo

Sets whether or not you want the styleguide to load with the pattern info open or closed.

**default**: `false`

### ishControlsHide

Sets whether or not to hide navigation options within the styleguide.

**default**:

```javascript
"ishControlsHide": {
  "s": false,
  "m": false,
  "l": false,
  "full": false,
  "random": false,
  "disco": false,
  "hay": true,
  "mqs": false,
  "find": false,
  "views-all": false,
  "views-annotations": false,
  "views-code": false,
  "views-new": false,
  "tools-all": false,
  "tools-docs": false
}
```

### ishViewportRange

Sets the boundaries of each of the viewport toggles, 'S'mall, 'M'edium, and 'L'arge. Clicking on one of these buttons will randomly set the ish Viewport to a value within the given range. Setting the range to the same number can effectively set an exact value. The first entry in `ishViewportRange.s` is the `ishViewportMinimum`, which is now obsolete. The second entry in `ishViewportRange.l` is the `ishViewportMaximum`, which is now also obsolete.

**default**:

```javascript
"ishViewportRange": {
  "s": [240, 500],
  "m": [500, 800],
  "l": [800, 2600]
},
```

### logLevel

Sets the level of verbosity for Pattern Lab Node logging.

- `error` will output a message as a thrown error
- `warning` will output all warnings plus above
- `info` will output all info messages, plus above (intended default)
- `debug` will output all debug messages, plus above
- `quiet` will output ZERO logs

This replaces the now obsolete `debug` flag.

**default**: `info`

### outputFileSuffixes

Sets the naming of output pattern files. Suffixes are defined for 'rendered', 'rawTemplate', and 'markupOnly' files. This configuration is needed for some PatternEngines that use the same input and output file extensions. Most users will not have to change this.

```javascript
"outputFileSuffixes": {
  "rendered": ".rendered",
  "rawTemplate": "",
  "markupOnly": ".markup-only"
},
```

### paths

Sets the configurable source and public directories for files Pattern Lab Node operates within. Build, copy, output, and server operations rely upon these paths. Some paths are relative to the current UIKit. See UIKit configuration for more info. Note the `patternlabFiles` which help create the front end styleguide. Note also the intentional repetition of the nested structure, made this way for maximum flexibility. These are unlikely to change unless you customize your environment or write custom UIKits.

**default** :

```javascript
  "paths": {
    "source": {
      "root": "./source/",
      "patterns": "./source/_patterns/",
      "data": "./source/_data/",
      "meta": "./source/_meta/",
      "annotations": "./source/_annotations/",
      "styleguide": "dist/",
      "patternlabFiles": {
        "general-header": "views/partials/general-header.mustache",
        "general-footer": "views/partials/general-footer.mustache",
        "patternSection": "views/partials/patternSection.mustache",
        "patternSectionSubtype": "views/partials/patternSectionSubtype.mustache",
        "viewall": "views/viewall.mustache"
      },
      "js": "./source/js",
      "images": "./source/images",
      "fonts": "./source/fonts",
      "css": "./source/css"
    },
    "public": {
      "root": "public/",
      "patterns": "public/patterns/",
      "data": "public/styleguide/data/",
      "annotations": "public/annotations/",
      "styleguide": "public/styleguide/",
      "js": "public/js",
      "images": "public/images",
      "fonts": "public/fonts",
      "css": "public/css"
    }
  },
```

### patternExtension

Sets the panel name and language for the code tab on the styleguide. Since this only accepts one value, this is a place where mixed pattern trees (different PatternEngines in the same instance of Pattern Lab) does not quite work.

**default**: `mustache`

### patternStateCascade

See the [Pattern State Documentation](http://patternlab.io/docs/pattern-states.html#node)

**default**:

```javascript
"patternStateCascade": ["inprogress", "inreview", "complete"],
```

### patternExportDirectory

Sets the location that any export operations should output files to. This may be a relative or absolute path.

**default**: `./pattern_exports/`

### patternExportPatternPartials

Sets an array of patterns (using the [short-hand pattern-include syntax](http://localhost:4000/docs/pattern-including.html)) to be exported after a build.

For example, to export the navigation, header, and footer, one might do:

```javascript
"patternExportPatternPartials": ["molecules-primary-nav", "organisms-footer", "organisms-header"],
```

**default**: `[]`

### serverOptions

Sets live-server options. See the [live-server documentation](https://github.com/pattern-lab/live-server#usage-from-node) for more details.

**default**:

```javascript
"serverOptions": {
  "wait": 1000
},
```

### starterkitSubDir

[Starterkits](http://localhost:4000/docs/advanced-starterkits.html) by convention house their files within the `dist/` directory. Should someone ever wish to change this, this key is available.

**default**:

```javascript
"starterkitSubDir": "dist",
```

### styleGuideExcludes

Sets whole pattern types to be excluded from the "All" patterns page on the styleguide. This is useful to decrease initial load of the styleguide. For example, to exlude all patterns under `templates` and `pages`, add the following:

```javascript
"styleGuideExcludes": [
	"templates",
	"pages"
]
```

These template and page patterns would still be accessible via navigation.

**default**: `[]`

### theme

Sets the theme options for the styleguide. There are three options: 'color', 'density', and 'layout'.

Available values are:

```javascript
"theme" : {
  "color" : "dark" | "light",
  "density" : "compact" | "cozy" | "comfortable",
  "layout" : "horizontal" | "vertical"
}
```

See the [initial release notes](https://github.com/pattern-lab/styleguidekit-assets-default/releases/tag/v4.0.0-alpha.2) for the theme feature for example output.

**default**:

```javascript
"theme" : {
  "color" : "dark",
  "density" : "compact",
  "layout" : "horizontal"
}
```

### uikits

Introduced in Pattern Lab Node v3, UIKits are a new term in the Pattern Lab [Ecosystem](http://patternlab.io/docs/advanced-ecosystem-overview.html). They are an evolution of the original Styleguidekit pattern which separated front-end templates from front-end assets like stylesheets and code. The existing `styleguidekit-assets-default` and `styleguidekit-mustache-default` have merged into `uikit-workshop`.

`uikits` accepts an array of UIKit objects, shipping with the one above.

- `name`: the name of the UIKit
- `outputDir` where to output this UIKit relative to the current root. By leaving this empty we retain the existing Pattern Lab 2.X behavior, outputting to `<project_root>/public`. If you had multiple UIKits, however, you would provide different values, such as:

```javascript
  "uikits": [
    {
      "name": "uikit-workshop",
      "outputDir": "workshop",
      ...
    },
    {
      "name": "uikit-storefront",
      "outputDir": "storefront",
      ...
    }
  ]
```

- `enabled`: quickly turn on or off the building of this UIKit
- `excludedPatternStates`: tell Pattern Lab not to include patterns with these states in this UIKit's output
- `excludedPatternTags`: tell Pattern Lab not to include patterns with these tags in this UIKit's output
  - [currently not supported](https://github.com/pattern-lab/patternlab-node/issues/844)

Important details:

- the [default `paths.source` object paths](https://github.com/pattern-lab/patternlab-node/pull/840/commits/a4961bd5d696a05fb516cdd951163b0f918d5e19) within `patternlab-config.json` are now relative to the current UIKit. See the [structure of uikit-workshop](https://github.com/pattern-lab/patternlab-node/tree/master/packages/uikit-workshop) for more info
- the [default `paths.public` object paths](https://github.com/pattern-lab/patternlab-node/pull/840/commits/812bab3659f504043e8b61b1dc1cdac71f248449) within `patternlab-config.json` are now relative to the current UIKit's `outputDir`. Absolute paths will no longer work. Someone could test putting an absolute path in a UIKit `outputDir` property and see what happens I suppose.
- `dependencyGraph.json` has moved to the project root rather than `public/` as we should only retain one

**default**:

```javascript
  "uikits": [
    {
      "name": "uikit-workshop",
      "outputDir": "",
      "enabled": true,
      "excludedPatternStates": [],
      "excludedTags": []
    }
  ]
```
