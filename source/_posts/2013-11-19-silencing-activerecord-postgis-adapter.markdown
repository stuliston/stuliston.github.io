---
layout: post
title: "Silencing activerecord-postgis-adapter"
date: 2013-11-19 13:26
comments: true
categories:
---

A while back I spotted that the ```activerecord-postgis-adapter``` gem was making a fair bit of noise in  my rails console.

I was seeing lots of queries like this:

```
SELECT * FROM geometry_columns WHERE f_table_name='articles'
SELECT * FROM geometry_columns WHERE f_table_name='comments'
```

From what I understand about the issue, which is discussed [here](https://github.com/dazuma/activerecord-postgis-adapter/issues/36) and [here](https://github.com/dazuma/activerecord-postgis-adapter/issues/71), this is a meta query to discover whether a particular table has geospatial columns.

I'm plannning to reach out to the maintainer to see if I can help, but in the meantime I have a little patch to cut out the noise.

It's *possible* that you'll gain a performance boost in the process, but I haven't benchmarked it yet.

###The patch

The monkeypatch involves altering the implementation of the offending ```spatial_column_info``` method so that it optionally eager-loads specified geospatial-aware tables from a setting in your ```database.yml```.

If you *don't* provide any tables up-front in config, it'll fall back to discovering the details at runtime as it did before.

```yaml config/database.yml
development:
  #
  # other config omitted…
  #
  postgis_spacial_tables: 'articles,addresses,etc,etc'

```

```ruby config/initializers/postgis_adapter_patch.rb
# encoding: utf-8

module ActiveRecord
  module ConnectionAdapters
    module PostGISAdapter

      MainAdapter.class_eval do

        alias_method :original_spatial_column_info, :spatial_column_info

        def spatial_column_info(table_name_)
          if _postgis_spacial_tables_configured? && !_postgis_spacial_tables.include?(table_name_)
            return {}
          end

          original_spatial_column_info(table_name_)
        end

        def _postgis_spacial_tables_configured?
          _postgis_spacial_tables.present?
        end

        def _postgis_spacial_tables
          @_postgis_spacial_tables ||= (ActiveRecord::Base.configurations[Rails.env]["postgis_spacial_tables"] || '').split(',')
        end

      end
    end
  end
end

```

###Caveats

- I only load this initialiser (and therefore the patch) in ```development``` mode. Although you're free to use it how you like, be warned that it's untested in production.

- I use this against version ```0.5.0``` of the activerecord-postgis-adapter gem. As with a lot of monkeypatching, if the methods in the gem are renamed then this runs the risk of not working anymore


###Happy patching!

Please make a note in the comments if you have some improvements in either the information above or the implementation I'm suggesting.
