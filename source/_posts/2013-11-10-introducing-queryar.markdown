---
layout: post
title: "Introducing QueryAr"
date: 2013-11-10 19:59
comments: true
published: false
categories:
- Ruby
- OSS
- ActiveRecord
---

I'd like to describe a small - and currently very focused - gem I've been working on.

<!-- more -->

*QueryAr gives you a concise DSL to confidently build filtered, scoped, paged and sorted ActiveRecord queries, based on a parameters hash.*

### Really quick usage example:

Given this ActiveRecord model:

```ruby
class User
  scope :older_than, ->(years) { where("age > ?", years) }
end
```

You can declare a query:

```ruby
class UserQuery
  include QueryAr

  defaults sort_by: 'last_name'

  queryable_by  :first_name, :last_name
  scopeable_by  :older_than
end
```

Then use it to query your model safely and succinctly from controller params:

```ruby

# GET /users
# params = { "older_than"=>30, "first_name"=>"Stu", "limit"=>5, "offset"=>0 }

def index
  query = UserQuery.new(params)
  render json: query.all
end
```

### Want to find out more?

Head over to the project's home on [GitHub](https://github.com/hooroo/query_ar) for the latest information. You're very welcome to make suggestions, ask for features or get involved!
