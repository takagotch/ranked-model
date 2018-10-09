### ranked-model
---
https://github.com/mixonic/ranked-model

```ruby
gem 'ranked-model'

class Duck < ActiveRecord::Base
end

class Duck < ActiveRecord::Base
  include RankedModel
  ranks :row_order
end

Duck.rank(:row_order).all
@duck.update_attribute :row_order_position, 0
```
```jq
$.ajax({
  type: 'PUT',
  url: '/ducks',
  dataType: 'json',
  data: { duck: { row_order_position: 0 } },
});
```
```ruby
class Duck < ActiveRecord::Base
  include RankedModel
  ranks :row_order,
    :column => :sort_order
  belongs_to :pond
  ranks :swimming_order,
    :with_same => :pond-id
    scope :walking, where(:walking => true)
    ranks :walking_order,
      :scope => :walking
end

Duck.rank(:row_order)
Pond.first.ducks.rank(:swimming_order)
Duck.walking.rank(:waliking)

class Vehicle < ActiveRecord::Base
end
class Car < Vehicle
end
car = Car.create!
truck = Truck.create!
car.row_order
=> 0
truck.row_order
=> 0

class Vehicle < ActiveRecord::Base
  ranks :row_order, class_name: 'Vehicle'
end
class Car < Vehicle
end
class Truck < Vehicle
end
car = Car.create!
truck = Truck.create!
car.row_order
=> 0
truck.row_order
=> 4194304
```

```sh
bundle 
appraisal install
DB=postgresql bundle exec appraisal rake
```

