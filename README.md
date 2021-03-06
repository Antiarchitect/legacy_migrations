# LegacyMigrations

This plugin implements a simple, expressive syntax for migrating data from one data 
structure to another. Here's a simple example:

  require 'legacy_migrations'

  transfer_from Person, :to => Animal do
    from :name, :to => :pet_name
  end

This transfers data from the people table to the animals table,
mapping the people's _name_ column to animals' _pet\_name_ column.

But that's just the beginning. This plugin also:

* Reports invalid data by using your application's own validation errors for easy data cleanup
  (just use ActiveRecord validations and after running the script from
  the command line, the output will give you helpful details about validation errors.)
* Maps foreign keys between the databases (currently not implemented)
* Gives you a bunch of options for mapping fields between tables.

## Example

In some file in your rails app (perhaps db/seeds.rb?)

    require 'legacy_migrations'

    transfer_from Person, :to => Animal do
      from :name, :to => :pet_name
      from :sex, :to => :gender do |sex|
        sex == 'm' ? 'male' : 'female'
      end
    end


OR, copy all columns with the same name

    transfer_from Person, :to => Animal do
      match_same_name_attributes
    end

Here's a slightly more thorough blog post about it:

http://frontended.com/?p=89

Copyright (c) 2010 Bernie Telles, released under the MIT license

# This fork

This fork improves legacy_migrations gem to preserve updated_at and created_at timestamps, id of a record (when record exist it just updates it).

Andrey Voronkov, [Evrone.com](http://evrone.com)
