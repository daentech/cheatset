# cheatset

[![Gem Version](https://badge.fury.io/rb/cheatset.png)](http://badge.fury.io/rb/cheatset)

Generate your own cheat sheets as docsets for [Dash](http://kapeli.com/dash)!
Use this simple command line tool and write your cheat sheets in an easy
language (Ruby DSL).

## Installation

    $ sudo gem install cheatset

Note: this requires the Xcode Command Line Tools to be installed. Install them using this:

    $ xcode-select --install
    
If it still doesn't work, it most likely means you got Xcode 5.1 which just broke a lot of gems. See [Issue #2](https://github.com/Kapeli/cheatset/issues/2#issuecomment-37369283) for more details and a workaround.

## Contributions

If you make an useful cheat sheet, please [contribute it](https://github.com/Kapeli/cheatsheets#readme) to Dash.

## Usage

Write a file (here `sample.rb`) containing your cheat sheet data, e.g.:

```ruby
cheatsheet do
  title 'Sample'             # Will be displayed by Dash in the docset list
  docset_file_name 'Sample'  # Used for the filename of the docset
  keyword 'sample'           # Used as the initial search keyword (listed in Preferences > Docsets)
  resources 'resources_dir'  # An optional resources folder which can contain images or anything else
  
  introduction 'My *awesome* cheat sheet'  # Optional, can contain Markdown or HTML

  # A cheat sheet must consist of categories
  category do
    id 'Windows'  # Must be unique and is used as title of the category

    entry do
      command 'CMD+N'         # Optional
      command 'CMD+SHIFT+N'   # Multiple commands are supported
      name 'Create window'    # A short name, can contain Markdown or HTML
      notes 'Some notes'      # Optional longer explanation, can contain Markdown or HTML
    end
    entry do
      command 'CMD+W'
      name 'Close window'
    end
  end

  category do
    id 'Code'
    entry do
      name 'Code sample'
      notes <<-'END'
        ```ruby
        sample = "You can include code snippets as well"
        ```
        Or anything else **Markdown** or HTML.
      END
    end
  end

  notes 'Some notes at the end of the cheat sheet'
end
```

To convert this file to a docset, call

    $ cheatset generate sample.rb

The following values may contain Markdown or HTML:

* The `introduction` and the `notes` of the cheat sheet
* The `name` and the `notes` of the entries

Syntax highlighting is supported (see Ruby code in the sample). For a list of supported languages, see [Rouge's Demo Page](http://rouge.jayferd.us/demo)

For more complete examples look at some of
[the actual cheat sheets](https://github.com/Kapeli/cheatsheets/tree/master/cheatsheets).

## Thanks

[Nix-wie-weg](https://github.com/Nix-wie-weg/dasheets) for the initial code.
