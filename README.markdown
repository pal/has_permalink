has_permalink
=============

Instalation
-----------

You can use I18n-JS as plugin and gem. Choose what's best for you!

	script/plugin install git://github.com/fnando/has_permalink.git

or
	gem install permalink

Usage
-----

Add the method call `has_permalink` to your model. Your model should have a `permalink` attribute.

    class Page < ActiveRecord::Base
      has_permalink :title
    end

You can specify the permalink field:

    class page < ActiveRecord::Base
      has_permalink :title, :to => :title_permalink
    end

If you don't want to use `has_permalink`, you can call `'some text'.to_permalink` string method and
manage the permalink process by yourself.

Permalinks are not unique by default. `has_permalink` overrides `to_param` as following:

    def to_param
      "#{id}-#{permalink}"
    end

You can define the `to_param` format:

    class Page < ActiveRecord::Base
      has_permalink :title, :to_param => %w(id permalink page)
    end

The above settings will generate something link `100-some-title-page`. By overriding `to_param` method you don't have to change a thing on your app routes.

If you want to generate unique permalink, use the option `:unique`:

	class Page < ActiveRecord::Base
	  has_permalink :title, :unique => true, :to_param => :permalink
	end

The permalink is generated using `ActiveSupport::Multibyte::Chars` class; this means that characters will properly replaced from `áéíó` to `aeio`, for instance.

The permalink is created when `before_validation` callback is evaluated. This plugin also tries
to generate a permalink when `before_save` callback is evaluated and the instance has no permalink set.

## License

Copyright (c) 2008 Nando Vieira, released under the MIT license

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
"Software"), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND
NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE
LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION
OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION
WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.