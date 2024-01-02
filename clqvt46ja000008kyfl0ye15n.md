---
title: "My VSCode settings for dart language - flutter 120 line length in JSON file"
seoTitle: "My VSCode settings for dart language - flutter 120 line length in JSON"
seoDescription: "My VSCode settings for dart language - flutter 120 line length in JSON file"
datePublished: Tue Jan 02 2024 03:45:42 GMT+0000 (Coordinated Universal Time)
cuid: clqvt46ja000008kyfl0ye15n
slug: my-vscode-settings-for-dart-language-flutter-120-line-length-in-json-file
tags: flutter

---

To open VSCode settings in JSON format, use the following command: `ctrl` + `shift` + `p` and type "user settings json".

```json
​{
  "dart.lineLength": 120,
  "[dart]": {
    "editor.rulers": [120],
    "editor.codeActionsOnSave": {
      "source.fixAll": "explicit"
    },
    "editor.formatOnSave": true
  },
  "dart.flutterHotReloadOnSave": "all",
  "dart.hotReloadOnSave": "all",
  "dart.debugExternalPackageLibraries": false,
  "dart.debugSdkLibraries": false,
  "dart.additionalAnalyzerFileExtensions": ["./analysis_options.yaml"]
}
```
