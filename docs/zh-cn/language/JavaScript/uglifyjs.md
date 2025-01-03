# uglify-js

## 1. 安装

`npm install -g uglify-js`

## 2. 命令

```shell
Usage: uglifyjs [files...] [options]

Options:
  -h, --help                               Print usage information.
                                           `--help options` for details on available options.
  -v, -V, --version                        Print version number.
  -p, --parse <options>                    Specify parser options.
  -c, --compress [options]                 Enable compressor/specify compressor options.
  -m, --mangle [options]                   Mangle names/specify mangler options.
  --mangle-props [options]                 Mangle properties/specify mangler options.
  -b, --beautify [options]                 Beautify output/specify output options.
  -O, --output-opts <options>              Output options (beautify disabled).
  -o, --output <file>                      Output file (default STDOUT).
  --annotations                            Process and preserve comment annotations.
  --no-annotations                         Ignore and discard comment annotations.
  --comments [filter]                      Preserve copyright comments in the output.
  --config-file <file>                     Read minify() options from JSON file.
  -d, --define <expr>[=value]              Global definitions.
  -e, --enclose [arg[,...][:value[,...]]]  Embed everything in a big function, with configurable argument(s) & value(s).
  --ie                                     Support non-standard Internet Explorer.
  --keep-fargs                             Do not mangle/drop function arguments.
  --keep-fnames                            Do not mangle/drop function names. Useful for code relying on Function.prototype.name.
  --name-cache <file>                      File to hold mangled name mappings.
  --rename                                 Force symbol expansion.
  --no-rename                              Disable symbol expansion.
  --self                                   Build UglifyJS as a library (implies --wrap UglifyJS)
  --source-map [options]                   Enable source map/specify source map options.
  --timings                                Display operations run time on STDERR.
  --toplevel                               Compress and/or mangle variables in toplevel scope.
  --v8                                     Support non-standard Chrome & Node.js.
  --validate                               Perform validation during AST manipulations.
  --verbose                                Print diagnostic messages.
  --warn                                   Print warning messages.
  --webkit                                 Support non-standard Safari/Webkit.
  --wrap <name>                            Embed everything as a function with “exports” corresponding to “name” globally.
```

## 3. 常用

`uglifyjs my_javascript.js -c -m -o my_javascript.min.js`

